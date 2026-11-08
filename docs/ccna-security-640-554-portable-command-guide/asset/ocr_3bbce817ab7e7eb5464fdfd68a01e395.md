**NOTE:** Instead of manually resetting an error-disabled port using the shutdown and no shutdown sequence, you can implement a dynamic port auto-recovery solution.

# Configuring Optional Port Security Settings

Optionally, you can configure the following port security settings:

+   - Statistically assign the secure MAC addresses to the port and enable the switch to dynamically learn the secure MAC addresses and add them to the running configuration.
+   - Enable the switch to automatically recover an error-disabled port after a specified amount of time.
+   - Enable address aging (if required).

MAC addresses can be explicitly assigned to the port manually or learned dynamically:

| Command | Description |
|---|---|
| `Switch(config-if)#switchport port-security mac-address mac-address` | Manually assign the MAC addresses connecting to the port. Repeat the command for each secure MAC address. |
| `Switch(config-if)#switchport port-security mac-address sticky` | Enable the switch to dynamically learn the connected MAC addresses until the maximum is reached. Learned MAC addresses are added to the running configuration. |

**NOTE:** Manually entering each secure MAC address is not a scalable solution.

You can also configure a switch to autorecover error-disabled ports after a specified amount of time:

| Command | Description |
|---|---|
| `Switch(config)#errdisable recovery cause psecure-violation` | Enable dynamic error recovery of an error-disabled port. Default is 300 seconds. |
| `Switch(config)#errdisable recovery interval seconds` | Specify how long a port will remain disabled before it is reenabled. **TIP:** Disconnect the offending host; otherwise, the port will remain disabled, and the violation counter will be incremented. |

**NOTE:** Use the show errdisable recovery command to display the error-disabled recovery timer information.