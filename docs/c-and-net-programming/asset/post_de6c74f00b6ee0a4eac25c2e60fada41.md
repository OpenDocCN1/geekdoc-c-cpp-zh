
- 2. Peer Machine 4 does not have an entry for the PNRP ID of 6000 and does not have any entries that are closer to 6000. Peer Machine 4 sends a response back to Peer Machine 3 indicating that it could not find an entry closer to 6000.
- 3. Because 2500 is the next numerically closer PNRP ID to 6000, Peer Machine 3 sends a PNRP Request message to the node that registered the PNRP ID of 2500 (Peer Machine 1).
- 4. Because Peer Machine 1 has an entry in its cache for the PNRP ID of 6000, it sends the IPv6 address of Peer Machine 2 to Peer Machine 3.
- 5. Peer Machine 3 sends a PNRP Request to Peer Machine 2.
- 6. Peer Machine 2 sends a positive name resolution response back to Peer Machine 3.

![](img/3005a4307e6d8f3bb7e76eea28a92357_566_0.png)

Fig. 18.6.2 PNRP endpoint determination scenario flow

- After endpoint determination, Peer Machine 3 sends a PNRP name resolution request for the service with which Peer Machine 3 wants to establish communication to Peer Machine 2. Peer Machine 2 sends back a response that contains optional data about the service for the requesting application.

## 18.6.5 Registering and Unregistering a Peer Name

- To register on the network an unsecured Peer Name, a valid unsecured Peer Name and an IP address is to be provided. Optionally, the Cloud name (Global by default) can be mentioned and an additional comment or description associated with the resource can be supplied. This information is stored in the WSAQUERYSET data structure and passed to the WSASetService with the Register option.
- To unregister on the network an unsecured Peer Name, a valid unsecured Peer Name and optionally the Cloud name (Global by default) is required to be provided. This information is stored in the WSAQUERYSET data structure and passed to the WSASetService with the Delete option.

### PNRP Name Publication

- To publish a new PNRP ID, a peer performs the following :
  - Sends PNRP publication messages to its cache neighbors (the peers that have registered PNRP IDs in the lowest level of the cache) to seed their caches.
  - Chooses random nodes in the cloud that are not its neighbors and sends them PNRP name resolution requests for its own P2P ID. The resulting endpoint determination process seeds the caches of random nodes in the cloud with the PNRP ID of the publishing peer.
- PNRP version 2 nodes do not publish PNRP IDs if they are only resolving other P2P IDs. The HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\PeerNet\PNRP\IPv6-Global\SearchOnly=1 registry value (REG_DWORD type) allows you to specify that peers only use PNRP for name resolution, never for name publication. This registry value can also be configured through Group Policy.

## 18.6.6 Scaling Peer Name Resolution with a Multi-Level Cache

- To keep the sizes of the PNRP caches small, peer nodes use a multi-level cache, in which each level contains a maximum number of entries. Each level in the cache represents a one tenth smaller portion of the PNRP ID number space (2^256). The lowest level in the cache contains a locally registered PNRP ID and other PNRP IDs that are numerically close to it. As a level of the cache is filled with a maximum of 20 entries, a new lower level is created.
- The maximum number of levels in the cache is on the order of log10 (Total number of PNRP IDs in the cloud). For example, for a global cloud with 100 million PNRP IDs, there are no more than 8 (=log10(100,000,000)) levels in the cache and a similar number of hops to resolve a PNRP ID during name resolution. This mechanism allows for a distributed hash table for which an arbitrary PNRP ID can be resolved by forwarding PNRP Request messages to the next-closest peer until the peer with the corresponding CPA is found. The result of this multi-level caching scheme is that each peer does not have to store a large amount of cache entries. Even for a large number of PNRP IDs, the local storage and network traffic to resolve an arbitrary PNRP ID is not substantial.

- To ensure that resolution can complete, each time a node adds an entry to the lowest level of its cache, it floods a copy of the entry to all the nodes within the last level of the cache. The cache entries are refreshed over time. Cache entries that are stale are removed from the cache. The result is that the distributed hash table of PNRP IDs is based on active endpoints, unlike DNS in which address records and the DNS protocol provide no guarantee that the node associated with the address is actively on the network.

### PNRP Cache Initialization

To initialize the PNRP cache when a peer node starts up, the node can use the following methods,

- 1. Persistent cache entries - Previous cache entries that were present when the node was shut down are loaded from hard disk storage.
- 2. PNRP seed nodes - PNRP allows administrators to specify the addresses or DNS names of PNRP seed nodes that contain CPAs for current participants in the cloud.
- 3. Simple Service Discovery Protocol - PNRP nodes are required to register themselves using the Universal Plug-and-Play (UPnP) Simple Service Discovery Protocol (SSDP). A node joining a cloud can use an SSDP Msearch message to locate nearby SSDP nodes.

## 18.7 Building P2P Application

### A Simple Peer to Peer Network Chat Application example

The simple WCF chat application discussed below uses netTcpPeerBinding. Using this binding, it is very easy to create a simple intranet chat application. TCP end point is used for the communication. Almost all the coding is encapsulated in,

- System.ServiceModel;
- System.ServiceModel.Channels;
- System.ServiceModel.PeerResolvers;

### 1. Chat Server

A chat server code is as below,

```csharp
<CODE>
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Text;
using System.Windows.Forms;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.PeerResolvers;

namespace ChatServer
{
    public partial class ChatServer : Form
    {
        private CustomPeerResolverService cprs;
        private ServiceHost host;

        public ChatServer()
        {
            InitializeComponent();
            btnStop.Enabled = false;
        }

        private void btnStart_Click(object sender, EventArgs e)
        {
            try
            {
                cprs = new CustomPeerResolverService();
                cprs.RefreshInterval = TimeSpan.FromSeconds(5);
                host = new ServiceHost(cprs);
                cprs.ControlShape = true;
                cprs.Open();
                host.Open(TimeSpan.FromDays(1000000));
                lblMessage.Text = "Server started successfully.";
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.ToString());
            }
        }
        finally
        {
btnStart.Enabled = false;
btnStop.Enabled = true;
}
}
private void btnStop_Click(object sender, EventArgs e)
{
try
{
cprs.Close();
host.Close();
lblMessage.Text = "Server stopped successfully.";
}
catch (Exception ex)
{
MessageBox.Show(ex.ToString());
}
finally
{
btnStart.Enabled = true;
btnStop.Enabled = false;
}
}
```
```

- **Explanation -** An object of CustomPeerResolverService class is created and passed as an input parameter to the ServiceHost class. Then peer resolver service is opened and host is started. The code is very simple and no new classes and no end points are required.

### 2. The Server's config file

The config file plays the most important role of specifying the required details as shown below,

```
<CODE>
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
system.serviceModel
services
service name="System.ServiceModel.PeerResolvers.
CustomPeerResolverService"
host
baseAddresses
add baseAddress="net.tcp://10.34.34.241/ChatServer"/
baseAddresses
```
