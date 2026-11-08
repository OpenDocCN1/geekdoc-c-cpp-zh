
### ASA 5505 Port Configuration

The ASA 5510 devices or later have Layer 3 routed interfaces. The interfaces are enabled by assigning an IP address, interface name, and security level.

The ASA 5505 is configured differently than higher models because it does not have any Layer 3 interfaces. It comes with an integrated eight-port Layer 2 Fast Ethernet switch. Each port is individually assigned to a specific VLAN. All Layer 3 parameters (that is, IP address, interface name, and security level) must be configured for the VLAN interface, also known as a switch virtual interface (SVI). Switch ports on the same VLAN can communicate with each other using hardware switching.

### ASA 5505 Deployment Scenarios

The ASA 5505 is commonly used as an edge security device that connects a small business to an ISP to access the Internet. It can be deployed as follows:

|  |  |
|---|---|
| **Small branch deployment** | - The ASA 5505 can be deployed with 2 security zones:<br>&nbsp;&nbsp;- VLAN 1 with security level 100 for inside hosts<br>&nbsp;&nbsp;- VLAN 2 with security level 0 for the Internet connection |
| **Small business deployment** | - The ASA 5505 can be deployed with 3 security zones:<br>&nbsp;&nbsp;- VLAN 1 for the inside network connecting workstations<br>&nbsp;&nbsp;- VLAN 2 for the outside network connecting to the Internet<br>&nbsp;&nbsp;- VLAN 3 for the DMZ connecting to a company web servers |
| **Enterprise deployment** | - The ASA 5505 can be used by telecommuters and home users to connect to a centralized location using a VPN |

### ASA 5505 Configuration Options

ASA devices can be configured and managed using either the

- Command-line interface (CLI) required for initial ASA deployment and maintenance
- Adaptive Security Device Manager (ASDM) GUI

> **NOTE:** ASDM simplifies the deployment and maintenance of an ASA.

## CHAPTER 19: Introduction to ASDM

This chapter covers the following topics:

- **Adaptive Security Device Manager**
  - Accessing ASDM
  - Factory Default Settings
  - Resetting the ASA 5505 to Factory Default Settings
  - Erasing the Factory Default Settings
  - Setup Initialization Wizard
- **Installing and Running ASDM**
  - Running ASDM
- **ASDM Wizards**
  - The Startup Wizard
  - VPN Wizards
  - Advanced Wizards

### Adaptive Security Device Manager

Cisco Adaptive Security Device Manager (ASDM) is a Java-based GUI tool that facilitates the setup, configuration, monitoring, and troubleshooting of Cisco Adaptive Security Appliances (ASA).

**NOTE:** ASDM is now preloaded in flash memory on any ASA versions 7.0 and later.

ASDM can be

- Run from a browser as a Java Web Start application that is dynamically downloaded from the ASA flash, allowing an administrator to configure and monitor that ASA device
- Downloaded from flash and installed locally on a host as an application, allowing an administrator to use ASDM to configure and manage multiple ASA devices

### Accessing ASDM

ASDM access requires connecting to a management interface that has some minimal configurations to communicate over the network.

The management interface depends on the model of the ASA:

- On an ASA 5505, the management switch port can be any port, except for Ethernet 0/0.
- On an ASA 5510 and later, the management interface is Management 0/0. However, another Fast Ethernet interface can also be used.

The minimal configuration can be provided on an ASA 5505 using any of the following methods:

| Method | Configuration |
|---|---|
| **Restore factory default settings** | - The ASA can be reset to provide a basic configuration that is sufficient for a small office/home office (SOHO) deployment.<br>- The configuration includes two preconfigured VLAN networks, Dynamic Host Configuration Protocol (DHCP), and Network Address Translation (NAT) services. |
| **Setup Initialization Wizard** | - The ASA interactively guides an administrator to configure the basic security settings to access ASDM.<br>- Additional HTTP settings must be configured to access the ASDM. |
| **CLI configuration** | - Configure all parameters using the command-line interface (CLI). |

**NOTE:** The next chapter covers the CLI configuration method.

### Factory Default Settings

The ASA 5505 with a Base license ships with the following default factory settings:

- A default hostname of ciscoasa.
- Console or enable passwords, which are blank.
- An inside VLAN 1 interface that includes the Ethernet 0/1 through 0/7 switch ports. The VLAN 1 IP address and mask are 192.168.1.1 and 255.255.255.0.
- An outside VLAN 2 interface that includes the Ethernet 0/0 switch port. VLAN 2 derives its IP address from the ISP using DHCP.
- The default route that is derived from DHCP.
- All inside IP addresses to be translated when accessing the outside using interface Port Address Translation (PAT).
- The HTTP server to support ASDM access.
- An internal DHCP server to provide addresses between 192.168.1.5 and 192.168.1.36 for hosts that connect to a VLAN 1 interface.

**NOTE:** You can change these settings manually using the CLI or interactively using either the CLI Setup Initialization Wizard or using the ASDM Startup Wizard.

**NOTE:** The Reset button on the ASA 5505 is disabled and inoperable by default.

### Resetting the ASA 5505 to Factory Default Settings

You can restore the ASA to its factory default configuration by using the following:

| Command | Description |
|---|---|
| `ciscoasa# config t` | Enter global configuration mode. |
| `ciscoasa(config)# config factory-default` | Reset the ASA to its factory default settings.<br><br>**NOTE:** A warning appears stating that the boot system configuration (startup configuration) will be cleared.<br><br>**NOTE:** The ASA loads a default configuration into the running configuration. |
| `ciscoasa(config)# reload save-config noconfirm` | Save the configuration and then reload the ASA without asking for confirmation. |

### Erasing the Factory Default Settings

| Command | Description |
|---|---|
| `ciscoasa# write erase` | Erase the startup-configuration file. |
| `ciscoasa(config)# reload noconfirm` | Reload the ASA without confirmation. |

### Setup Initialization Wizard

When the default factory settings are erased and an ASA is reloaded, the ASA Setup Initialization Wizard prompts will eventually appear asking **Pre-configure firewall now through interactive prompts [yes]?**

Answering no cancels the Setup Initialization Wizard, and the ASA displays its default prompt. In this case, you must manually configure the ASA via the CLI.

Pressing **Enter** accepts the default (**yes**), and the ASA will interactively guide an administrator to configure basic ASA features, including the following:

- Firewall mode
- Enable password
- Enable password recovery
- Time and date settings
- Inside IP address and mask
- ASA device name
- Domain name

**NOTE:** The security appliance displays the default values in brackets (`[ ]`) before prompting the user to accept or change them. To accept the default input, press **Enter**.

When the interactive portion of the Setup Initialization Wizard completes, the security appliance displays the summary of the new configuration and prompts the user to save or reject the settings:

- Answering **yes** saves the configuration and displays the configured hostname prompt.
- Answering **no** restarts the Setup Initialization Wizard. Any changes previously made become the new default settings, enabling an administrator to correct a misconfigured setting.

The Setup Initialization Wizard provides most of the settings for ASDM. However, the HTTP service must be enabled.

To allow access to ASDM, enable HTTPS connections from any host on the inside network:

| Command | Description |
|---|---|
| `ciscoasa(config)# http server enable` | Enable HTTP services. |
| `ciscoasa(config)# http ip-address network-mask interface-name` | Identify a host or hosts that can access the ASA HTTP server using ASDM. |

**NOTE:** To remove and disable the ASA HTTP server service, use the global configuration command `clear configure http`.

### Installing and Running ASDM

The ASDM interface can be accessed from any workstation with an IP address included in the HTTP trusted network list.

**TIP:** Before attempting to establish a secure ASDM connection to the ASA, verify that IP connectivity exists between the workstation and the Cisco ASA.

With a factory default configuration

- A host on the 192.168.1.0/24 network can connect to the ASA default management IP address of 192.168.1.1 using ASDM.
- The host must establish a connection through a browser to the inside interface IP address using the HTTPS protocol.

A security certificate window may appear. Depending on the browser settings, select **Yes** or click on **Continue to This Website** to continue to the ASDM launcher window.
