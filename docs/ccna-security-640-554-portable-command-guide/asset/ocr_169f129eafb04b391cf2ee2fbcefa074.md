Alternatively, Telnet can be configured to use authentication, authorization, and accounting (AAA) authentication:

| Command | Description |
|---|---|
| `ciscoasa(config)# username name password`<br>`password` | Create a local database entry. |
| `ciscoasa(config)# aaa authentication`<br>`telnet console LOCAL` | Configure Telnet to refer to the local database for authentication. |

Secure Shell (SSH) is also supported, but it requires AAA authentication to be enabled. Use the following commands to enable SSH support:

| Command | Description |
|---|---|
| `ciscoasa(config)# aaa authentication`<br>`ssh console LOCAL` | Configure SSH to refer to the local database for authentication. |
| **NOTE:** The `LOCAL` keyword is case sensitive and is a predefined server tag. | |
| `ciscoasa(config)# crypto key`<br>`generate rsa modulus modulus` | Generates the RSA key required for SSH encryption. |
| **NOTE:** Valid modulus values include 512, 768, 1024, and 2048. Higher modulus values are recommended. | |
| `ciscoasa(config)# ssh ip-address`<br>`subnet-mask interface-name` | Identify which inside hosts can SSH to which ASA interface. |
| `ciscoasa(config)# ssh timeout minutes` | Alters the default exec timeout of 5 minutes. |

**NOTE:** To verify the SSH configuration, use the `show ssh` command.

Enable HTTPS services on the ASA:

| Command | Description |
|---|---|
| `ciscoasa(config)# http server`<br>`enable` | Enable the ASA HTTP server. |
| `ciscoasa(config)# http ip-address`<br>`network-mask interface-name` | Identify a host or hosts that can access the ASA HTTP server using ASDM. |

**NOTE:** To remove and disable the ASA HTTP server service, use the `clear configure http` global configuration command.