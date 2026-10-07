# 400 Performance, Reliability, and Availability Evaluation of Computational Systems

```
00010: 45b8 004c e770 4011 bd47 c0a8 3d80  E..L.p.@..G=.
00020: 2dbb6 69fd 007a 007b 08d7 23d3 062e 10ea  -...(.{B..#...
00030: 6618 9c88 e2c6 10b5 6f56 03e8 e2c6 10b6  f....H....M....
00040: 308d da51 e2c6 10f4 08f6 99fc          O..Q....
3 packets captured
3 packets dropped by kernel
```

For instance, the data shown above, after the header of the first packet,

```
16:37:23.034792 192.168.61.128.123 > 146.164.48.53.123: NTPv4, Client, length 48,
```

we get the packet's content:

```
00000: 45b8 004c 5e25 4001 1af2 c03a8 3d80  E..L%@..G=.
00010: 92a4 30b5 007b 0079 01fbc 2302 062e 06e8  ...(.{B..#...
00020: 0000 265d 0001 48c0 037a e2c6 10ea  ...H....M....
00030: 6618 9c88 e2c6 10b5 6f56 bdc1 e2c6 10b5  f....H....M....
00040: 22cc 44f0 e2c6 10f3 01f3 08e2 00da  ........
```

The command tcpdump is capable of monitoring many different protocols, such as IP, TCP, UDP, ICMP, and other. The aim here is not to support the reader getting started. Details and formats of different protocols may be found in tcpdump's manual. Assume the TCP packet captured by tcpdump below:

```
16:14:06.396782 192.168.61.128.50394 > 192.168.61.128.50394: Flags [.], seq 2921:4381, ack 430,
```

```
win 64240, length 1460: HTTP
```

The header's content may vary depending on the type of packet. However, the TCP packet header has its first field,

```
17:14:06.396782,
```

that represents the timestamp of the received or sent packet. The field IP denotes the network layer protocol in (IP for IPv4 and IP6 for IPv6 packets). In this particular case, we have IP. The next field is

```
150.161.2.99.80,
```

which is the source IP and port (80). Port 80 is adopted for HTTP traffic. The next field is the destination IP address and port

```
192.168.61.128.50394,
```