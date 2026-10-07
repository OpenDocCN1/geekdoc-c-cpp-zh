# Performance Measuring

| State Recv-Q | Local Address:Port | Peer Address:Port |
|---|---|---||
| ESTAB 0 | 0 | 192.168.61.128:47406 | 54.213.219.163<br>time:(keepalive,4min2sec,0)<br>uid:1000 ino:662872: sk46 <-> |
| ESTAB 0 | 0 | 192.168.61.128:36464 | 216.58.222.106:443<br>uid:1000 ino:63068: sk4f <-> |
| ESTAB 0 | 0 | 192.168.61.128:47230 | 64.23.190.183<br>uid:1000 ino:628765: sk4a <-> |
| ESTAB 0 | 0 | 192.168.61.128:49990 | 216.58.202.238:443<br>uid:1000 ino:625069: sk5f <-> |
| ESTAB 0 | 0 | 192.168.61.128:59188 | 172.17.219.183<br>uid:1000 ino:629634: sk41 <-> |
| ESTAB 0 | 0 | 192.168.61.128:55262 | 216.58.222.69<br>uid:1000 ino:633562: sk472 <-> |

# Command tcpdump

The `tcpdump` is a powerful command-line tool for network traffic monitoring (sniffing and analysis) [426]. The `tcpdump` command is used to create "dumps" or "traces" of network traffic can also be launched in the background or by other tools. Monitoring network traffic through `tcpdump` requires high permission levels, so most commands are prefixed with `sudo` command.

As already mentioned at the beginning of this section, our aim is not to reference network working tools but rather introduce few simple and examples and point out a specific reference on the subject. The `tcpdump` has many options (parameters) that allow configuring and filtering specific types of network traffic. This section discusses the most basic options that can be used as well as some useful examples of `tcpdump` for sniffing and analyzing network traffic.

Hence let us start the command `tcpdump -D` to find out interfaces are available in the system. As a result, information as depicted below is provided, which shows all the interfaces available. The particular interface allows capturing in any active interface.

```
1.ens33-device [Up, Running]
2.any (Pseudo-device that captures on all interfaces) [Up, Running]
3.lo [Up, Running, Loopback]
4.bluetooth0 (Bluetooth adapter number 0)
5.nfilterlog (Linux netfilter log (NLOG) interface)
6.nfqueue (Linux netfilter queue (QUEUE) interface)
7.usb1 (USB bus number 1)
8.usb0 (USB bus number 2)
```

A specific interface can be sniffed using the -i option, followed by the interface name. The command `sudo tcpdump -i ens33` captures packets in interface ens33 until an interrupt signal is sent, which occurs by pressing Ctrl+C. Below, a chunk of data packets is depicted as example.

```
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on ens33, link-type EN10MB (Ethernet), capture size 262144 bytes
```