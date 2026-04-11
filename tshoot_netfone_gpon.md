### TSHOOT NETFONE GPON #####
>> Profile OK (NETSMS, LDAP, SAC, ACS)?
 
>> Comunicação da OLT com o ACS está OK?
Link ACS TR69: http://tr069.sdm.virtua.com.br:7547/service/cwm
Porta ACS TR69: 7547
tracert ipv6 2804:14d:fe00:0:201:6:22:84
ping ipv6 2804:14d:fe00:0:201:6:22:84
telnet ipv6 2804:14d:fe00:0:201:6:22:84 7547
 
>> ONT pegou IP na WAN de MTA?
### Filtrar Frame/Slot/Port e ONT-ID
display ont info by-sn <SN> | include F/S/P|ONT-ID
 
### Filtrar Index, Name e IPv4 Address (Suporte somente para ONTs HUAWEI)
display ont wan-info <F/S> <P> <ONT-ID> | include Index|Name|IPv4 address
 
### Filtrar IP Address em ONTs de outro Vendor (by Service Port)
display current-configuration | include <F/S/P> ont <ONT-ID>
display current-configuration ont <F/S/P> <ONT-ID>
diagnose
display udm user service-port <Service Port Number>
quit
 
>> IP de MTA da ONT responde a ping a partir da OLT?
>>> Obs.: Notado que as ONUs da ZTE não respondem a ping para a WAN de NETFONE;
 
>> IP de MTA da ONT responde a ping a partir dos RTDs que tem link de NetFone?
>>> Se não, RTDs estão recebendo as redes de NETFONE via iBGP IPRAN?
>>> ACL correta? RP correta?
 
>> ONT está enviando requisições de dns para os DNSs Autoritativos da cidade matriz? Se sim, DNSs respondem com o ip dos callagents?
snoop -r port 53 | grep <IP_MTA_ONT>
>>> DNSs Autoritativos devem responder às queries de callagents;
 
>> Se tudo OK e Netfone ainda não registrado, realizar reboot e/ou reset de fábrica;
 
>> Se ainda assim não registrar, escalar incidente para o N3 validar ACS e/ou time de TI para validar credenciais SIP;
 
>> Recomendações do N3:
>>> Terminais em sync_failed precisam de um reset de fábrica;
>>> Terminais em not_sync por mais de 5 min deve ser enviado ao meu time para analise, este é um tatus transitório não deve estar neste status;
>>> Terminais em N/D deve ser validado se o terminal ou cidade inteira tem comunicação com o ACS. DC local analise e se não encontrar a falha abre ticket para suporte;
>>> Terminais em sync deve ser feito o tshoot de fone, ping IP Fone do terminal de um router de borda de uma cidade HFC e olhar se o DNS recebe as query de callagent, se LDAP esta ok, se ACS tem os objetos corretos;
