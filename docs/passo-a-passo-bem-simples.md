# Passo a passo bem simples - Packet Tracer

Este guia e para configurar o projeto dentro do Cisco Packet Tracer sem pular etapa.

## Antes de comecar

Abra este arquivo:

```text
D:\ProjetosRedes2026\rede-corporativa-packet-tracer\rede-corporativa-packet-tracer.pkt
```

Se alguma porta tiver nome diferente, use o mesmo raciocinio:

- Onde estiver `g0/0`, pode aparecer como `fa0/0`, `g0/0/0` ou algo parecido no seu roteador.
- Onde estiver `fa0/1`, pode aparecer como `GigabitEthernet0/1` em alguns switches.

O importante e saber qual cabo esta ligado em qual porta.

## 1. Montar ou conferir os equipamentos

Use estes equipamentos:

- 1 roteador
- 1 switch principal
- PCs para os setores
- 1 servidor

Conecte assim:

| Equipamento | Porta | Liga em |
| --- | --- | --- |
| Roteador | g0/0 | Switch fa0/1 |
| PC Administracao | fa0 | Switch fa0/2 |
| PC Financeiro | fa0 | Switch fa0/6 |
| PC TI | fa0 | Switch fa0/10 |
| PC Atendimento | fa0 | Switch fa0/14 |
| PC Visitante | fa0 | Switch fa0/18 |
| Servidor | fa0 | Switch fa0/21 |

## 2. Configurar o switch

Clique no switch.

Entre em:

```text
CLI
```

Se aparecer uma pergunta inicial, responda:

```text
no
```

Agora cole este bloco:

```text
enable
configure terminal
hostname SW1

vlan 10
name ADMINISTRACAO
exit

vlan 20
name FINANCEIRO
exit

vlan 30
name TI
exit

vlan 40
name ATENDIMENTO
exit

vlan 50
name VISITANTES
exit

vlan 60
name SERVIDORES
exit
```

Agora configure a porta que vai para o roteador.

No nosso exemplo e a `fa0/1`:

```text
interface fa0/1
description LINK_PARA_ROTEADOR
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60
exit
```

Agora configure as portas dos computadores.

Administracao:

```text
interface range fa0/2-5
description PCS_ADMINISTRACAO
switchport mode access
switchport access vlan 10
exit
```

Financeiro:

```text
interface range fa0/6-9
description PCS_FINANCEIRO
switchport mode access
switchport access vlan 20
exit
```

TI:

```text
interface range fa0/10-13
description PCS_TI
switchport mode access
switchport access vlan 30
exit
```

Atendimento:

```text
interface range fa0/14-17
description PCS_ATENDIMENTO
switchport mode access
switchport access vlan 40
exit
```

Visitantes:

```text
interface range fa0/18-20
description PCS_VISITANTES
switchport mode access
switchport access vlan 50
exit
```

Servidor:

```text
interface range fa0/21-22
description SERVIDORES
switchport mode access
switchport access vlan 60
exit
```

Salve:

```text
end
write
```

## 3. Conferir se o switch ficou certo

Ainda no switch, digite:

```text
show vlan brief
```

Voce deve ver as VLANs:

```text
10 ADMINISTRACAO
20 FINANCEIRO
30 TI
40 ATENDIMENTO
50 VISITANTES
60 SERVIDORES
```

Depois digite:

```text
show interfaces trunk
```

Voce deve ver a porta `fa0/1` como trunk.

## 4. Configurar o roteador

Clique no roteador.

Entre em:

```text
CLI
```

Se aparecer uma pergunta inicial, responda:

```text
no
```

Agora cole este bloco:

```text
enable
configure terminal
hostname R1

interface g0/0
description LINK_PARA_SW1
no shutdown
exit
```

Agora crie as subinterfaces.

VLAN 10 - Administracao:

```text
interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit
```

VLAN 20 - Financeiro:

```text
interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
```

VLAN 30 - TI:

```text
interface g0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
exit
```

VLAN 40 - Atendimento:

```text
interface g0/0.40
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0
exit
```

VLAN 50 - Visitantes:

```text
interface g0/0.50
encapsulation dot1Q 50
ip address 192.168.50.1 255.255.255.0
exit
```

VLAN 60 - Servidores:

```text
interface g0/0.60
encapsulation dot1Q 60
ip address 192.168.60.1 255.255.255.0
exit
```

## 5. Configurar DHCP no roteador

Ainda no roteador, cole:

```text
ip dhcp excluded-address 192.168.10.1 192.168.10.9
ip dhcp excluded-address 192.168.20.1 192.168.20.9
ip dhcp excluded-address 192.168.30.1 192.168.30.9
ip dhcp excluded-address 192.168.40.1 192.168.40.9
ip dhcp excluded-address 192.168.50.1 192.168.50.9

ip dhcp pool ADMINISTRACAO
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8
exit

ip dhcp pool FINANCEIRO
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
dns-server 8.8.8.8
exit

ip dhcp pool TI
network 192.168.30.0 255.255.255.0
default-router 192.168.30.1
dns-server 8.8.8.8
exit

ip dhcp pool ATENDIMENTO
network 192.168.40.0 255.255.255.0
default-router 192.168.40.1
dns-server 8.8.8.8
exit

ip dhcp pool VISITANTES
network 192.168.50.0 255.255.255.0
default-router 192.168.50.1
dns-server 8.8.8.8
exit
```

Salve:

```text
end
write
```

## 6. Configurar o servidor

Clique no servidor.

Va em:

```text
Desktop > IP Configuration
```

Preencha:

```text
IP Address: 192.168.60.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.60.1
DNS Server: 8.8.8.8
```

## 7. Configurar os PCs

Em cada PC:

1. Clique no PC.
2. Va em `Desktop`.
3. Clique em `IP Configuration`.
4. Marque `DHCP`.

Cada PC deve receber um IP conforme o setor:

| Setor | IP esperado |
| --- | --- |
| Administracao | 192.168.10.x |
| Financeiro | 192.168.20.x |
| TI | 192.168.30.x |
| Atendimento | 192.168.40.x |
| Visitantes | 192.168.50.x |

## 8. Testar a rede

Clique em um PC da Administracao.

Va em:

```text
Desktop > Command Prompt
```

Teste o gateway:

```text
ping 192.168.10.1
```

Teste o servidor:

```text
ping 192.168.60.10
```

Agora faca testes de outros setores:

PC Financeiro:

```text
ping 192.168.20.1
ping 192.168.60.10
```

PC TI:

```text
ping 192.168.30.1
ping 192.168.60.10
```

PC Atendimento:

```text
ping 192.168.40.1
ping 192.168.60.10
```

PC Visitante:

```text
ping 192.168.50.1
ping 192.168.60.10
```

Se responder `Reply from`, funcionou.

Se responder `Request timed out`, tem algo errado em cabo, porta, VLAN, trunk ou interface do roteador.

## 9. Conferir o roteador

No roteador, digite:

```text
show ip interface brief
```

Voce deve ver as interfaces:

```text
g0/0.10
g0/0.20
g0/0.30
g0/0.40
g0/0.50
g0/0.60
```

Tambem digite:

```text
show ip dhcp binding
```

Esse comando mostra quais PCs receberam IP por DHCP.

## 10. Prints para colocar no GitHub

Tire print de:

- Topologia geral
- `show vlan brief`
- `show interfaces trunk`
- PC recebendo IP por DHCP
- Ping funcionando
- Servidor com IP fixo

Salve na pasta:

```text
D:\ProjetosRedes2026\rede-corporativa-packet-tracer\assets
```

