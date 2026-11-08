# # Chapter 17

IOS requires that you configure parameters for the three highlighted parts of Figure 17-2. For the protocol type, you simply use a keyword, such as tcp, udp, or icmp, matching IP packets that happen to have a TCP, UDP, or ICMP header, respectively, following the IP header. Or you can use the keyword ip, which means “all IPv4 packets.” You also must configure some values for the source and destination IP address fields that follow; these fields use the same syntax and options for matching the IP addresses as discussed in Chapter 16, “Basic IPv4 Access Control Lists.” Figure 17-3 shows the syntax.

![](bbox=[0.135, 0.258, 0.735, 0.497])

**Figure 17-3** *Extended ACL Syntax, with Required Fields*