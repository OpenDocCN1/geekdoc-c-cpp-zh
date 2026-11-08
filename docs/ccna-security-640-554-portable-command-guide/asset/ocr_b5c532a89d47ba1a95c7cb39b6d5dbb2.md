# ## Accessing ASDM

ASDM access requires connecting to a management interface that has some minimal configurations to communicate over the network.

The management interface depends on the model of the ASA:

+   - On an ASA 5505, the management switch port can be any port, except for Ethernet 0/0.
+   - On an ASA 5510 and later, the management interface is Management 0/0. However, another Fast Ethernet interface can also be used.

The minimal configuration can be provided on an ASA 5505 using any of the following methods:

| Method | Configuration |
|---|---|
| **Restore factory default settings** | - The ASA can be reset to provide a basic configuration that is sufficient for a small office/home office (SOHO) deployment.<br>- The configuration includes two preconfigured VLAN networks, Dynamic Host Configuration Protocol (DHCP), and Network Address Translation (NAT) services. |
| **Setup Initialization Wizard** | - The ASA interactively guides an administrator to configure the basic security settings to access ASDM.<br>- Additional HTTP settings must be configured to access the ASDM. |
| **CLI configuration** | - Configure all parameters using the command-line interface (CLI). |

**NOTE:** The next chapter covers the CLI configuration method.

# ## Factory Default Settings

The ASA 5505 with a Base license ships with the following default factory settings:

+   - A default hostname of ciscoasa.
+   - Console or enable passwords, which are blank.
+   - An inside VLAN 1 interface that includes the Ethernet 0/1 through 0/7 switch ports. The VLAN 1 IP address and mask are 192.168.1.1 and 255.255.255.0.
+   - An outside VLAN 2 interface that includes the Ethernet 0/0 switch port. VLAN 2 derives its IP address from the ISP using DHCP.
+   - The default route that is derived from DHCP.
+   - All inside IP addresses to be translated when accessing the outside using interface Port Address Translation (PAT).
+   - The HTTP server to support ASDM access.
+   - An internal DHCP server to provide addresses between 192.168.1.5 and 192.168.1.36 for hosts that connect to a VLAN 1 interface.