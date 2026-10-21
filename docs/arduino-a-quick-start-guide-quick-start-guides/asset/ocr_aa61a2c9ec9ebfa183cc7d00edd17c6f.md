First, we include the Ethernet library and define a constant for the DAYTIME service port (we also have to include the SPI library, because the Ethernet library depends on it). Then we define three byte arrays:

+   - mac contains the MAC address we are going to use for the Ethernet shield. A MAC address is a 48-bit number that uniquely identifies a network device.¹¹ Usually, the manufacturer sets this identifier, but for the Ethernet shield, we have to set it ourselves; we use an arbitrary number.

Important note: the MAC address has to be unique on your network. If you connect more than one Arduino, make sure they all have different MAC addresses!

+   - Whenever you connect your PC to the Internet, it probably gets a new IP address via the Dynamic Host Configuration Protocol (DHCP).¹² For most Arduino applications, a DHCP implementation is comparatively costly, so you usually assign an IP address manually. In most cases, this will be a local address in the 192.168.x.y range; we store this address in the my_ip array.

+   - To turn domain names such as time.nist.gov into an IP address, you need access to the Domain Name System (DNS). The Arduino’s standard library doesn’t support DNS, so we have to find out the IP address ourselves. We assign it to time_server. The telnet command already turned the DAYTIME service domain name into an IP address for us. Alternatively, you can use one of the following commands to determine a domain name’s IP address:

```
maik> host time.nist.gov
time.nist.gov has address 192.43.244.18
maik> dig +short time.nist.gov
192.43.244.18
maik> resolveip time.nist.gov
IP address of time.nist.gov is 192.43.244.18
maik> ping -c 1 time.nist.gov
PING time.nist.gov (192.43.244.18): 56 data bytes
64 bytes from 192.43.244.18: icmp_seq=0 ttl=48 time=173.598 ms

--- time.nist.gov ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 173.598/173.598/173.598/0.000 ms
```

11. http://en.wikipedia.org/wiki/Mac_address
12. http://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol

![](bbox=[0.78, 0.27, 0.85, 0.34])