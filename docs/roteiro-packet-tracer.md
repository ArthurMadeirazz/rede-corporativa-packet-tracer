 # Roteiro para montar no Packet Tracer

Esse roteiro serve para montar o projeto dentro do Cisco Packet Tracer. A rede usa VLANs no switch e subinterfaces no roteador.

## 1. Criar a topologia

Adicione os equipamentos:

- 1 roteador
- 2 switches
- 1 servidor
- 2 PCs para Administracao
- 2 PCs para Financeiro
- 2 PCs para TI / Suporte
- 2 PCs para Atendimento
- 1 ou 2 dispositivos para Visitantes

## 2. Conectar os equipamentos

Conecte:

- Roteador ao switch principal pela porta `g0/0` do roteador e `fa0/1` do switch
- Switch principal ao segundo switch
- PCs aos switches
- Servidor ao switch principal

Use cabos automaticos ou cabo cobre direto, dependendo do equipamento.

## 3. Configurar as VLANs

No switch, crie as VLANs dos setores:

```text
10 - Administracao
20 - Financeiro
30 - TI
40 - Atendimento
50 - Visitantes
60 - Servidores
```

Depois configure:

- Porta do roteador como trunk
- Portas dos computadores como access
- Porta entre switches como trunk

Os comandos base estao no arquivo:

```text
docs/configuracao-cisco.md
```

## 4. Configurar os IPs

Use o plano de enderecamento do arquivo:

```text
docs/plano-de-enderecamento.md
```

O servidor deve usar IP fixo:

```text
IP: 192.168.60.10
Mascara: 255.255.255.0
Gateway: 192.168.60.1
```

## 5. Configurar DHCP

Crie pools DHCP para os setores:

- Administracao
- Financeiro
- TI / Suporte
- Atendimento
- Visitantes

Cada pool deve entregar:

- IP automatico
- Mascara
- Gateway
- DNS, se for configurado

## 6. Testar a rede

Em cada computador:

1. Abra a area de configuracao de IP.
2. Marque DHCP.
3. Confirme se recebeu um IP da faixa correta.
4. Abra o terminal.
5. Teste ping para o gateway.
6. Teste ping para o servidor.

Exemplo:

```text
ping 192.168.10.1
ping 192.168.60.10
```

## 7. Tirar prints

Tire prints de:

- Topologia geral
- VLANs criadas no switch
- Configuracao de DHCP
- Computador recebendo IP automaticamente
- Teste de ping funcionando
- Servidor configurado com IP fixo

Salve as imagens na pasta:

```text
assets/
```
