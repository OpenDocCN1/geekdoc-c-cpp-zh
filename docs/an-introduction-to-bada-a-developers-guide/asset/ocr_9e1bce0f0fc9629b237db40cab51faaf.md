> Note: Push messages are not supported by version 1.0.0b3 of the bada SDK, which is the current version at the time of writing.

```
Osp::Net
```

# Declared In:

FNet.h

# Library:

FNet

# Privileges Required:

You will need at least one of the privilege groups listed below to use the features of this namespace and possibly more, depending on what features you’re using:

| Privilege group | Privilege level | Description |
|---|---|---|
| NET | NORMAL | Manipulating netaccount information |
| NET_STATISTICS | NORMAL | Accessing information on a data call |
| NET_ACCOUNT | SYSTEM | Creating and deleting net accounts |

# Prerequisites:

You may need to use a proxy server if you are behind a firewall.

# Summary

Selected important classes:

+   - NetAccountInfo
+   - NetAccountManager
+   - NetConnection

This namespace is responsible for accessing the data communications capabilities of bada. It contains classes for establishing, maintaining, and monitoring the connections required to send and receive data over a network. It also provides methods to retrieve information about a specific host using the internet Domain Name System (DNS). Sub-namespaces are provided for managing Wi-Fi and Bluetooth connections, and sending and receiving data using HTTP or low-level socket functions.