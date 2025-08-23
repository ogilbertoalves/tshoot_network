# Troubleshooting Básico & Intermediário

## Básico

### Ping
Exibir a ajuda do comando:
```sh
ping www.google.com.br
ping -t www.google.com.br

ping -6 www.google.com.br
ping -6 -t www.google.com.br
```
Referência: [Microsoft Docs - ping](https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/ping)

### Tracert
Exibir a ajuda do comando:
```sh
tracert www.google.com.br
tracert -h 5 www.google.com.br (Máximo de 5 saltos) *Prioriza saída IPv6
tracert -4 -h 5 www.google.com.br (Forçando saída IPv4 com máximo de 5 saltos)
```
Referência: [Microsoft Docs - tracert](https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/tracert)

### Nslookup
Exibir a ajuda do comando:
```sh
nslookup www.google.com.br <IP_DNS1>
nslookup www.google.com.br <IP_DNS2>

nslookup -type=AAAA www.google.com.br (Forçar consulta em IPv6)
```
Referência: [Nslookup](https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/nslookup)

### Portais
#### IPv4 e IPv6 Check
- [https://test-ipv6.com](https://test-ipv6.com)
- [https://test-ipv6.csclub.uwaterloo.ca/index.html.pt_BR](https://test-ipv6.csclub.uwaterloo.ca/index.html.pt_BR)

#### LookingGlass
[https://lg.he.net/](https://lg.he.net/)

#### PortScanner
- [PortForward - Network Utilities](https://portforward.com/software/download-instructions/network-utilities/)
- [Check All Open Ports Online](http://ports.my-addr.com/check-all-open-ports-online.php)


## Intermediário
- `traceroute`
- `tracepath`
- `tcping` ([Referência](https://neoctobers.readthedocs.io/en/latest/linux/tcpping_on_ubuntu.html))
- `route print`
- `dig`
- `nc` & `netcat`
- `nmap`
- `curl`
  ```sh
  curl https://bb.com.br --verbose
  ```
  [Referência](https://curl.se/docs/manpage.html)
- `mtr`
  ```sh
  sh -c 'mtr -n -z --report-cycles 10 --report 52.20.78.240'
  ```
  [Referência](https://linuxcommandlibrary.com/man/mtr)
- `LookingGlass`

## PowerShell

## WireShark

## WSL Linux
### Instalar WSL
[Guia de Instalação](https://learn.microsoft.com/pt-br/windows/wsl/install)

### Checar Interfaces
```sh
netsh interface ipv4 show subinterfaces
```
[Referência](https://learn.microsoft.com/en-us/powershell/module/netadapter/get-netadapter?view=windowsserver2022-ps)

### Manipular o MTU
```sh
netsh interface ipv4 set subinterface "vEthernet (WSL)" mtu=1490 store=persistent
```
[Referência](https://www.bemmelhor.com.br/info/index.php?title=Configurando_MTU_no_Windows)

### Testar Sites
```sh
curl https://bb.com.br --verbose
curl https://iw.claro.com.br --verbose
```

## PortScanner
- [PortForward - Network Utilities](https://portforward.com/software/download-instructions/network-utilities/)
- [Check All Open Ports Online](http://ports.my-addr.com/check-all-open-ports-online.php)
- [nPerf - Network Testing](https://www.nperf.com/pt/)

### Tools Port and Vulnerability Scanner
- [Nmap](https://nmap.org/)
- [How to Run a Vulnerability Scan Using Nmap](https://www.datamation.com/security/how-to-easily-run-a-vulnerability-scan-using-nmap/#:~:text=Nmap%20(network%20mapper)%20can%20be,experts%20perform%20scans%20for%20safety.)
- [Nmap Vulnerability Scan](https://securitytrails.com/blog/nmap-vulnerability-scan)
- [Check All Open Ports Online](http://ports.my-addr.com/check-all-open-ports-online.php)
- [PowerShell Port Scan](https://medium.com/@nallamuthu/powershell-port-scan-bf27fc754585)
- [Nmap Advanced Port Scans - TryHackMe](https://medium.com/@Aircon/nmap-advanced-port-scans-tryhackme-thm-ed3859a33eca)

## Wi-Fi Analyzer
### Windows
- Windows - Insider

### Android
