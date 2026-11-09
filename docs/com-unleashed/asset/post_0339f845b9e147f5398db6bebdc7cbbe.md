
You can close Internet Service Manager now. At a command prompt, stop and restart the Internet Information Server with the following commands:

```text
net stop iisadmin

net start w3svc
```

Enable CIS on the server as described later in this chapter in the section “Enabling CIS.”

> **Note**
>
> In previous versions of IIS, you could stop the entire Web service by typing at the command line `net stop w3svc`. This would terminate all the Web services on the computer, and shut down the `inetinfo.exe` process. As a result of the new multiple-Web-site architecture, there is another service, `iisadmin`, that keeps running, even when W3SVC is shut down. The same is true for starting and stopping services from Control Panel. If you truly want to unload the `inetinfo.exe` process and make sure that all the extensions are unloaded properly, you should now type `net stop iisadmin`, rather than `net stop w3svc`. Typing `net start w3svc` or `net start msftpsvc` automatically starts `iisadmin`.

## Configuring the RPC Proxy on Windows 2000 Server

On the Windows 2000 Server, CIS requires that the Internet Information Services (including the Internet Services Manager) be running.

On Windows 2000 Server, CIS has its own optional network setup (it is not installed by default). It can be installed just like other optional network components.

From the Control Panel, select Add/Remove Programs, click Add/Remove Windows Components, and then click the Components button. This will start the Windows Components Wizard. From the wizard, complete the following:

- 1. Select Networking Services, and click the Details button.
- 2. Select the COM Internet Services Proxy check box.

You can add CIS during the initial Windows 2000 Server install, or add it later to an existing system. On an upgrade from a Windows NT 4.0 (SP4) Server that already has CIS installed to Windows 2000, you will need to reinstall CIS as described previously.

## Enabling CIS

To enable CIS on the server, you need to add the Tunneling TCP protocol to the DCOM protocol list. You do this by running the DCOMCNFG from the Windows\System directory (using either a command prompt or the run box), and then follow the next steps:

- 1. Select the Default Protocols tab.
- 2. Use the Add button to add Tunneling TCP/IP.
- 3. Reboot the system to have this change take effect.

In addition, it is possible to control whether CIS is enabled by changing the value of a DCOM property. This setting, which defaults to disabled, can act as a coarse-grained security control to disable potential Internet access to DCOM. Note, however, that even when CIS is enabled, the usual DCOM security checks remain in effect. Run DCOMCNFG to set this property by implementing these steps:

- 1. Select the Default Properties tab.
- 2. Select or unselect the Enable COM Internet Services on this computer check box.
- 3. Reboot the system for the change to take effect.

## Proxy Server Configuration

If the client is configured to access the Internet through a proxy, the proxy server must be configured to enable the HTTP CONNECT method for the port to which the client connects (port 80 by default). This port configuration is sometimes referred to as “enabling SSL tunneling.” Consult the documentation for your proxy server for details on how to configure a port for the HTTP CONNECT method.

### Configuring Microsoft Proxy Server

If you are using Microsoft Proxy Server, enabling HTTP CONNECT is achieved by manipulating a registry key (for example, using regedt32.exe) to indicate what ports should allow HTTP CONNECT. In the default configuration, two ports are enabled: 443 (https) and 563 (snews). The registry key of interest is

```
HKEY_LOCAL_MACHINE\system\CurrentControlSet\services\w3proxy\parameters\SSLPortListMembers
```

The key value consists of a list of pairs of ports. For the default proxy configuration (handling HTTP traffic on port 80), add the pair 80 80 to the existing registry values. After making this modification, you will need to stop and restart the Microsoft Proxy Server for the new settings to take effect. You can view the Microsoft Proxy Server in Figure 14.4.

**FIGURE 14.4**  
*Configuring Microsoft Proxy Server with regedt32.*

![](img/112c2326f49d26b8d59aa054e14c5747_390_0.png)

## Firewall Configuration

The only configuration requirement placed by CIS on the firewall is that it allows TCP/IP traffic through port 80 unimpeded. Because port 80 is usually open to HTTP traffic, this is the standard scenario. In some rare cases, however, a firewall performs so-called application-level filtering on incoming traffic that might result in CIS traffic being rejected.

## Configuration Tips and Known Issues

There are a few things that can go wrong when you configure CIS. I've found a number of them that are documented in TechNet.

### Incorrect Proxy Server Settings on the CIS Client

The proxy server setting on the client should not contain any leading forward slash (/). For example, the reference myproxy:80 is correct but http://myproxy is not. Note that the proxy server setting (set using Internet in the Control Panel) is stored in the registry as the value of the

```
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ProxyServer
```

> **Caution**
>
> CIS server side should not be installed on a machine hosting Microsoft Proxy Server because of the port control conflicts.

The RPC proxy, RpcProxy.dll, does not function properly when installed on a machine hosting Microsoft Proxy Server.

### Issue with a Multihomed CIS Server

A client of a multihomed CIS server activating an object using one of the server IP addresses can cause failure. To work around this limitation, the client should use the server name (for example, the DNS name). For example, instead of 209.42.234.81, use www.sourceDNA.com.

### MTS Use of Callbacks

When a client and a server share a transaction in a Microsoft Transaction Server (MTS) scenario, the MTS infrastructure makes a callback to the client. This scenario is not supported with CIS unless the client machine is configured as a CIS server. Note, however, that this limitation does not hinder the most common transaction scenario for a base client, the case of a client not in a transaction calling a component that requires one.

### Issue with HTTP Caching Devices

HTTP caching devices (for example, Cisco LocalDirector) might need to be tweaked or disabled.

Intelligent routers such as Cisco’s LocalDirector allow a group of servers to appear as a single virtual server. The IP address of the virtual server is registered with the DNS server, whereas the IP addresses of the servers themselves remain unpublished. When the virtual server receives incoming requests, the router distributes the requests to one of them. The entire group of servers thus appears to the client as a single server.

When Cisco’s LocalDirector is used in combination with IIS for session-aware load-balancing in a Web farm, it is important to make sure that the interval for the router matches or exceeds the timeout interval for the session object. By default, the Session object timeout is set to 20 minutes. The timeout interval can be changed to 15 minutes by adding the following line to the Global.asa file:

```
<% Session.Timeout = 15 %>
```

### Registry Keys Affecting CIS

The information in Table 14.2 shows you the registry keys that affect CIS.

**Table 14.2 — Registry Keys that Affect CIS Operation**

| Registry Key | Description |
|---|---|
| `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ProxyServer` | The value of this client-side setting indicates the `<proxy server>:<port>` that CIS uses. `<proxy server>` should not contain leading forward slashes (`/`). Note that this configuration is shared with the RPC runtime environment by other applications that use HTTP, such as Internet Explorer. Proxy Server configuration can also be set in the Control Panel by opening the Internet icon. |
