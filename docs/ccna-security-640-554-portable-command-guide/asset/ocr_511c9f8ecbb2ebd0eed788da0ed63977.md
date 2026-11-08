# Configuring an IPv6 ACL Example

Figure 11-13 displays the network topology for the IPv6 ACL example.

![](bbox=[0.078, 0.136, 0.809, 0.228])

**Figure 11-13**  Network Topology for the IPv6 ACL Example

| Configuration | Description |
|---|---|
| `R1(config)#ipv6 access-list IPV6-ACL-IN` | Define an IPv6 ACL. |
| `R1(config-ipv6-acl)#remark Basic anti-spoofing ACL` | Document the ACL. |
| `R1(config-ipv6-acl)#deny 2001:db8:2c80:1000::/64 any` | Deny incoming traffic with the source address the same as the internal network address. |
| `R1(config-ipv6-acl)#permit any 2001:db8:2c80:1000::1/128` | Permit traffic to reach the server. |
| `R1(config-ipv6-acl)#interface serial 0/0` | Enter interface configuration mode for the serial interface. |
| `R1(config-if)#ipv6 traffic-filter IPV6-ACL-IN in` | Apply the IPV6-ACL-IN ACL incoming on the outside interface. |