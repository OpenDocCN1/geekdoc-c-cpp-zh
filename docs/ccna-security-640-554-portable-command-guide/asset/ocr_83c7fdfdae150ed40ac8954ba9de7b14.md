| Security measure | Description |
|---|---|
| **Filter incoming traffic** | Only receive packets that have a destination address within your allocated block from an Internet service provider and multicast group address or link-local address for NDP. |
| **Filter ICMPv6 messages** | Granularly filter ICMPv6 messages at the perimeter. (Remember, ICMPv6 is needed for protocol operations such as NDP.) |
| **Drop packets with unknown extension headers** | Drop RH0 packets and unknown extension headers at the perimeter and throughout the interior of the network. |

# Secure Transition Mechanisms

| Security measure | Description |
|---|---|
| **Secure dual stack** | Prefer dual stack as the transition mechanism, but secure IPv4 and IPv6 equally. |
| **Implement IPsec VPN tunnels** | When tunnels are used to send sensitive traffic over a public network, they should be secured by adding IPsec authentication and confidentiality that can prevent both the injection/sniffing attacks and unauthorized access. |
| **Do not allow tunnels through perimeter unless required** | Terminate tunnels at the edge and do not permit host-to-host tunnels. |

# Future Security Enhancements

Consider current and future security enhancements:

| Security enhancement | Description |
|---|---|
| **Secure Neighbor Discovery (SeND)** | Combines NDP with crypto features. The SeND protocol enhances NDP with address ownership proof, message protection, and router authorization. |
| **RA-Guard** | RA-Guard blocks router advertisement and router redirect ICMP packets from Layer 2 ports. |

> **NOTE:** IPv6 security will now be included in other chapters.