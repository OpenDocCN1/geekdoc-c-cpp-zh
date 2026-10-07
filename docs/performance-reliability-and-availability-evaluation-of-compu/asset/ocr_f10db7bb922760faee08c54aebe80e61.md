# Performance Measuring

The main difference is the source and destination hostnames are replaced by the IP addresses and ports. Thus, the second field shows the source host address and port, followed by the destination host address and port, 192.168.61.128 > 200.186.195.123.

The number of packets to be ready may also be specified by using the option -c, such as `sudo tcpdump - any -c 10`, where the number after -c denotes the number of packets to capture. In the command, the tcpdump finishing the process as soon as it gets ten (10) packets. Below, a chunk of information collected is presented as an example.

```
tcpdump: verbose output, -v or -vv for full protocol listening on any, link-type LINUX_XX (Linux connected), capture size 262144 bytes
21:53.47.023515 192.168... ...
```

```
21:53.47.17619 192.168.61.128.17500 > 54.225.82.232.123: 192.168.61.128.123: IPv4, Client,
```

```
21:53.47.98319 192.168.61.128.17500 > 255.255.255.17500: UDF, length 242
```

```
21:53.47.96808 192.168.61.128.17500 < 255.255.255.17500: UDF, length 242
```

```
21:53.47.98629 192.168.61.128.17500 > 255.255.255.17500: UDF, length 242
```

```
21:53.47.98738 192.168.61.128.17500 > 192.168.61.128.130:130: UDP, length 242
```

```
21:53.47.96118 192.168.61.128.17500 < 255.255.255.17500: UDP, length 242
```

```
21:53.51.02394 192.168.61.128.123 > 192.36.143.130.123: IPv4, Client,
```

+   10 packets
10 packets received by filter
0 dropped by kernel

The option -X prints the data of each packet in hexadecimal and ASCII, besides the headers of each packet. For instance, consider the command line `sudo tcpdump - any -c 3`. This command switches for all interfaces, the source and destination addresses with the respective ports, and the content of each packet in hexadecimal and ASCII formats (option -A presents the content in ASCII only). This is useful when the administrator wants to analyze the content of the packets. Typical output looks like:

```
tcpdump: verbose output, -v or -vv for full protocol listening on any, link-type LINUX_XX (Linux connected), capture size 262144 bytes
16:37:23.034421 192.168.61.128.123 > 164.146.48.5: IPv4, Client,
```

```
0000 4b8b 000c 5e25 4000 401f a1fa c0a9 3d80 E..L%8...
0010 925a 30d5 0070 003b 0078 1fbc 2302 08e6 ....0.(I..#..
0020 0000 265d 0000 08c1 05f5 f2c1 02b6 10f5 ...f........
0030 6619 98d2 e8c6 10b4 f57da 22c1 02b6 10f5 ...f........
0040 f000 f000 f000 f000 f000 f000 f000 f0000 .........
```

```
16:37:23.168734 164.146.48.5 > 192.168.61.128.123: IPv4, Server,
```

```
0000 4500 02c6 2000 8011 a8ae 92a4 0305 ....E..L.......O,
```

```
0010 0c1a 38d0 0077 003b 00e4 0241 0060 ....W.(I..S..
```

```
0020 0000 0000 0012 4750 5300 02e6 10ef 00ec ....GPS.1....
```

```
0030 241f 7404 02e6 10f3 08e7 00d4 02e6 10f2 ..S.t......1...
```

```
0040 e5f3 dd38 e2c 02e6 10f2 e5fd 4eaf ....f...3...1......
```

16:37:24.034421 192.168.61.128.123 > 45.110.195.253.123: IPv4, Client,