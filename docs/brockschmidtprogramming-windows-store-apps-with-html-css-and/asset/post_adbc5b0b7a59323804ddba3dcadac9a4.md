
capability rather than those related to the Internet.

**Note** The *Private Networks* capability isn't necessary when you'll be using the File Picker (see Chapter 11) to allow users to browse local networks. It's necessary only if you're needing to make direct programmatic connections to such resources.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_160_0.png)

**FIGURE 4-1** Additional network capabilities in the manifest.

### Sidebar: Localhost Loopback

Regardless of the capabilities declared in the manifest, local loopback—that is, using http://localhost URIs—is blocked for Windows Store apps. An exception is made for machines on which a developer license has been installed, as described in “Sidebar: Using the Localhost” in the “Background Transfer” section of this chapter (we'll need to use it with a sample there). This exception exists only to simplify debugging apps and services together on the same machine during development. You can disable this allowance in Visual Studio through the Project > Property Pages dialog under Debugging > Allow Local Network Loopback, which helps you test your app as a consumer would experience it.

## Network Information (the Network Object Roster)

Regardless of the network involved, everything you want to know about that network is available through the `Connectivity.NetworkInformation` object. Besides a single `networkstatuschanged` event that we'll discuss in “Connectivity Events” a little later, the interface of this object is made up of methods to retrieve more specific details in other objects.

Below is the roster of the methods in `NetworkInformation` and the contents of the objects obtained through them. You can exercise the most common of these APIs through the indicated scenarios of the Network information sample:

- `getInternetConnectionProfile` (Scenario 1) Returns a single `ConnectionProfile` object for the currently active Internet connection. If there is more than one connection, this method returns the preferred profile that’s most likely to be used for Internet traffic.
- `getConnectionProfiles` (Scenario 3) Returns a vector of `ConnectionProfile` objects, one for each connection, among which will be the active Internet connection as returned by `getInternetConnectionProfile`. Also included are any wireless connections you’ve made in the past for which you indicated Connect Automatically. (In this way the sample will show you some details of where you’ve been recently.) See the next section for more on `ConnectionProfile`.
- `findConnectionProfilesAsync` (Scenario 6) Given a `ConnectionProfileFilter` object, returns a vector of `ConnectionProfile` objects that match the filter criteria. This helps you find available networks that are suitable for specific app scenarios such as finding a Wi-Fi connection or one with a specific cost policy.
- `getHostNames` Returns a vector (see note below) of `HostName` objects, one for each connection, that provides various name strings (`displayName`, `canonicalName`, and `rawName`), the name’s type (from `HostNameType`, with values of `domainName`, `ipv4`, `ipv6`, and `bluetooth`), and an `ipInformation` property (of type `IPInformation`) containing `prefixLength` and `networkAdapter` properties for IPv4 and IPv6 hosts. (The latter is a `NetworkAdapter` object with various low-level details.) The `HostName` class is used in various networking APIs to identify a server or some other endpoint.
- `getLanIdentifiers` (Scenario 4) Returns a vector of `LanIdentifier` objects, each of which contains an `infrastructureId` (`LanIdentifierData` containing a type and value), a `networkAdapterId` (a GUID), and a `portId` (`LanIdentifierData`).
- `getProxyConfigurationAsync` Returns a `ProxyConfiguration` object for a given URI and the current user. The properties of this object are `canConnectDirectly` (a Boolean) and `proxyUris` (a vector of `Windows.Foundation.Uri` objects for the configuration).
- `getSortedEndpointPairs` Sorts an array of `EndpointPair` objects according to `HostNameSortOptions`. An `EndpointPair` contains a host and service name for local and remote endpoints, typically obtained when you set up specific connections like sockets. The two sort options are `none` and `optimizeForLongConnections`, which vary connection behaviors based on whether the app is making short or long duration connection. See the documentation for `EndpointPair` and `HostNameSortOptions` for more details.

**What is a vector?** A **vector** is a WinRT type that’s often used for managing a list or collection. It has methods like `append`, `removeAt`, and `clear` through which you can manage the list. Other methods like `getAt` and `getMany` allow retrieval of items, and a vector supports the `[ ]` operator like an array. For more details, see “Windows.Foundation.Collections Types” in Chapter 6, “Data Binding, Templates, and Collections.” In its simplest use, you can treat a vector like a JavaScript array through the `[ ]` operator.

## The ConnectionProfile Object

Of all the information available through the `NetworkInformation` object, the most important for apps is found in `ConnectionProfile`, most frequently that returned by `getInternetConnectionProfile` because that's the one through which an app's Internet traffic will flow. The profile is what contains all the information you need to make decisions about how you're using the network, especially for cost awareness. It's also what you'll typically check when there's a change in network status. Scenarios 1 and 3 of the Network information sample retrieve and display most of these details.

Each profile has a `profileName` property (a string), such as "Ethernet" or the SSID of your wireless access point, a `serviceProviderGuid` property (the network operator ID), plus a `getNetworkNames` method that returns a vector of friendly names for the endpoint. The `networkAdapter` property contains a `NetworkAdapter` object for low-level details, should you want them, and the `networkSecuritySettings` property contains a `NetworkSecuritySettings` object describing authentication and encryption types.

More generally interesting is the `getNetworkConnectivityLevel` method, which returns a value from the `NetworkConnectivityLevel` enumeration: none (no connectivity), localAccess (the level you hate to see when you're trying to get a good connection!), constrainedInternetAccess (captive portal connectivity, typically requiring further credentials as is often encountered in hotels, airports, etc.), and internetAccess (the state you're almost always trying to achieve). The connectivity level is often a factor in your app logic and something you typically watch with network status changes. Related to this is the `getDomainConnectivityLevel` that provides a `DomainConnectivityLevel` value of none (no domain controller), unauthenticated (user has not been authenticated by the domain controller), and authenticated.

To check if a connection is on Wi-Fi, check the `isWlanConnectionProfile` flag and, if it's true, you can look at the `wlanConnectionProfileDetails` property for more details, such as the SSID. If you're on a mobile connection, on the other hand, the `isWwanConnectionProfile` flag will be true, in which case the `wwanConnectionProfileDetails` property tells you about the type of data service and registration state of the connection. And if for either of these you want to display the connection's strength, the `getSignalBars` method will give you back a value from 0 to 5.

The ups and downs of a connection's lifetime is retrieved through `getConnectivityIntervalsAsync`, which produces a vector of `ConnectivityInterval` objects. Each one describes when this network was connected and how long it remained so.

To track the inbound and outbound traffic on a connection, the `getNetworkUsageAsync` method returns a `NetworkUsage` object that contains `bytesReceived`, `bytesSent`, and `connectionDuration` properties for a given time period and `NetworkUsageStates` (roaming or shared). Similarly, the `getConnectionCost` and `getDataPlanStatus` provide the information an app needs to be aware of how much network traffic is happening and how much it might cost the user. We'll come back to this in "Cost Awareness" shortly, including how to see per-app usage in Task Manager.
