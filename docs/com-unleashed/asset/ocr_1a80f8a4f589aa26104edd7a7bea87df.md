**FIGURE 14.4**  
*Configuring Microsoft Proxy Server with regedit.*

![](bbox=[0.241, 0.111, 0.533, 0.206])

# Firewall Configuration

The only configuration requirement placed by CIS on the firewall is that it allows TCP/IP traffic through port 80 unimpeded. Because port 80 is usually open to HTTP traffic, this is the standard scenario. In some rare cases, however, a firewall performs so-called application-level filtering on incoming traffic that might result in CIS traffic being rejected.

# Configuration Tips and Known Issues

There are a few things that can go wrong when you configure CIS. I've found a number of them that are documented in TechNet.

# Incorrect Proxy Server Settings on the CIS Client

The proxy server setting on the client should not contain any leading forward slash (/). For example, the reference myproxy:80 is correct but http://myproxy is not. Note that the proxy server setting (set using Internet in the Control Panel) is stored in the registry as the value of the

```
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\
ProxyServer
```

> **Caution**
> 
> CIS server side should not be installed on a machine hosting Microsoft Proxy Server because of the port control conflicts.

The RPC proxy, RpcProxy.dll, does not function properly when installed on a machine hosting Microsoft Proxy Server.