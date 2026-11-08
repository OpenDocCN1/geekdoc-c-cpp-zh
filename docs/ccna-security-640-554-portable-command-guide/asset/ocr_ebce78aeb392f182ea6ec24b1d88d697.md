ACLs operate in two directions:

| ACL direction | Description |
|---|---|
| **Inbound ACLs** | Incoming packets are processed before they are routed to an outbound interface. |
| **Outbound ACLs** | Incoming packets are routed to the outbound interface, and then they are processed through the outbound ACL. |

**NOTE:** Inbound ACLs are usually more efficient because they do not perform routing lookups on denied packets. Only permitted packets are processed for routing.

Routers support two types of ACL:

| ACL type | Rules |
|---|---|
| **Standard ACL** | - Filters IP packets based on source address only.<br>- ACLs can be numbered or named.<br>- Valid number ranges include 1–99 and 1300–1999. |
| **Extended ACL** | - Filters IP packets based on protocol, source and destination addresses, source and destination UDP and TCP ports, and ICMP and Internet Group Management Protocol (IGMP) message types.<br>- ACLs can be numbered or named.<br>- Valid number ranges include 100–199 and 2000–2699. |

**NOTE:** Numbered ACLs are configured using the `access-list` global configuration command. You cannot edit numbered ACLs using the `ip access-list` command. New ACL entries are appended to the end of the ACL.

Standard and extended ACLs can be named. Named ACLs are useful because they provide a hint as to the purpose of the ACL. Names can be alphanumeric but must begin with an alphabetic character. In addition, names cannot contain spaces or punctuation.

**NOTE:** Named ACLs are configured using the `ip access-list` global configuration command.

**TIP:** Use uppercase letters to make the named ACL stand out in the configuration.

**TIP:** You can edit numbered and named ACLs using the `ip access-list` command.