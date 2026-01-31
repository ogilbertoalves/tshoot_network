# Troubleshooting Básico & Intermediário (v3 -- Completo com Todas as Referências)

------------------------------------------------------------------------

# 1️⃣ Básico

## 🔹 Ping

``` sh
ping www.google.com.br
ping -t www.google.com.br
ping -6 www.google.com.br
ping -6 -t www.google.com.br
```

Referência:\
https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/ping

------------------------------------------------------------------------

## 🔹 Tracert

``` sh
tracert www.google.com.br
tracert -h 5 www.google.com.br
tracert -4 -h 5 www.google.com.br
```

Referência:\
https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/tracert

------------------------------------------------------------------------

## 🔹 Nslookup

``` sh
nslookup www.google.com.br <IP_DNS1>
nslookup www.google.com.br <IP_DNS2>
nslookup -type=AAAA www.google.com.br
```

Referência:\
https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/nslookup

------------------------------------------------------------------------

# 2️⃣ Portais

## 🔹 IPv4 e IPv6 Check

-   https://ipv6.br/
-   https://test-ipv6.com
-   https://test-ipv6.csclub.uwaterloo.ca/index.html.pt_BR

------------------------------------------------------------------------

## 🔹 Looking Glass

-   https://lg.he.net/
-   https://lg.nocclaro.com.br/
-   https://lg-hg.nocclaro.com.br/

------------------------------------------------------------------------

## 🔹 PortScanner

-   https://portforward.com/software/download-instructions/network-utilities/
-   http://ports.my-addr.com/check-all-open-ports-online.php

------------------------------------------------------------------------

# 3️⃣ Intermediário

## 🔹 Comandos

-   traceroute

-   tracepath

-   tcping\
    Referência:
    https://neoctobers.readthedocs.io/en/latest/linux/tcpping_on_ubuntu.html

-   route print

-   dig

-   nc & netcat

-   nmap

-   curl

    ``` sh
    curl https://bb.com.br --verbose
    ```

    Referência: https://curl.se/docs/manpage.html

-   mtr

    ``` sh
    sh -c 'mtr -n -z --report-cycles 10 --report 52.20.78.240'
    ```

    Referência: https://linuxcommandlibrary.com/man/mtr

-   LookingGlass

------------------------------------------------------------------------

# 4️⃣ PowerShell

(Seção reservada)

------------------------------------------------------------------------

# 5️⃣ WireShark

Site oficial:\
https://www.wireshark.org/

------------------------------------------------------------------------

# 6️⃣ WSL Linux

### Instalar WSL

https://learn.microsoft.com/pt-br/windows/wsl/install

------------------------------------------------------------------------

# 7️⃣ NETSH

## 🔹 Checar Interfaces

``` sh
netsh interface ipv4 show subinterfaces
```

Referência:\
https://learn.microsoft.com/en-us/powershell/module/netadapter/get-netadapter?view=windowsserver2022-ps

------------------------------------------------------------------------

## 🔹 Manipular MTU

``` sh
netsh interface ipv4 set subinterface "vEthernet (WSL)" mtu=1490 store=persistent
```

Referência:\
https://www.bemmelhor.com.br/info/index.php?title=Configurando_MTU_no_Windows

------------------------------------------------------------------------

# 8️⃣ CURL

``` sh
curl https://bb.com.br --verbose
curl https://iw.claro.com.br --verbose
```

Referência:\
https://curl.se/docs/manpage.html

------------------------------------------------------------------------

# 9️⃣ PortScanner e Vulnerability Scanner

-   https://portforward.com/software/download-instructions/network-utilities/
-   http://ports.my-addr.com/check-all-open-ports-online.php
-   https://www.nperf.com/pt/
-   https://nmap.org/
-   https://www.datamation.com/security/how-to-easily-run-a-vulnerability-scan-using-nmap/
-   https://securitytrails.com/blog/nmap-vulnerability-scan
-   http://ports.my-addr.com/check-all-open-ports-online.php
-   https://medium.com/@nallamuthu/powershell-port-scan-bf27fc754585
-   https://medium.com/@Aircon/nmap-advanced-port-scans-tryhackme-thm-ed3859a33eca

------------------------------------------------------------------------

# 🔟 Wi-Fi Analyzer

## Windows

-   Windows Insider

## Android

-   https://fidanov.net/landroid/
-   https://play.google.com/store/apps/details?id=net.fidanov.landroid

------------------------------------------------------------------------

# 1️⃣1️⃣ Advanced Tools -- BGP

BGP IPv4/IPv6 Looking Glass Servers\
BGP Route Servers\
Border Gateway Protocol / Advanced Internet Routing

## 🔹 ASN / Prefix Analysis

-   https://stat.ripe.net/app/launchpad
-   https://bgp.he.net/AS28573

------------------------------------------------------------------------

## 🔹 Lista Global de Looking Glass

-   https://www.bgp4.as/looking-glasses
-   https://lg.maxiweb.com.br/cgi-local/lg.cgi
-   https://lg.he.net/
-   https://lg.bsa.g8.net.br/
-   https://lg.nocclaro.com.br/
-   http://looking-glass.eletronet.com/

------------------------------------------------------------------------

## 🔹 Referências Técnicas BGP

-   https://news.lacnic.net/pt-br/roteamento/ferramentas-fundamentais-para-uma-boa-gestao-de-redes
-   https://semanacap.bcp.nic.br/files/apresentacao/arquivo/1208/Ferramentas%20monitoramento%20(5).pdf
-   https://wiki.brasilpeeringforum.org/w/Solucoes_para_o\_gerenciamento_efetivo_do_bgp_em_um_sistema_autonomo
