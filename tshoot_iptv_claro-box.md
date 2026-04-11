# TSHOOT — IPTV GPON & IPTV VAS (CLARO BOX)

------------------------------------------------------------------------

## 📋 Visão Geral

Este roteiro cobre o diagnóstico de falhas em serviços de IPTV na plataforma Claro Box, tanto para clientes com tecnologia **IPTV VAS** quanto **IPTV GPON**.

------------------------------------------------------------------------

## 1️⃣ Triagem Inicial — TIME AT

### 1.1 Identificação do Serviço e Conectividade

| # | Verificação | Observação |
|---|---|---|
| 1 | IPTV VAS ou IPTV GPON? | Identificar a plataforma antes de prosseguir |
| 2 | Está conectado à rede GPON Claro? | Confirmar com o cliente |
| 3 | Conectado em outra rede, funciona? | Isola se a falha é da rede Claro |
| 4 | Foi realizado Factory Reset? | Descartar falha de configuração local |

### 1.2 Coleta de Informações do Terminal

Solicitar evidências (print/foto) das seguintes informações:

- **Endereçamento IP:** IP / Máscara / Gateway / DNS
- **Status do Diagnóstico do Servidor:**

| Campo | Valor |
|---|---|
| Vendor | |
| Modelo | |
| Decoder NUID | |
| Decoder CA | |
| Versão Firmware | |
| Versão Atual | |
| Control Plane | |
| Data Plane | |
| ID de Rede | |
| Conexão com Traxis | |
| SDP | |
| VOD | |

### 1.3 Identificação da Falha por Tipo de Canal

- Se tudo OK nas fases anteriores:
  - Quais canais estão falhando? **UNICAST**, **MULTICAST** ou **ambos**?
- Se **IPTV GPON** com falha em canais **Multicast**:
  - É possível testar com VLC na URL RTP do canal?
  - ⚠️ Obs.: O teste deve ser feito na mesma faixa de rede do Set-Top-Box.

> **Se não resolvido:** Escalonar para o Time HE/DTC N1/N2.

------------------------------------------------------------------------

## 2️⃣ Diagnóstico Avançado — TIME HE/DTC N1/N2

### 2.1 Validação da ONU na Plataforma

Verificar o status da ONU nos sistemas: **LDAP / SAC / ACS / EMS (NCE | U31) / OLT**

**Formato de evidência:**
```
<CÓDIGO+CONTRATO> <SERIAL-NUMBER> <MAC> <OLT> <NAP> <LDAP> <SAC> <ACS> <EMS> <OLT>

Exemplo:
994001027358  485754438C5BEE9F  D0C65B301BF1  JIPNBAOLT01  NBA0080304  LDAP OK  SAC OK  ACS OK  NCE OK  OLT OK
```

Verificar também:
- Quais serviços estão habilitados na ONU?
- A ONU possui IPs para as WANs conforme os Service-Port / VPort?
- Se NOK: há descolamento de IPs no DHCP?

------------------------------------------------------------------------

### 2.2 Canais UNICAST

#### 2.2.1 Todos os canais nacionais com falha?
> Se sim, acionar VOC/CAS e verificar:

| Etapa | Ação | Nível |
|---|---|---|
| 1 | Verificar sinal de origem no DCM FEC | N3 |
| 2 | Verificar sinal DCM/vDCM/X2 — Encoders | N3 |
| 3 | Verificar PMx0 — Packager | N3 |
| 4 | Verificar Mídia-Grid | N3 |
| 5 | Verificar com CAS o DRM e Multi-DRM | N3 |
| 6 | Verificar CDN — Service Router / Content Acquire / Streamer | N3 |

#### 2.2.2 Canal local específico com falha?

| Etapa | Ação | Nível |
|---|---|---|
| 1 | Verificar sinal de origem DCM/IRD Operação | HE N1/N2 |
| 2 | Verificar sinal de origem DCM FEC | N3 |
| 3 | Verificar link All IP Contribution | HE N1/N2 |
| 4 | Verificar sinal DCM/vDCM/X2 — Encoders | N3 |
| 5 | Verificar PMx0 — Packager | N3 |
| 6 | Verificar Mídia-Grid | N3 |

------------------------------------------------------------------------

### 2.3 Canais MULTICAST

| Etapa | Verificação |
|---|---|
| 1 | Sinal de origem DCM/IRD (Local e VOC) OK? |
| 2 | Tráfego do canal na OLT OK? (direto na OLT, Nagios e GRB) |
| 3 | Tráfego na IPRAM OK? (GRB — gráfico da subinterface de Multicast: lado IPRAM×OLT e lado IPRAM×RTD_RESIDENCIAL) |
| 4 | Teste com VLC na URL RTP do canal OK? (necessário apoio do time de campo e/ou bases) |
| 5 | NetworkLocation com apontamento para a URL RTP correta? |

------------------------------------------------------------------------

## 📎 Referências

- Metadata de canais por região:
  `http://metadata.dth.virtua.com.br/metadata/delivery/NET/btv/services?filter={"technical.regions":"1994"}&pretty=true`
- Documentação interna DDAY FTTH (SharePoint Claro):
  `https://corpclarobr.sharepoint.com/sites/OT-CyberArk/...`
