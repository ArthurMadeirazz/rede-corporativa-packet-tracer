# Plano de Enderecamento

Este documento organiza as redes usadas no projeto.

## Redes por setor

| Setor | Rede | Mascara | Gateway | Observacao |
| --- | --- | --- | --- | --- |
| Administracao | 192.168.10.0 | 255.255.255.0 | 192.168.10.1 | PCs administrativos |
| Financeiro | 192.168.20.0 | 255.255.255.0 | 192.168.20.1 | PCs do financeiro |
| TI / Suporte | 192.168.30.0 | 255.255.255.0 | 192.168.30.1 | Maquinas de suporte |
| Atendimento | 192.168.40.0 | 255.255.255.0 | 192.168.40.1 | Maquinas de atendimento |
| Visitantes | 192.168.50.0 | 255.255.255.0 | 192.168.50.1 | Dispositivos de visitantes |
| Servidor | 192.168.60.0 | 255.255.255.0 | 192.168.60.1 | Servidor interno |

## IPs fixos

| Equipamento | IP | Observacao |
| --- | --- | --- |
| Roteador - Administracao | 192.168.10.1 | Gateway do setor |
| Roteador - Financeiro | 192.168.20.1 | Gateway do setor |
| Roteador - TI / Suporte | 192.168.30.1 | Gateway do setor |
| Roteador - Atendimento | 192.168.40.1 | Gateway do setor |
| Roteador - Visitantes | 192.168.50.1 | Gateway do setor |
| Roteador - Servidor | 192.168.60.1 | Gateway da rede de servidor |
| Servidor Interno | 192.168.60.10 | IP fixo |

## Faixas DHCP sugeridas

| Setor | Inicio | Fim |
| --- | --- | --- |
| Administracao | 192.168.10.10 | 192.168.10.100 |
| Financeiro | 192.168.20.10 | 192.168.20.100 |
| TI / Suporte | 192.168.30.10 | 192.168.30.100 |
| Atendimento | 192.168.40.10 | 192.168.40.100 |
| Visitantes | 192.168.50.10 | 192.168.50.100 |

