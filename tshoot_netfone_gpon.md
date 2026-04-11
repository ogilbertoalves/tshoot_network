# TSHOOT — NETFONE GPON

------------------------------------------------------------------------

## 📋 Visão Geral

Roteiro de diagnóstico para falhas no serviço de **NetFone GPON** (VoIP via ONU), cobrindo desde validação de perfil e conectividade com o ACS até o registro SIP do terminal.

------------------------------------------------------------------------

## 1️⃣ Validação de Perfil nos Sistemas

Verificar se o perfil do cliente está correto em todos os sistemas:

| Sistema | Status |
|---|---|
| NETSMS | OK / NOK |
| LDAP | OK / NOK |
| SAC | OK / NOK |
| ACS | OK / NOK |

------------------------------------------------------------------------

## 2️⃣ Comunicação ONU ↔ ACS (TR-069)

Verificar se a OLT está se comunicando corretamente com o ACS:

| Parâmetro | Valor |
|---|---|
| Link ACS TR-069 | `http://tr069.sdm.virtua.com.br:7547/service/cwm` |
| Porta ACS TR-069 | `7547` |
| Endereço IPv6 ACS | `2804:14d:fe00:0:201:6:22:84` |

**Comandos de validação:**
```sh
# Testar alcance IPv6 ao ACS
ping ipv6 2804:14d:fe00:0:201:6:22:84

# Traçar rota IPv6 ao ACS
tracert ipv6 2804:14d:fe00:0:201:6:22:84

# Testar porta TR-069
telnet ipv6 2804:14d:fe00:0:201:6:22:84 7547
```

------------------------------------------------------------------------

## 3️⃣ Verificação de IP na WAN de MTA

### 3.1 Localizar Frame/Slot/Port e ONT-ID

```sh
display ont info by-sn <SN> | include F/S/P|ONT-ID
```

### 3.2 Verificar IP na WAN (ONUs Huawei)

```sh
display ont wan-info <F/S> <P> <ONT-ID> | include Index|Name|IPv4 address
```

### 3.3 Verificar IP na WAN (outros vendors — via Service Port)

```sh
display current-configuration | include <F/S/P> ont <ONT-ID>
display current-configuration ont <F/S/P> <ONT-ID>
diagnose
display udm user service-port <Service Port Number>
quit
```

> ⚠️ **Nota:** ONUs ZTE não respondem a ping para a WAN de NetFone — comportamento esperado.

------------------------------------------------------------------------

## 4️⃣ Alcançabilidade do IP de MTA

| Teste | Origem | Resultado esperado |
|---|---|---|
| Ping ao IP de MTA | A partir da OLT | Resposta (exceto ZTE) |
| Ping ao IP de MTA | A partir dos RTDs com link de NetFone | Resposta |

Se o ping dos RTDs falhar, verificar:
- RTDs estão recebendo as redes de NetFone via **iBGP IPRAN**?
- **ACL** correta?
- **RP** correta?

------------------------------------------------------------------------

## 5️⃣ Validação de DNS e Registro SIP

Verificar se a ONU está consultando os **DNSs Autoritativos da cidade matriz** e recebendo o IP dos Call Agents:

```sh
snoop -r port 53 | grep <IP_MTA_ONT>
```

> Os DNSs Autoritativos devem responder às queries de Call Agents.

------------------------------------------------------------------------

## 6️⃣ Ações de Recuperação

Se todas as etapas anteriores estiverem OK e o NetFone ainda não estiver registrado:

1. **Reboot** da ONU
2. **Reset de fábrica** da ONU

Se mesmo assim não registrar:
- Escalar incidente para o **N3** validar ACS
- e/ou acionar o time de **TI** para validar as credenciais SIP

------------------------------------------------------------------------

## 7️⃣ Referências e Recomendações do N3

| Status do Terminal | Ação Recomendada |
|---|---|
| `sync_failed` | Realizar reset de fábrica |
| `not_sync` por mais de 5 min | Enviar ao time N3 para análise (status transitório, não deve persistir) |
| `N/D` | Validar comunicação do terminal ou da cidade inteira com o ACS; se não encontrado, abrir ticket para suporte |
| `sync` | Executar tshoot de fone: ping do IP do terminal a partir de um router de borda HFC, verificar DNS (queries de Call Agent), LDAP e objetos no ACS |
