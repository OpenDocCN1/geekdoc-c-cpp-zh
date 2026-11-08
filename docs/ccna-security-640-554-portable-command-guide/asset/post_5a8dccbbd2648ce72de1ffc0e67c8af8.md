
## Configuring DHCP Server Example Using ASDM

To enable DHCP server services, choose **Configuration > Device Management > DHCP > DHCP Server**. ASDM opens the DHCP Server screen (see Figure 21-2).

![](img/0d9540c65a85f4cb1c32cee46038d8ab_306_0.png)

**Figure 21-2**  DHCP Server Screen

In this window, you can modify the general DHCP settings.

To enable DHCP services to inside users, click the inside interface and click the **Edit** button. ASDM then opens the Edit DHCP Server dialog, shown in Figure 21-3.

**NOTE:** Remember to click the **Apply** button any time a change is made.

## ASA Objects and Object Groups

Objects make it easier to maintain configurations. When an object is modified, the change automatically applies to all rules that use the specified object. Objects are used in Network Address Translation (NAT), access lists, and nested into other object groups.

The ASA supports the following:

| Category | Description |
|---|---|
| **Objects** | - An object identifies an IP address/mask or a protocol (and a port).<br>- An object can be reused in several configurations.<br>- The ASA supports network objects and service objects.<br>- Objects are created using the <code>object {network &#124; service} object-name</code> command. |
| **Object groups** | - Object groups are used to group objects.<br>- Objects can be attached or detached from multiple object groups.<br>- You can create network, protocol, and Internet Control Message Protocol (ICMP)-type object groups created using the <code>object-group {network &#124; protocol &#124; icmp-type} group-name</code> command.<br>- You can also create service object groups by using <code>object-group service group-name [tcp &#124; udp &#124; tcp-udp]</code>. |

### Network and Service Objects

A network object contains a single IP address/mask pair that can be identified using a host, subnet, or range of addresses.

Use the following commands to create or edit a network object:

| Command | Description |
|---|---|
| <code>ciscoasa(config)# object network object-name</code> | Create or edit a network object and enter network object configuration mode. |
| <code>ciscoasa(config-network-object)# {host ip_addr &#124; subnet net_addr net_mask &#124; range ip_addr_1 ip_addr_2}</code> | Assign the IP address to the named object. You can configure a host address, a subnet, or a range of addresses. |

**NOTE:** Use the `no` form of any of these three commands to remove a network object.

**NOTE:** There can only be one statement in the network object. Entering a second IP address/mask pair will replace the existing configured statement.

**NOTE:** To verify, use the `show running-config object` command.

**NOTE:** You cannot remove an object group or make an object group empty if it is used in a command.

### Network, Protocol, ICMP, and Service Object Groups

Use the following commands to create a network object group:

| Command | Description |
|---|---|
| <code>ciscoasa(config)# object-group network group-name</code> | Create or edit a network object group and enter network object group configuration mode. |

Use the following commands to identify specific hosts or network object groups:

| Command | Description |
|---|---|
| <code>ciscoasa(config-network-object-group)# network-object host ip-addr</code> | Assign an IP address to the named object. |
| <code>ciscoasa(config-network-object-group)# group-object group-name</code> | Assign an object group to the named object.<br><br>**NOTE:** This allows for logical grouping of the same type of objects and construction of hierarchical object groups for structured configuration. |

**NOTE:** Multiple hosts, networks, and objects can be added to a network object group.

**NOTE:** A network object group cannot be used to implement NAT. A network object is required to implement NAT.

A protocol-based object group combines IP protocols into one object.

Use the following commands to create a protocol object group:

| Command | Description |
|---|---|
| <code>ciscoasa(config)# object-group protocol group-name</code> | Create or edit a protocol object group and enter protocol object group configuration mode. |

Use one of the following commands to identify a protocol or other protocol object groups:

| Command | Description |
|---|---|
| <code>ciscoasa(config-protocol-object-group)# protocol-object protocol</code> | Define the protocols in the group. **NOTE:** The `protocol` parameter is the IP protocol numeric identifier (1 through 254) or a keyword identifier (for example, `icmp`, `tcp`, `udp`, or `ip` to include all IP protocols). |
| <code>ciscoasa(config-protocol-object-group)# group-object group-name</code> | Assign an object group to the named object. |

Use the following commands to create an ICMP object group:

| Command | Description |
|---|---|
| <code>ciscoasa(config)# object-group icmp-type group-name</code> | Create or edit an ICMP object group and enter ICMP type object group configuration mode. |

Use one of the following commands to identify a protocol or other protocol object groups:

| Command | Description |
|---|---|
| <code>ciscoasa(config-icmp-object-group)# icmp-object icmp-type</code> | Define the ICMP types in the group. Enter the command for each type. |
| <code>ciscoasa(config-icmp-object-group)# group-object group-name</code> | Assign an object group to the named object. |

A service-based object group is used to group TCP, UDP, or TCP and UDP ports into an object. The ASA enables the creation of a service object group that can contain a mix of TCP services; UDP services; ICMP-type services; and any protocol such as Encapsulation Security Protocol (ESP), generic routing encapsulation (GRE), and TCP.

Use the following commands to create a service object group:

| Command | Description |
|---|---|
| <code>ciscoasa(config)# object-group service group-name</code> | Create or edit a service group object and enter service object group configuration mode. |

Use one of the following commands to identify a protocol or other protocol object groups:

| Command | Description |
|---|---|
| <code>ciscoasa(config-service-object-group)# port-object eq service</code> | Add a port object to a service object group. Specify the decimal number or name of a TCP or UDP port for a service object. |
| <code>ciscoasa(config-service-object-group)# group-object group-name</code> | Assign an object group to the named object. |

ACLs on a security appliance can be used for the following:

| Category | Description |
|---|---|
| Through-traffic packet filtering | - Traffic is passing through the appliance from one interface to another interface.<br>- The configuration requires an ACL to be defined and then applied to an interface. |
| To-the-box traffic packet filtering | - Traffic (for example, Telnet, SSH, Simple Network Management Protocol [SNMP]) is destined for the appliance.<br>- It filters traffic destined to the ASA management plane.<br>- It is completed in one step but requires an additional set of rules to implement access control.<br>- Also known as a management access rule. |

## ACL Syntax

You can use many options with ACLs. However, for most needs, a more useful and condensed version of the syntax is as follows:

```
    ciscoasa(config)# access-list id extended {deny | permit} protocol
    {source_addr source_mask} | any | host src_host |
    interface src_if_name
    {operator port [port]}
    {dest_addr dest_mask} | any | host dst_host |
    interface dst_if_name
    {operator port [port]}
```

**NOTE:** The `interface` keyword is used for to-the-box filtering.

**NOTE:** Explanation of all ACL syntax is beyond the scope of this chapter.

**NOTE:** Use the `help access-list` command to view complete syntax information.

**NOTE:** To verify ACLs, use the `show access-list` and `show running-config access-list` commands.

**NOTE:** To erase a configured ACL, use the `clear configure access-list id` command.

After you configure an ACL to identify traffic allowed or denied by the ASA, the next step is to apply the ACL to an interface in either the inbound or the outbound direction.
