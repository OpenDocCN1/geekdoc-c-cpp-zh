| Command | Description |
|---|---|
| `Router(config-sec-zone-pair)#service-policy type inspect MY-POLICY` | Assign the service policy MY-POLICY for all traffic travelling from the source to the destination. |
| `R1(config-sec-zone-pair)#exit` | Return to global configuration mode. |
| `R1(config)#int fa0/0` | Enter interface Fa0/0 configuration mode. |
| `R1(config-if)#zone-member security INTERNET` | Assign the interface to be a member of the INTERNET zone. |
| `R1(config-if)#exit` | Return to global configuration mode. |
| `R1(config)#int fa0/1` | Enter interface Fa0/1 configuration mode. |
| `R1(config-if)#zone-member security PRIVATE` | Assign the interface to be a member of the PRIVATE zone. |

**NOTE:** Use the `show zone security` and the `show zone-pair security` commands to verify the configuration.

**NOTE:** The preceding example was based on a fairly simple security policy. You can use Cisco Configuration Professional (CCP) to create more comprehensive security policies.

# Configuring an IOS ZFW Using CCP Example

To configure basic interzone policies using CCP, follow these steps:

+   1. Start the Basic Firewall Wizard.
+   2. Select trusted and untrusted interfaces.
+   3. Review and verify resulting policies.
+   4. (Optional) Enable logging.
+   5. View firewall status and activity.
+   6. (Optional) Modify basic policy objects.

**NOTE:** LAN and WAN configurations must be completed before using the Firewall Wizard.

Use the Basic Firewall Wizard to configure a basic firewall. Choose **Configure > Security > Firewall > Firewall > Create Firewall > Basic Firewall** to open the Basic Firewall Wizard. Figure 12-2 shows the Basic Firewall Wizard screen.