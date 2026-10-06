like nmap 10.0.0.51 with no options, the nmap-service file is used to provide the service information, as such:

```
PORT STATE SERVICE
80/tcp open http
139/tcp open netbios-ssn
9100/tcp open jetdirect
9101/tcp open jetdirect
9102/tcp open jetdirect
9110/tcp open unknown
9220/tcp open unknown
9290/tcp open unknown
```

As we said, this is simply a match from the nmap-service file, with no additional checks made. We can certainly edit this file to add or change entries, but this has limited utility as the file is fairly exhaustive.

If we want to get a better idea of what exactly the running services are, we can run nmap -sV 10.0.0.51, which with the version checking turned on, should produce results along the lines of the following:

```
PORT STATE SERVICE VERSION
80/tcp open http Virata-EmWeb 6.0.1 (HP PhotoSmart/Desjet printer http config)
139/tcp open netbios-ssn?
9100/tcp open jetdirect?
9101/tcp open jetdirect?
9102/tcp open jetdirect?
9110/tcp open unknown
9220/tcp open hp-gsq HP Generic Scan Gateway 1.0
9290/tcp open hp-gsq IEEE 1284.4 scant peripheral gateway
```

service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at http://www.insecure.org/cgi-bin/servicefp-submit.cgi :
SF-Port9110-TCP:V=5.51%D=4/20%4Time=4DD72E40P=x\x86_64-unknown-linux-gnu

```
SF:%&r(RPCCck,2B,"\0)
(r\xfe\xid\x13\x01\x00\x01\x00\x00\x02\x00\x01\x86\x80\x0
SF:\x01\x91\x97\x00\x00\x00\x00\x00\x00\x00\x00
```

We can see here that we got back a bit more detailed information on several of the ports, although not everything was successful. This information is pulled from the entries in the nmap-