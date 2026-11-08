agent to be disabled. Then, the first time an snmp-server global command is configured, IOS enables the SNMP agent.

> > **NOTE** Because of this odd way to enable the SNMP agent, to disable the agent, you have to first remove all SNMP configuration with no commands, and then reload the router or switch. There is also no single command to disable the SNMP agent.

With that backdrop, a typical SNMPv2c configuration requires only one or two settings. To be useful, the agent needs at least a read-only (RO) community string. The agent will not reply to SNMPv2c Get messages without at least the RO community string configured. The network engineer may also want the agent to have a read-write (RW) community string, to support Set messages.

> > **NOTE** When configuring an RW community, use some caution: configuring an RW community means that you have defined a clear-text password that can be used to configure many settings on the router or switch.

The following checklist details the commands used to configure SNMPv2c on a Cisco router or switch. This list shows the method to configure the RO and RW communities, plus a few optional but common settings (location and contact information).

![](bbox=[0.07, 0.514, 0.142, 0.56])

+   1. **Step 1.** Use the snmp-server community communitystring RO [ipv6 acl-name] [acl-name] command in global configuration mode to enable the SNMP agent (if not already started), set the read-only community string, and restrict incoming SNMP messages based on the optional referenced IPv4 or IPv6 ACL.
+   2. **Step 2.** (Optional) Use the snmp-server community communitystring RW [ipv6 acl-name] [acl-name] command in global configuration mode to enable the SNMP agent (if not already started), set the read-write community string, and restrict incoming SNMP messages based on the optional referenced IPv4 or IPv6 ACL.
+   3. **Step 3.** (Optional) If referenced by an snmp-server community command, configure an IPv4 or IPv6 ACL, with the same name or number referenced by the snmp-server community command, with the ACL permitting by matching the source IPv4 or IPv6 address of the allowed SNMP management hosts.
+   4. **Step 4.** (Optional) Use the snmp-server location text-describing-location command in global configuration mode to document the location of the device.
+   5. **Step 5.** (Optional) Use the snmp-server contact contact-name command in global configuration mode to document the person to contact if problems occur.

> > **NOTE** In the SNMP model, the SNMP agent acts as a server, with the NMS (SNMP Manager) acting as an SNMP client by requesting information with Get messages. The IOS snmp-server command happens to emphasize the idea that the SNMP agent on a router or switch acts as the SNMP server.