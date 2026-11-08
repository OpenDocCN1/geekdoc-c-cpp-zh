
Create an IOS IPS directory in flash:

| Command | Description |
|---|---|
| `Router#mkdir flash:dir-name` | Create a directory in flash. |
| **NOTE:** You could specify other locations. |  |

Copy the Cisco IOS IPS signature package to flash using one of the following methods:

| Command | Description |
|---|---|
| `Router#copy ftp://username:password@server/IOS-Sxxx-CLI.pkg flash:dir-name idconf` | Copy from an FTP server to the directory in flash. |
| `Router#copy tftp://tftp-server/IOS-Sxxx-CLI.pkg flash:dir-name idconf` | Copy from a TFTP server to the directory in flash. |
| `Router#copy usbflash0:/IOS-Sxxx-CLI.pkg flash:dir-name idconf` | Copy from the USB drive to the directory in flash. |

**NOTE:** Add the `idconf` parameter at the end to initiate the compiling process after the copy is complete.

**NOTE:** The preceding list shows only common examples. Other methods are available.

To create the RSA crypto key, copy and paste the following:

- Open the `realm-cisco-pub.key.txt` text file and select the entire contents.
- Copy the text and paste it in global configuration mode.

**NOTE:** The router executes all the commands from the text file and creates the RSA key. Use the `show running-config | section crypto key pubkey-chain rsa` command to verify the configuration.

## Creating an IOS IPS Rule and Specifying the IPS Signature File Location

| Command | Description |
|---|---|
| `Router(config)#ip ips name ips-name [list acl]` | Create an IPS rule name. |
|  | `list acl` is optional and specifies an extended or standard ACL to filter the traffic that will be scanned. All traffic that is permitted by the ACL is subject to inspection by the IPS. Traffic that is denied by the ACL is not inspected by the IPS. |
| `Router(config)#ip ips config location flash:dir-name` | Specify the IPS signature file location. The IPS signature file location is used to restore the IPS configuration in cases such as router reboots or IPS becoming disabled or reenabled. Files, such as signature definitions, signature-type definitions, and signature category information, are written in Extensible Markup Language (XML) format, compressed, and saved to the specified IPS signature location. |

**NOTE:** The IPS does not load the signatures until the rule is applied to an interface.

Enable SDEE and logging event notification:

| Command | Description |
|---|---|
| `Router(config)#ip http server` | Enable the HTTP server (required). |
| `Router(config)#ip ips notify sdee` | Enable IPS SDEE event notification. |
| `Router(config)#ip ips notify log` | Enable logging. |

### Tuning Signatures per Category

Router memory and resource constraints prevent a router from loading all Cisco IOS IPS signatures. Therefore, only load a selected set of signatures that are defined by the categories.

**TIP:** The larger the number of signatures, the larger the amount of memory consumed. Therefore, retire signatures that are irrelevant to your network to save router memory.

All signatures are pregrouped into categories; the categories are hierarchical. An individual signature can belong to more than one category. Top-level categories help to define general types of signatures.

**TIP:** Because the categories are applied in a top-down order, you should first retire all signatures, followed by unretiring specific categories.

| Command | Description |
|---|---|
| `Router(config)#ip ips signature-category` | Enter IPS category configuration mode to tune Cisco IOS IPS signature parameters on the basis of a signature category. |
| `Router(config-ips-category)#category {all \| ios_ips {basic \| advanced}}` | Specify the signature category to change, and enter IPS category action mode.<br><br>**NOTE:** Many other categories and sub-categories exist (for example, attack, dos, ddos, email, p2p). For a list of supported top-level categories, use the router CLI help (`?`).<br><br>**NOTE:** IOS IPS processes category commands in the order listed in the configuration. |
| `Router(config-ips-category-action)#retired {false \| true}` | Specify whether a signature or signature category definition should be saved in the router memory.<br><br>`false` unretires all signatures within a given category.<br><br>`true` retires all signatures within a given category.<br><br>**NOTE:** Retired signatures are not scanned by Cisco IOS IPS and therefore do not fire alarms.<br><br>**NOTE:** To return to the default action, use the `no retired` command. |
| `Router(config-ips-category-action)#event-action action` | Change router actions for a specified signature category.<br><br>Actions include the following:<br><br>- `deny-attacker-inline`<br>- `deny-connection-inline`<br>- `deny-packet-inline`<br>- `produce-alert`<br>- `reset-tcp-connection`<br><br>**NOTE:** Event actions associated with a category can be entered separately or on a single line.<br><br>**NOTE:** To verify the event-action configuration, use the `show ip ips signatures` command. |
| `Router(config-ips-category-action)#alert-severity {high \| medium \| low \| informational}` | (Optional) Change the alert severity rating for a given signature or signature category. **NOTE:** To return to the default action, use the `no alert-severity` command. |
| `Router(config-ips-category-action)#fidelity-rating rating` | (Optional) Changes the signature fidelity rating for a given signature category. |
| `Router(config-ips-category)#exit` | Return to IPS category mode. |
| `Router(config-ips-category)#exit`<br>`Do you want to accept these changes? [confirm]` | After signature-based changes are complete, you are prompted to confirm whether or not the changes are acceptable.<br><br>Confirming the changes instructs IOS IPS to compile the changes for the signature and modify memory structures to reflect the change and save the changes to the IPS location specified. |

**CAUTION:** Do not unretire the all category because it contains all the signatures in a signature release. The IOS IPS cannot compile and use all the signatures at one time; if it were to do so, it would run out of memory.

**NOTE:** Use the `show ip ips` command to display IPS configuration information. Use the `show ip ips signature-category {config}` command to display IPS signature parameters by signature category.

Apply the IPS rule to a desired interface and specify the direction:

| Command | Description |
|---|---|
| `Router(config-if)#ip ips ips-name {in \| out}` | Apply the IPS rule to an interface. The router loads the signatures and builds the signature engines when IPS is applied to the first interface:<br><br>`in` inspects only incoming traffic.<br><br>`out` inspects only outgoing traffic.<br><br>**NOTE:** The command can be repeated to configure incoming and outgoing traffic. |

**NOTE:** The router prompt disappears while the signatures are loading and the signature engines are building. It reappears after these tasks are complete.

**NOTE:** Building the signature engine can take several minutes depending on the router platform and how many signatures are being loaded. It is recommended that you enable logging messages so you can monitor the engine building status.

**NOTE:** The process creates six files in the IPS directory: `router-sigdef-default.xml`, which contains all the category default signature definitions; `router-sigdef.xml`, which contains signature definitions that have been changed from the default; `router-sigdef-type.xml`, which is a file that has all the signature parameter definitions; `router-sigdef-category.xml`, which has all the signature category information, such as category ios_ips basic and advanced; `router-sigdef-seap.xml`, which contains changes made to the default Signature Event Action Processor (SEAP) parameters; and `router-seap-typedef.xml`, which contains all of the SEAP parameter definitions.

(Maintenance) To periodically update the signature package after the IPS has been configured, use this command:

`Router#copy url idconf` Load a signature package to the identified IPS directory.

`url` specifies the location from which the router loads the signature file (for example, FTP, TFTP, USB, rcp).

**NOTE:** Use the `clear ip ips configuration` to remove all IPS configuration entries and release dynamic resources. Use the `clear ip ips statistics` command to reset statistics on packets analyzed and alarms sent.

**NOTE:** Configure automatic signature updates using the `ip ips auto-update` command. Updates can be configured to run on the basis of a preset time.

## Configuring IOS IPS Example

- 1. Create an IOS IPS configuration directory called **IPS-DIR** in flash.
- 2. Copy the Cisco IOS IPS signature package from a USB drive to flash.
- 3. Configure an IOS IPS crypto key.
- 4. Create an IPS rule called **MY-IPS** and specify the location of the IPS file.
- 5. Enable SDEE event notification.
- 6. Retire the all signature category and then unretire the **ios_ips basic** and the **ids_evasion** categories. Change the **ids_evasion** default event notification.
- 7. Assign the IPS rule to inspect inbound traffic on the Fast Ethernet 0/0 interface.

Figure 13-1 shows the network topology for the IOS IPS example.

![](img/0d9540c65a85f4cb1c32cee46038d8ab_202_0.png)

**Figure 13-1**  Network Topology for the IOS IPS Example
