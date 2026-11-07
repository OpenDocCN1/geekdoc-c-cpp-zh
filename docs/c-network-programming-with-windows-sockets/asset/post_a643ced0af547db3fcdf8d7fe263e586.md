
![](img/5e551abe6e0cb0588043ee757a235ddb_0_0.png)

## Introduction to Networking

- 1. Networking and Network Programming
- 2. TCP/IP Overview
- 3. WinSock Overview
- 4. Visual C++

## 1

![](img/5e551abe6e0cb0588043ee757a235ddb_1_0.png)

## Networking and Network Programming

The purpose of this book is to show you how to make network-aware applications that run on the Microsoft Windows and Windows NT operating systems using the Windows Sockets (WinSock) Application Programming Interface (API). To that end, several practical examples are examined that utilize the basic functionality of WinSock.

Network operating systems, such as Windows for Workgroups and Windows NT, provide basic file and printer sharing services. This most basic level of functionality is provided “out of the box.” Network-aware applications are programs that use the capabilities of a collection of connected computers. Network-aware programs range from custom applications that transfer data among computers on a network to mainstream applications that enable electronic mail and remote database access. The WinSock API is a library of functions that a programmer can use to build these network-aware applications. WinSock has its roots in Berkeley sockets as introduced in the Berkeley Software Distribution of UNIX. WinSock uses the TCP/IP (Transmission Control Protocol/Internet Protocol) suite, which provides the formal rules of behavior that govern network communications between all computers running this particular computer networking protocol.

Before I begin the examination of network programming, look at the basics of computer networking in general. A network can be loosely defined as a collection of two or more computers that have some sort of communication path between them. A network can be loosely classified as either a local area network (LAN) or wide-area network (WAN). The use of the terms *LAN* and *WAN* is somewhat misleading because which term you use is relative to the particular network installation you’re describing. Generally speaking, a LAN covers a much more geographically restricted area than does a WAN. Whereas a LAN may connect computers within an office building, a WAN may connect computers spread across the country. With the advances in networking hardware and software, many widely dispersed LANs can now be connected to form a much larger homogeneous WAN. Devices known as *bridges* and *routers* allow for this connection of disparate LANs. Computer networks aren’t new, but they weren’t accepted in the personal computer realm until perhaps the late 1980s, when computer firms began offering cost-effective and reliable networking for the desktop PC. At that time, the primary goal of the PC network was to provide a central repository for files and to allow printers to be shared among many users. It hasn’t been until relatively recently that businesses have realized the true potential of a PC network.

### Goals of Networking

The goals of PC networking have been expanding over the last few years—from simple file and printer sharing to access of fax machines, modems, and enterprise-wide electronic mail systems. All the while, the essential goals of networking have always been to share resources and to provide a medium for communications.

### Resource Sharing

For the sake of this discussion, a network resource is either a device or a capability on the network that’s available for use by network users. The computer that the network resources are attached to is called the server. The other computers that access those resources over the network are called clients. The typical PC network user today takes shared file and printer access for granted. But there are now other resources that also can be made available to the user. Among them are fax machines, modems, compute servers, and database servers.

### Files

The traditional use of PC networks has been and probably always will be to act as a repository for files. By storing files in a common location accessible to coworkers, for example, much productivity can be gained. Several products exist from Microsoft and other vendors that provide this capability. Windows for Workgroups is one such product. It’s classified as a peer-to-peer network, which means that there’s no dedicated, central-file server. Instead, any computer on the network can share files with any other; any computer on the network can act as either a client, server, or both. Windows NT and Windows NT Advanced Server expand on this idea by providing a much more robust file-sharing capability and better file system security.

Figure 1.1 shows two computers labeled Computer A and Computer B. Each has access to files on the File and Print Server and stored on the computer server. To illustrate the difference between the central-file server model and the peer-to-peer model, examine the following scenario, where Computer A has a file on its hard disk that it would like to make available to Computer B. In the central-file server model, Computer A must connect to the File and Print Server, place the file on the server’s hard disk, and then inform Computer B that the file is available. Computer B then connects to the File and Print Server and accesses the file deposited there by Computer A. Using a peer-to-peer network, Computer A could simply give Computer B permission to access the file on Computer A’s hard disk.

**FIGURE 1.1.**  
*File and printer resource sharing.*

![](img/5e551abe6e0cb0588043ee757a235ddb_4_0.png)

At a minimum, a computer network with a file server, whether it be centralized or peer-to-peer, prevents the use of the infamous “sneaker net” whereby files are transferred between computer users by first putting the desired files onto a floppy disk and then walking that floppy over to the designated recipient.

### Printers

Another popular use of PC networks is to make printers available to all network users. This obviously provides a great cost savings by reducing the number of expensive printers and the cost of maintenance and management of those devices. Windows for Workgroups and Windows NT provide printer-sharing capabilities. As Figure 1.1 shows, the two computers labeled Computer A and Computer B, as well as the File and Print Server computer, have access to the laser printer attached to the File and Print Server. When the user seated at Computer A prints a document, it’s sent to the File and Print Server where it’s printed. If a user at Computer B tries to print a document while Computer A’s document is still printing, Computer B’s document is stored in a temporary location on the File and Print Server. This process is called printer spooling. As soon as the first submitted print job belonging to Computer A’s user is complete, the next job, belonging to Computer B’s user, is begun.

A Windows NT-based network fully supports the remote management of networked printers. An administrator of a Windows NT network can monitor the status (to see if the paper is out, for example) of a remotely located printer and also manipulate the queue of jobs waiting to be printed. He could, for instance, pause a print job sent by a user at 1:00 to make a print job submitted at 1:05 print first. The administrator can control other printer options such as which hours of the day the printer is available, who on the network can access the printer, and which users' print jobs have higher priority than others.

### Fax Machines

The fax “machines” that are now being attached to computer networks are really just specialized modems that can communicate with other fax “modems” and more traditional stand-alone fax machines. There are several benefits to networked fax modems. Most documents that are eventually faxed are created with a computer’s word processing program, printed on a traditional laser or dot-matrix printer, and then fed into a traditional fax machine. The networked fax modem saves these last two time-consuming steps by allowing the word processing program to “print” directly to the fax device. Most fax modems appear as just another printer to the word processing program. When the user selects the fax modem as the “printer” to print to, the user is asked to fill out a fax cover sheet which includes the recipient’s name and the telephone number of the recipient’s fax machine. A fax modem also allows a fax to be easily distributed to multiple recipients at different telephone numbers.

Microsoft at Work fax software is a component of the Microsoft at Work architecture (to be discussed shortly). This software allows networked computers running Windows to share a fax modem attached to one of the networked computers.

### Modems

Standard modems, as opposed to fax modems, are also being used now as shared devices on PC networks. In the past, users who had a regular need for modem communications had to have their own personal modems. More often than not, that modem was very underutilized. By arranging several modems in a modem pool reachable by a network, many more users can have access to modem communications without the expense of personal modems. When users need to access a modem, they request one from the modem pool and then proceed as if that modem were theirs alone. When they’re finished with the modem resources, those resources are freed and made available to the next user who requests them. Figure 1.2 shows four computers and a two-modem pool. The Modem Pool Server is the computer that manages the modem pool. Computers A, B, and C have access to these modems. When Computer A requests the use of a modem, the Server removes that modem from its availability list. When Computer B requests a modem, the Server assigns the second modem to Computer B. If Computer C then requests a modem, the request is placed in a queue. As soon as Computer A or B relinquishes its “borrowed” resource, Computer C gets use of that freed modem.
