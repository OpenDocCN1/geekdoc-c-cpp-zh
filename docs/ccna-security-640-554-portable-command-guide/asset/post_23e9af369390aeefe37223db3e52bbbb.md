
- Create the inside network SVI (VLAN 1) and assign it an IP address, create the outside network SVI (VLAN 2) and assign it an IP address, and create a limited DMZ network SVI (VLAN 3) and assign it an IP address and a security level.
- Assign interface Ethernet 0/1 to VLAN 1, E0/0 to VLAN 2, and E0/2 to VLAN 3.
- Enable Telnet, SSH, and HTTPS access and NTP time services.
- Configure a default route to the ISP.

Figure 20-1 shows the network topology for the ASA basic settings example.

![](img/0d9540c65a85f4cb1c32cee46038d8ab_294_0.png)

**Figure 20-1**  Network Topology for the ASA Basic Settings Example

### Configuring Basic Settings Example Using the CLI

| Command | Description |
| --- | --- |
| `ciscoasa(config)# hostname ASA-1` | Name the ASA. |
| `ASA-1(config)# domain-name ccnas.com` | Configure the domain name. |
| `ASA-1(config)# enable password cisco123` | Configure the privileged EXEC password. |
| `ASA-1(config)# key config-key password-encryption cisco123` | Configure the master passphrase key. |
| `ASA-1(config)# password encryption aes` | Enable the master passphrase. |
| `ASA-1(config)# interface vlan 1` | Define the inside SVI (VLAN 1). |
| `ASA-1(config-if)# nameif inside`<br>`INFO: Security level for "inside" set to 100 by default.` | Name the inside SVI. It defaults to a security level of 100. |
| `ASA-1(config-if)# ip address 192.168.1.1 255.255.255.0` | Assign the inside interface IP address. |
| `ASA-1(config-if)# interface vlan 2` | Define the outside SVI (VLAN 2). |
| `ASA-1(config-if)# nameif outside` | Name the outside SVI. It defaults to a security level of 0. |
| `INFO: Security level for "outside" set to 0 by default.` | |
| `ASA-1(config-if)# ip address 209.165.200.226 255.255.255.248` | Assign the outside interface IP address. |
| `ASA-1(config-if)# interface vlan 3` | Define the DMZ SVI (VLAN 3). |
| `ASA-1(config-if)# no forward interface vlan 1` | Disable forwarding to interface VLAN 1, denying the DMZ server the ability to communicate with the inside users. |
| **NOTE:** | Required because of the Base license restriction. |
| `ASA-1(config-if)# nameif dmz` | Name the DMZ SVI. It defaults to a security level of 0. |
| `INFO: Security level for "dmz" set to 0 by default.` | |
| `ASA-1(config-if)# security-level 70` | Change the security level to 70. |
| `ASA-1(config-if)# ip address 192.168.2.1 255.255.255.0` | Assign the DMZ interface an IP address. |
| `ASA-1(config-if)# exit` | Return to global configuration mode. |
| `ASA-1(config)# interface e0/1` | Configure interface Ethernet 0/1. |
| `ASA-1(config-if)# switchport access vlan 1` | Assign it to VLAN 1. |
| `ASA-1(config-if)# no shut` | Enable the physical port. |
| `ASA-1(config-if)# interface e0/0` | Configure interface Ethernet 0/0. |
| `ASA-1(config-if)# switchport access vlan 2` | Assign it to VLAN 2. |
| `ASA-1(config-if)# no shut` | Enable the physical port. |
| `ASA-1(config-if)# interface e0/2` | Configure interface Ethernet 0/2. |
| `ASA-1(config-if)# switchport access vlan 3` | Assign it to VLAN 3. |
| `ASA-1(config-if)# no shut` | Enable the physical port. |
| `ASA-1(config-if)# exit` | Return to global configuration. |
| `ASA-1(config)# password cisco123` | Create a Telnet / SSH password. |
| `ASA-1(config)# telnet 192.168.1.10 255.255.255.255 inside` | Identify which inside host can connect to the ASA using Telnet. |
| `ASA-1(config)# telnet timeout 4` | Change the default EXEC timeout from 5 minutes to 4 minutes. |

To configure NTP, choose **Configuration > Device Setup > System Time > NTP** to open the NTP screen (see Figure 20-7).

![](img/0d9540c65a85f4cb1c32cee46038d8ab_300_0.png)

**Figure 20-7**  System Time NTP Screen

In this window, you can add, edit, or delete an NTP server. When adding a server, you can configure the IP address and authentication parameters. Time derived from an NTP server overrides any time set manually.

To configure a default static route, choose **Configuration > Device Setup > Routing > Static Routes** to open the Static Routes screen (see Figure 20-8).

![](img/0d9540c65a85f4cb1c32cee46038d8ab_300_1.png)

**Figure 20-8**  Static Routes Screen

In this window, you can enter or edit the static and default static routes.

## CHAPTER 21 Configuring Cisco ASA Advanced Settings

This chapter covers the following topics:

### ASA DHCP Services

- DHCP Client
- DHCP Server Services
- Configuring DHCP Server Example Using the CLI
- Configuring DHCP Server Example Using ASDM

### ASA Objects and Object Groups

- Network and Service Objects
- Network, Protocol, ICMP, and Service Object Groups
- Configuring Objects and Object Groups Example Using ASDM

### ASA ACLs

- ACL Syntax
- Configuring ACLs Example Using the CLI
- Configuring ACLs with Object Groups Example Using the CLI
- Configuring ACLs with Object Groups Example Using ASDM

### ASA NAT Services

- Auto-NAT
- Dynamic NAT, Dynamic PAT, and Static NAT
- Configuring Dynamic and Static NAT Example Using the CLI
- Configuring Dynamic NAT Example Using ASDM

### AAA Access Control

- Local AAA Authentication
- Server-Based AAA Authentication
- Configuring AAA Server-Based Authentication Example Using the CLI
- Configuring AAA Server-Based Authentication Example Using ASDM

| Command | Description |
| --- | --- |
| `ciscoasa(config)# dhcpd enable interface-name` | Enable the DHCP server service (daemon) on the specified interface of the ASA. |
| **NOTE:** | The inside interface is usually configured to provide DHCP services by using the `dhcpd enable` command. |

**NOTE:** For the ASA 5505, the maximum number of DHCP client addresses varies depending on the license. If the limit is 10 hosts, the maximum available DHCP pool is 32 addresses. If the limit is 50 hosts, the maximum available DHCP pool is 128 addresses. If the number of hosts is unlimited, the maximum available DHCP pool is 256 addresses.

Use the following commands to manually configure DHCP options:

| Command | Description |
| --- | --- |
| `ciscoasa(config)# dhcpd domain domain-name` | Configure the DNS domain name. |
| `ciscoasa(config)# dhcpd dns dns-ip-address` | Configure the DNS server IP address. |
| `ciscoasa(config)# dhcpd wins wins-ip-address` | Configure a WINS server address (if applicable). |
| `ciscoasa(config)# dhcpd lease seconds` | Configure the lease time in seconds. The default is 3600 seconds (1 hour). |
| `ciscoasa(config)# dhcpd option value` | Configure the DHCP option code. Option code is in the range 0 to 255. |

**NOTE:** If the ASA outside interface is configured as a DHCP client, you can use the `dhcpd auto_config outside` global configuration command to redistribute DHCP options learned from the upstream device to the DHCP clients on the inside interface.

### Configuring DHCP Server Example Using the CLI

Figure 21-1 shows the network topology for the DHCP server example.

![](img/0d9540c65a85f4cb1c32cee46038d8ab_305_0.png)

**Figure 21-1**  DHCP Server Topology Example

| ASA 配置命令 | 说明 |
| --- | --- |
| `ASA-1(config)# dhcpd address`<br>`192.168.1.1-192.168.1.30 inside` | Define the pool of IP addresses assigned to inside users. |
| `ASA-1(config)# dhcpd enable inside` | Enable the DHCP server service (daemon) on the inside interface of the ASA. |
| `ASA-1(config)# dhcpd domain ccnas.com` | Define the domain name for DHCP clients. |
| `ASA-1(config)# dhcpd dns 209.165.200.225` | Define a Domain Name Service (DNS) server to DHCP clients. |
| `ASA-1(config)# dhcpd lease 7200` | Configure the lease time in seconds. The default is 3600 seconds (1 hour). |

**NOTE:** To verify DHCP settings, use the `show dhcpd state` to display the current DHCP state for inside and outside interfaces, the `show dhcpd binding` command to display the current DHCP bindings of inside users, and the `show dhcpd statistics` command to display the current DHCP statistics.

**NOTE:** To clear the DHCP bindings or statistics, use the `clear dhcpd binding` or `clear dhcpd statistics` command.
