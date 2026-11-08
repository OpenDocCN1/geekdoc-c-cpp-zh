# ## Server-Based AAA Authentication

Server-based AAA authentication is a much more scalable solution that uses an external database server resource leveraging RADIUS or TACACS+ protocols.

Server-based AAA authentication lets you do the following:

+   - Create a TACACS+ or RADIUS AAA server group.
+   - Add a AAA server and parameters to the AAA server group.
+   - Configure server-based AAA authentication.

| Command | Description |
|---|---|
| `ciscoasa(config)# aaa-server server-tag protocol {tacacs+ \| radius}` | Create a TACACS+ or RADIUS AAA server group. **NOTE:** Other protocols include `http-form`, `kerberos`, `ldap`, `ntp`, and `sdi`. All are beyond the scope of this chapter. |
| `ciscoasa(config-aaa-server-group)# aaa-server server-tag (interface-name) host {server-ip \| name} [key]` | Identify a AAA server and parameters to be part of the AAA server group. |
| `ciscoasa(config)# aaa authentication {enable \| http \| ssh \| telnet} console server-tag [LOCAL]` | Enable server-based AAA authentication. |

> **NOTE:** To erase all AAA server configurations, use the `clear config aaa-server` command.

> **NOTE:** To view all user accounts, use the `show running-config aaa-server` command.

# ## Configuring AAA Server-Based Authentication Example Using the CLI

Figure 21-18 shows the network topology for the server-based AAA authentication example.

![](bbox=[0.091, 0.762, 0.931, 0.877])

**Figure 21-18** Server-Based AAA Authentication Topology