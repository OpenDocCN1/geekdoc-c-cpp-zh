![](bbox=[0.089, 0.083, 0.929, 0.233])

**Figure 18-3** ASA 5510 Front and Back Panel

The back panel of the ASA 5510 features are numbered in Figure 18-3 as follows:

| No. | Feature | Description |
|---|---|---|
| 1 | **SSM** | The SSM can be used to add the following:<br>▪ 4-Port Gigabit Ethernet Security Services Module (4GE SSM)<br>▪ Advanced Inspection and Prevention Security Services Module (AIP-SSM)<br>▪ Series Content Security and Control Security Services Module (CSC-SSM) |
| 2 | **USB ports** | Two USB ports can be used to enable additional services and capabilities. |
| 3 | **OOB management interface** | A dedicated Fast Ethernet out-of-band (OOB) management interface. |
| 4 | **Four Fast Ethernet interfaces** | By default, interfaces Fa0/0 through Fa0/2 are enabled, but the Fa0/3 is disabled.<br><br>The OOB interface could also be used as a fifth Fast Ethernet port (ASA software must support). |
| 5 | **Flash card slot** | Provides storage for system images and configuration files. |
| 6 | **LED indicators** | Power, Status, Active, VPN, and Flash LED indicators. |
| 7 | **Management ports** | A console port for the initial configuration.<br><br>An auxiliary port could be used for OOB management. |

# ASA Security Levels

The building blocks of ASA security are assigning interfaces to security levels to distinguish between inside (trusted) and outside (untrusted) networks:

+   - Security levels define the level of trustworthiness of an interface.
+   - The higher the level, the more trusted the interface.