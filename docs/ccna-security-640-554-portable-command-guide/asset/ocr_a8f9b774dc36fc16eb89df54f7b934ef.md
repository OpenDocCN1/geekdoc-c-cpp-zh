| Command | Description |
|---|---|
| `ciscoasa(config)# dhcpd enable interface-name` | Enable the DHCP server service (daemon) on the specified interface of the ASA. |
| **NOTE:** | The inside interface is usually configured to provide DHCP services by using the `dhcpd enable` command. |

**NOTE:** For the ASA 5505, the maximum number of DHCP client addresses varies depending on the license. If the limit is 10 hosts, the maximum available DHCP pool is 32 addresses. If the limit is 50 hosts, the maximum available DHCP pool is 128 addresses. If the number of hosts is unlimited, the maximum available DHCP pool is 256 addresses.

Use the following commands to manually configure DHCP options:

| Command | Description |
|---|---|
| `ciscoasa(config)# dhcpd domain domain-name` | Configure the DNS domain name. |
| `ciscoasa(config)# dhcpd dns dns-ip-address` | Configure the DNS domain name. |
| `ciscoasa(config)# dhcpd wins wins-ip-address` | Configure a WINS server address (if applicable). |
| `ciscoasa(config)# dhcpd lease seconds` | Configure the lease time in seconds. The default is 3600 seconds (1 hour). |
| `ciscoasa(config)# dhcpd option value` | Configure the DHCP option code. Option code is in the range 0 [and] 255. |

**NOTE:** If the ASA outside interface is configured as a DHCP client, you can use the `dhcpd auto_config outside` global configuration command to redistribute DHCP options learned from the upstream device to the DHCP clients on the inside interface.

# Configuring DHCP Server Example Using the CLI

Figure 21-1 shows the network topology for the DHCP server example.