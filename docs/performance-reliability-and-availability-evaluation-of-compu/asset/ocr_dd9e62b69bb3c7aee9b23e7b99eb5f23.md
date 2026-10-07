# Performance Measuring

```
12:25:30.200250 IP 192.168.61.128.51282 > 150.161.2.9.80 Flags [],
ack 7193, win 43800, length 0
```

```
12:25:30.200345 IP 192.168.61.128.51282 > 150.161.2.9.80 Flags [],
ack 8653, win 46720, length 0
```

```
12:25:30.200422 IP 192.168.61.128.51282 > 150.161.2.9.80 Flags [],
ack 9969, win 49640, length 0
```

The tcpdump command can generate a dump file in binary format by using the option -w. This option saves the output in a file file-name.pcap, which can be read by tcpdump with the -r option. It is worth noting that one cannot open a file with extension pcap with a text editor unless it is

These basic features will help you get started with tcpdump. For a more detailed description of tcpdump options and filters, look at [426]. It is also important to mention that the analyst may not be restricted to the tcpdump utility. There are many other valuable tools for monitoring and analysis of network traffic such as Wireshark [467], NetworkMiner [303], SolarWinds [405], WinDump [466] and Ngrep [307], for instance.

# Command ping

The ping is used to check the reachability of a host on the Internet. It is commonly used to check if a host is alive and verify if a host-to-connection is performing. For the instance command ping -c5 108.61.13.174 sends five (-c5) packets to the host address 108.61.13.174, we have a typical display of a ping session, which shows five packets of fifty-six bytes sent to the host address 108.61.13.174 and receiving five packets of sixty-four bytes from the host. The round trip time (rtt) of each transaction is shown as well as a short summary. Check ping manual for options and other information

```
PING 108.61.13.174 (108.61.13.174) 56(84) bytes of data.
64 bytes from 108.61.13.174: icmp_seq=1 ttl=128 time=253ms
64 bytes from 108.61.13.174: icmp_seq=2 ttl=128 time=248ms
64 bytes from 108.61.13.174: icmp_seq=3 ttl=128 time=255ms
64 bytes from 108.61.13.174: icmp_seq=4 ttl=128 time=252ms
64 bytes from 108.61.13.174: icmp_seq=5 ttl=128 time=249ms

--- 108.61.13.174 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/mdev = 248.339/252.008/255.728/2.839 ms
```

# Command iperf

The iperf is an open-source networking tool to measure TCP and UDP throughput in a network. Iperf can work in Linux, Windows, and other operating systems. The iperf works in the client-server mode that one computer could

> 16rtt is the delay between a request is from a caller to a responder and the instance of reception time by the caller of the requested information.