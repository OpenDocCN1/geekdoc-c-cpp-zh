| Command | Description |
|---|---|
| `S3(config-if)#switchport port-security violation shutdown` | If a violation occurs, error-disable the port and generate messages. |
| `S3(config-if)#switchport port-security mac-address aaaa.aaaa.aaaa` | Manually configure the IP phone MAC address. |
| `S3(config-if)#switchport port-security mac-address bbbb.bbbb.bbbb` | Manually configure the host MAC address. |
| `S3(config-if)#errdisable recovery cause psecure-violation` | Enables dynamic error recovery of an error-disabled port. |
| `S3(config-if)#errdisable recovery interval 900` | Change the default time to wait from 300 seconds to 900 seconds. |

> **NOTE:** Configure MAC address notification using the global configuration command `mac address-table notification to generate MAC address learning and aging messages.`

> **NOTE:** Although only a single port is used in this example, port security is typically enabled on all user-facing ports.

# Spanning Tree Protocol Attacks

Redundant Layer 2 topologies eliminate single points of failure, but they are more susceptible to broadcast storms, topology flap, and MAC address table instability problems.

Spanning Tree Protocol (STP) is a Layer 2 protocol that provides a loop-free redundant network topology by placing certain ports in the blocking state. A hacker could manipulate STP to conduct an attack by changing the topology of a network (for example, by connecting a rogue switch in an attempt to take over as the root and have all traffic for the immediate switched domain flow through it).

> **NOTE:** Configure the STP enhancement features PortFast, BPDU guard, and root guard features to mitigate STP manipulation attacks.

# STP Enhancement Features

| Feature | Description |
|---|---|
| **PortFast** | ▪ Feature minimizes the time an access port must wait for spanning tree to converge.<br>▪ The Layer 2 access port immediately transitions from the blocking to the forwarding state, bypassing the listening and learning states.<br>▪ It should be enabled on user-facing access ports. |