# Testes da Rede

Este arquivo registra os testes feitos no projeto.

## Testes de DHCP

| Equipamento | Resultado |
| --- | --- |
| PC Administracao 1 | Sucesso |
| PC Financeiro 1 | Sucesso |
| PC TI 1 | Sucesso |
| PC Atendimento 1 | Sucesso |
| PC Visitante 1 | Sucesso |

## Testes de VLAN

| Teste | Comando | Resultado |
| --- | --- | --- |
| Listar VLANs no switch | `show vlan brief` | Sucesso |
| Conferir trunk do switch | `show interfaces trunk` | Sucesso |
| Conferir subinterfaces do roteador | `show ip interface brief` | Sucesso |

## Testes de conectividade

| Origem | Destino | Comando | Resultado |
| --- | --- | --- | --- |
| PC Administracao 1 | Gateway Administracao | `ping 192.168.10.1` | Sucesso |
| PC Financeiro 1 | Gateway Financeiro | `ping 192.168.20.1` | Sucesso |
| PC TI 1 | Gateway TI | `ping 192.168.30.1` | Sucesso |
| PC Atendimento 1 | Gateway Atendimento | `ping 192.168.40.1` | Sucesso |
| PC TI 1 | Servidor Interno | `ping 192.168.60.10` | Sucesso |

## Observacoes

Os testes principais foram concluidos no Packet Tracer. Os PCs receberam IP por DHCP, as VLANs apareceram no switch e o roteador mostrou as subinterfaces ativas.
