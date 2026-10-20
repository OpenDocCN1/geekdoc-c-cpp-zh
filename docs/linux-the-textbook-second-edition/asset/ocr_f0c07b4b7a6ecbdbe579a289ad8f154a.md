![](bbox=[0.18, 0.06, 0.82, 0.34])

You can use the ifconfig command to view and set network interface parameters, including the IP address, localhost, netmask, broadcast address, and maximum transmission unit (MTU). However, this command is not maintained anymore and has been replaced with more contemporary ip command in most modern Linux systems. It can be used for doing post-install network configuration of network interface parameters as well see their current settings. You can do with the ip command all that you can do with the ifconfig command and more. In this section, we show few sample runs of the ip command for checking and setting network interface parameters in Chapter 17, Section 8.2.

Netmask, also known as subnetmask, is a bit mask used by TCP/IP to identify whether a host is on a remote network or on a local subnet. A broadcast address is used by the IP layer in a host to send a datagram to all the hosts on a subnet or to a remote network. The Ethernet broadcast address is all 1s. The MTU in a TCP/IP network is the maximum size of an IP datagram (packet) and is dependent on the technology used at the data link layer for connection to other hosts.

The following is an example run of ip on our Linux Mint machine. The output of the ip addr show (or ip a s) command shows that you are logged on to a host that has localhost interface and network interfaces enp2s0 and eno1, each having IPv4 and IPv6 addresses. For IPv4, localhost is 127.0.0.1, with MTU 65,536 bytes. For IPv6, localhost is ::1/128. The IPv4 network addresses are 202.147.169.195 and 172.16.0.101; each with MTU 1,500 bytes, and broadcast addresses 202.147.169.223 and 172.16.255.255, respectively. Further, the IP address 202.147.169.195 is associated with MAC address 00:10:18:30:ee:6e. For IPv6, network IP addresses for external traffic are fe80::67ab:4f1a:21fa:f0f5 and fe80::e352:b2f4:9833:cebd, respectively, for enp2s0 and eno1.

```
$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
2: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
link/ether 00:10:18:30:ee:6e brd ff:ff:ff:ff:ff:ff
inet 202.147.169.195/27 brd 202.147.169.223 scope global enp2s0
valid_lft forever preferred_lft forever
inet6 fe80::67ab:4f1a:21fa:f0f5/64 scope link
valid_lft forever preferred_lft forever
3: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
link/ether 00:10:18:30:ee:6e brd ff:ff:ff:ff:ff:ff
inet 172.16.0.101/24 brd 172.16.255.255 scope global eno1
valid_lft forever preferred_lft forever
inet6 fe80::e352:b2f4:9833:cebd/64 scope link
valid_lft forever preferred_lft forever
```