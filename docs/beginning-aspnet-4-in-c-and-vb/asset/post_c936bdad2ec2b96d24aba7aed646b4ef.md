
## 45
## Peer-to-Peer Networking
### WHAT'S IN THIS CHAPTER?
- ► An overview of P2P
- ► The Microsoft Windows Peer-to-Peer Networking platform, including PNRP and PNM
- ► Building P2P applications with the .NET Framework

Peer-to-peer networking, often referred to as P2P, is perhaps one of the most useful and yet misunderstood technologies to emerge in recent years. When people think of P2P they usually think of one thing: sharing music files, often illegally. This is because file-sharing applications such as BitTorrent have risen in popularity at a staggering rate, and these applications use P2P technology to work.

Although P2P is used in file-sharing applications, that doesn’t mean it doesn’t have other applications. Indeed, as you see in this chapter, P2P can be used for a vast array of applications, and is becoming more and more important in the interconnected world in which we live. You learn about this in the first part of this chapter, when you look at an overview of P2P technologies.

Microsoft has not been oblivious to the emergence of P2P, and has been developing its own tools and technologies to use it. You can use the Microsoft Windows Peer-to-Peer Networking platform as a communication framework for P2P applications. This platform includes the important components Peer Name Resolution Protocol (PNRP) and People Near Me (PNM). Also, version 3.5 of the .NET Framework introduced a new namespace, System.Net.PeerToPeer, and several new types and features that you can use to build P2P applications yourself with minimal effort.

## PEER-TO-PEER NETWORKING OVERVIEW

Peer-to-peer networking is an alternative approach to network communication. To understand how P2P differs from the “standard” approach to network communication it is helpful to take a step backward and look at client-server communications. Client-server communications are ubiquitous in networked applications today.

You could use P2P technology to prevent this web server collapse. Instead of sending the file directly from the server to all the clients, you send the file to just a few clients. A few of the remaining clients then download the file from the clients that already have it, a few more clients download it from those second-level clients, and so on. In fact, this process is made even faster by splitting the file into chunks and dividing these chunks among clients, some of whom download it directly from the server, and some who download chunks from other clients. This is how file-sharing technologies such as BitTorrent work, and is illustrated in Figure 45-3.

![](img/d7d2ffa0a76feaab821930e95daace93_1402_0.png)

FIGURE 45-3

### P2P Architectural Challenges

There are still problems to solve in the file-sharing architecture discussed here. For a start, how do clients detect that other clients exist, and how do they locate chunks of the file that other clients might have? Also, how can you ensure optimal communication between clients that may be separated by entire continents?

Every client participating in a P2P network application must be able to perform the following operations to overcome these problems:

- It must be able to *discover* other clients.
- It must be able to *connect* to other clients.
- It must be able to *communicate* with other clients.

The discovery problem has two obvious solutions. You can either keep a list of the clients on the server so clients can obtain this list and contact other clients (known as *peers*), or you can use an infrastructure (for example PNRP, covered in the next section) that enables clients to find each other directly. Most file-sharing

- Multi-user communication applications that allow users to communicate and exchange data directly rather than through a server
- Distributed processing applications, as an alternative to supercomputing applications that process enormous amounts of data
- Web 2.0 applications that combine some or all the above in dynamic, next-generation web applications

## MICROSOFT WINDOWS PEER-TO-PEER NETWORKING

The Microsoft Windows Peer-to-Peer Networking platform is Microsoft's implementation of P2P technology. It is part of Windows XP SP2, Windows Vista, and Windows 7, and is also available as an add-on for Windows XP SP1. It includes two technologies that you can use when creating .NET P2P applications:

- The Peer Name Resolution Protocol (PNRP), which is used to publish and resolve peer addresses
- The People Near Me server, which is used to locate local peers (currently for Vista and Windows 7 only)

In this section you learn about these technologies.

### Peer Name Resolution Protocol (PNRP)

You can of course use any protocol at your disposal to implement a P2P application, but if you are working in a Microsoft Windows environment (and, let's face it, if you're reading this book you probably are) it makes sense to at least consider PNRP. There have been two versions of PNRP released to date. PNRP version 1 was included in Windows XP SP2, Windows XP Professional x64 Edition, and Windows XP SP1 with the Advanced Networking Pack for Windows XP. PNRP version 2 was released with Windows Vista, and was made available to Windows XP SP2 users through a separate download (see KB920342 at support.microsoft.com/kb/920342). Windows 7 also uses version 2. Version 1 and version 2 of PNRP are not compatible, and this chapter covers only version 2.

In itself, PNRP doesn't give you everything you need to create a P2P application. Rather, it is one of the underlying technologies that you use to resolve peer addresses. PNRP enables a client to register an endpoint (known as a peer name) that is automatically circulated among peers in a cloud. This peer name is encapsulated in a PNRP ID. A peer that discovers the PNRP ID is able to use PNRP to resolve it to the actual peer name, and can then communicate directly with the associated client.

For example, you might define a peer name that represents a WCF service endpoint. You could use PNRP to register this peer name in a cloud as a PNRP ID. A peer running a suitable client application that uses a discovery mechanism that can identify peer names for the service you are exposing might then discover this PNRP ID. Once discovered, the peer would use PNRP to locate the endpoint of the WCF service and then use that service.

![](img/d7d2ffa0a76feaab821930e95daace93_1404_0.png)

> *In past releases of PNRP there was a third type of cloud, site local. This is no longer used and is not covered in this chapter.*

You can discover what clouds you are connected to with the following command:

```
netsh p2p pnrp cloud show list
```

A typical result is shown in Figure 45-5.

![](img/d7d2ffa0a76feaab821930e95daace93_1406_0.png)

**FIGURE 45-5**

Figure 45-5 shows that a single cloud is available, and that it is a link local cloud. You can tell this from both the name and the scope value, which is 3 for link local clouds and 1 for global clouds. To connect to a global cloud you must have a global IPv6 address. The computer used to generate Figure 45-5 does not have one, which is why only a local cloud is available.

Clouds may be in one of the following states:

- **Active** — If the state of a cloud is active, you can use it to publish and resolve peer names.
- **Alone** — If the peer you are querying the cloud from is not connected to any other peers, it will have a state of alone.
- **No Net** — If the peer is not connected to a network, the cloud state may change from active to no net.
- **Synchronizing** — Clouds will be in the synchronizing state when the peer is connecting to them. This state will change to another state extremely quickly because this connection does not take long, so you will probably never see a cloud in this state.
- **Virtual** — The PNRP service connects to clouds only as required by peer name registration and resolution. If a cloud connection has been inactive for more than 15 minutes it may enter the virtual state.

### PNRP in Windows 7

With Windows 7, PNRP makes use of a new component called the Distributed Routing Table (DRT). This component is responsible for determining the structure of the keys used by PNRP, the default implementation of which is the PNRP ID previously described. By using the DRT API it is possible to define an
