+   - Create the inside network SVI (VLAN 1) and assign it an IP address, create the outside network SVI (VLAN 2) and assign it an IP address, and create a limited DMZ network SVI (VLAN 3) and assign it an IP address and a security level.
+   - Assign interface Ethernet 0/1 to VLAN 1, E0/0 to VLAN 2, and E0/2 to VLAN 3.
+   - Enable Telnet, SSH, and HTTPS access and NTP time services.
+   - Configure a default route to the ISP.

Figure 20-1 shows the network topology for the ASA basic settings example.

![](bbox=[0.1, 0.23, 0.95, 0.46])

Figure 20-1  Network Topology for the ASA Basic Settings Example

# Configuring Basic Settings Example Using the CLI

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