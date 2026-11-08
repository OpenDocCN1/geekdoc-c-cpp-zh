# ACLs and Private VLANs

| Feature | Description |
|---|---|
| **Port-based ACLs for Layer 2 ports** | You can apply security policies on individual switch ports. |
| **Private VLANs** | Private VLANs restrict traffic between hosts in a common segment by segregating traffic at Layer 2, turning a broadcast segment into a nonbroadcast multiaccess-like segment. |
| **Private VLAN edge** | Private VLAN edge provides security and isolation between switch ports, which helps ensure that users cannot snoop on other users’ traffic. |

# Cisco Integrated Security Features

Cisco integrated security features are easy-to-use tools to effectively prevent potentially damaging Layer 2 security threats. Features include the previously covered port security and DHCP snooping, dynamic ARP inspection, and IP source guard.

| Feature | Description |
|---|---|
| **DHCP snooping** | Prevents malicious users from spoofing a Dynamic Host Configuration Protocol (DHCP) server and sending out bogus addresses. This feature is used by other primary security features to prevent a number of other attacks, such as ARP poisoning. |
| **Dynamic ARP inspection** | Dynamic ARP inspection (DAI) helps ensure user integrity by preventing malicious users from exploiting the unsecure nature of the ARP protocol. |
| **IP source guard** | IP source guard prevents a malicious user from spoofing or taking over another user’s IP address. It does so by creating a binding table between the client’s IP and MAC address, port, and VLAN. |

# Secure the Switch Management Plane

Just as the management plane is secured on Cisco routers, the Layer 2 switching man-