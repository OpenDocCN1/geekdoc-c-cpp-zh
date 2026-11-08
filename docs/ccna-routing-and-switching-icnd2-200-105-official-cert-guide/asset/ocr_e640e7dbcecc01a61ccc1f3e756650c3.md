The next step in the process is to test sending IPv6 traffic through the ACL. Using a simple ping6 command from host A to host B will validate that the packets are being allowed. Example 25-4 shows the output from host A successfully executing the ping6 command.

# **Example 25-4** _Validating ping Command’s Packets Are Permitted by the ACL_

```
cisco@HostA:~$ ping 2001:db8:1111:2:f816:3eff:fe9a:c89f
PING 2001:db8:1111:2:f816:3eff:fe9a:c89f (2001:db8:1111:2:f816:3eff:fe9a:c89f) 56 data
 bytes
64 bytes from 2001:db8:1111:2:f816:3eff:fe9a:c89f: icmp_seq=1 ttl=62 time=8.63 ms
64 bytes from 2001:db8:1111:2:f816:3eff:fe9a:c89f: icmp_seq=2 ttl=62 time=8.71 ms
64 bytes from 2001:db8:1111:2:f816:3eff:fe9a:c89f: icmp_seq=3 ttl=62 time=6.25 ms
^C

--- 2001:db8:1111:2:f816:3eff:fe9a:c89f ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 6.257/7.869/8.712/1.142 ms
cisco@HostA:~$
```

Three ICMPv6 Echo Request messages were sent and it appears that they were successfully received and three ICMPv6 Echo Reply messages were returned. The next step is to check the IPv6 ACL on R1 and see how many packets have matched its single permit ACL entry. Example 25-5 shows the IPv6 ACL and shows that three packets have matched this ACL entry.

# **Example 25-5** _Finding Counters of Packets That Matched the ACL_

```
R1# show ipv6 access-list
IPv6 access list V6_ACL_IN
 permit ipv6 any 2001:DB8:1111:2::/64  (3 matches) sequence 10

R1#
```

To clear the IPv6 ACL traffic counters, use the following command:

```
clear access-list counters V6_ACL_IN
```

# Configuring Extended IPv6 ACLs

The previous section covered a simplified syntax for a standard IPv6 ACL. This section will review the additional types of packets that extended IPv6 ACLs can match and the syntax for ACL configuration. Extended IPv6 ACLs can match on many IPv6 header fields as well as ICMPv6 messages, TCP and UDP port numbers, and other IPv6 header items like IPv6 extension headers. Following is the complete syntax of an IPv6 ACL entry.

```
[permit | deny] protocol { [source-ipv6-prefix/prefix-length | any | host source-ipv6-address] [operator [port-number]] | destination-ipv6-prefix/prefix-length | any | host destination-ipv6-address] [operator [port-number]]} [dest-option-type [dest-option-data-type]] [icmp6 value] [flow-label value] [fragments] [log] [log-input] [mobility [mobility-type [mh-number] [mh-type]]] [reflect name] [timeout value] [routing] [routing-type routing-number]] [sequence value] [time-range name]
```

> **NOTE** The next few pages show many details of IPv6 ACL syntax so that you can see the large number of options. The upcoming Figure 25-2 reduces the complexity down to a few key values, similar to those used with IPv4 ACLs, more useful for preparing for the exam.