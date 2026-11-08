**NOTE:** To verify VLAN settings, use the `show switch vlan` command. To verify interface settings, use the `show interface` or `show int ip brief` command.

**NOTE:** ASA Fast Ethernet interfaces are designated as Ethernet x/x (for example, E0/0).

# Configuring a Third SVI

An ASA 5505 with the Security Plus license automatically supports the creation of additional VLANs to create other zones such as a demilitarized zone (DMZ) zone. However, an ASA 5505 with a Base license only supports a third, restricted SVI that is limited from initiating contact to another specified VLAN.

Use the following to configure a third VLAN SVI on an ASA 5505 with a Base license:

| Command | Description |
|---|---|
| `ciscoasa(config)# interface interface/number` | Specify a Layer 2 physical port. |
| `ciscoasa(config-if)# no forward interface vlan vlan-id` | Limit the interface from initiating contact to another VLAN. |

> **NOTE:** The `vlan-id` argument specifies the VLAN ID to which this VLAN interface cannot initiate traffic.

> **NOTE:** You must configure this command before the interface is named.

> **NOTE:** Configure this command on the third SVI after the inside and outside VLAN interfaces have been configured.

# Configuring the Management Plane

# Enabling Telnet, SSH, and HTTPS Access

The ASA can be configured to accept Telnet connections from a single host or a range of hosts on the inside network. Use the following commands to enable the Telnet service:

| Command | Description |
|---|---|
| `ciscoasa(config)# passwd password` | Configure the Telnet / SSH password. |
| `ciscoasa(config)# telnet ip-address subnet-mask interface-name` | Identify which inside hosts can telnet to which ASA interface. |
| `ciscoasa(config)# telnet timeout minutes` | Alters the default EXEC timeout of 5 minutes. |