# ## AAA Accounting

Cisco Secure ACS serves as a central repository for accounting information, essentially tracking events that occur on the network. This stored information can prove very helpful for management, security audits, capacity planning, and network-usage billing.

Method lists for accounting define the way accounting will be performed and the sequence in which these methods are performed. AAA supports six different types of accounting: network, connection, exec, system, command, and resource.

```
```
Router(config)# aaa accounting {system
| network | exec | commands level} {default
| list-name} {start-stop | wait-start |
stop-only | none} [method1 [method2]]
```
```

Define the accounting method to use for a specific service. It keeps track of requested services for billing or security purposes.

+   - **system** tracks system-level events such as reloads.
+   - **network** tracks network-related service requests such as PPP.
+   - **exec** tracks EXEC shell sessions.
+   - **commands** tracks all commands at the specified privilege level.

# ### Configuring AAA Accounting Example

```
```
R1(config)#aaa accounting exec default
start-stop group tacacs+
```
```

The router sends a start accounting notice at the beginning of the requested event and a stop accounting notice at the end of the event.

# ## Cisco Secure ACS

Cisco Secure Access Control Server (ACS) 5.3 for Windows provides a centralized identity networking solution and simplified user management experience across all Cisco devices and security management applications.

Before Cisco Secure ACS Version 5, users were made part of a group and used group-based policies. Since ACSv5, rule-based policies are implemented, providing a flexible approach that can match a variety of access conditions.

In Cisco Secure ACS, you can define network device groups (NDG), which are sets of devices. These NDGs provide logical grouping of devices, for example, by device location or type, which you can use in policy conditions.