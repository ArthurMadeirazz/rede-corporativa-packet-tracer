# Configuracao Cisco

Este arquivo guarda uma base de comandos para configurar o projeto no Packet Tracer.

A ideia principal e usar VLANs no switch e subinterfaces no roteador. Esse modelo e conhecido como router-on-a-stick.

## VLANs usadas

| VLAN | Nome | Rede |
| --- | --- | --- |
| 10 | ADMINISTRACAO | 192.168.10.0/24 |
| 20 | FINANCEIRO | 192.168.20.0/24 |
| 30 | TI | 192.168.30.0/24 |
| 40 | ATENDIMENTO | 192.168.40.0/24 |
| 50 | VISITANTES | 192.168.50.0/24 |
| 60 | SERVIDORES | 192.168.60.0/24 |

## Switch principal

Exemplo usando um switch 2960.

```text
enable
configure terminal
hostname SW1

vlan 10
name ADMINISTRACAO
vlan 20
name FINANCEIRO
vlan 30
name TI
vlan 40
name ATENDIMENTO
vlan 50
name VISITANTES
vlan 60
name SERVIDORES

interface fa0/1
description LINK_PARA_ROTEADOR
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60

interface range fa0/2-5
description PCS_ADMINISTRACAO
switchport mode access
switchport access vlan 10

interface range fa0/6-9
description PCS_FINANCEIRO
switchport mode access
switchport access vlan 20

interface range fa0/10-13
description PCS_TI
switchport mode access
switchport access vlan 30

interface range fa0/14-17
description PCS_ATENDIMENTO
switchport mode access
switchport access vlan 40

interface range fa0/18-20
description PCS_VISITANTES
switchport mode access
switchport access vlan 50

interface range fa0/21-22
description SERVIDORES
switchport mode access
switchport access vlan 60

interface range fa0/23-24
description TRUNK_PARA_OUTRO_SWITCH
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60

end
write
```

## Roteador

Exemplo usando a interface `g0/0` ligada ao switch.

```text
enable
configure terminal
hostname R1

interface g0/0
description LINK_PARA_SW1
no shutdown

interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

interface g0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0

interface g0/0.40
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0

interface g0/0.50
encapsulation dot1Q 50
ip address 192.168.50.1 255.255.255.0

interface g0/0.60
encapsulation dot1Q 60
ip address 192.168.60.1 255.255.255.0

ip dhcp excluded-address 192.168.10.1 192.168.10.9
ip dhcp excluded-address 192.168.20.1 192.168.20.9
ip dhcp excluded-address 192.168.30.1 192.168.30.9
ip dhcp excluded-address 192.168.40.1 192.168.40.9
ip dhcp excluded-address 192.168.50.1 192.168.50.9

ip dhcp pool ADMINISTRACAO
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8

ip dhcp pool FINANCEIRO
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
dns-server 8.8.8.8

ip dhcp pool TI
network 192.168.30.0 255.255.255.0
default-router 192.168.30.1
dns-server 8.8.8.8

ip dhcp pool ATENDIMENTO
network 192.168.40.0 255.255.255.0
default-router 192.168.40.1
dns-server 8.8.8.8

ip dhcp pool VISITANTES
network 192.168.50.0 255.255.255.0
default-router 192.168.50.1
dns-server 8.8.8.8

end
write
```

## Comandos uteis para conferir

No switch:

```text
show vlan brief
show interfaces trunk
```

No roteador:

```text
show ip interface brief
show ip dhcp binding
show running-config
```

