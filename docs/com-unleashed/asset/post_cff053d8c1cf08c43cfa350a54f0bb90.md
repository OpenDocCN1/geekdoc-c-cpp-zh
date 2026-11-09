
and technologies within the DNA framework. Again, DNA is not a specification, and this illustration is only a representation of DNA in the eyes of the author. There is no one key required ingredient to make your application DNA-compliant. This figure does, however, suggest an arrangement that is typical of the DNA framework as touted by Microsoft.

> **Tip**
>
> If you are familiar with the three-tiered architecture model, you will notice its pattern in the following discussion. If you are not, you needn't worry because Chapter 2 covers it in depth.

**FIGURE 1.1**
*The Windows DNA services.*

![](img/112c2326f49d26b8d59aa054e14c5747_34_0.png)

## The Windows DNA Services: COM and COM+

In order to make DNA work, there must be support from the operating system kernel. An authoring service must be present at all times to interpret and oversee communication protocols and component synergy. This is where COM/DCOM/COM+ (and the Service Control Manager, for that matter) come into the DNA picture as the Distributed Operating Environment (see Figure 1.1).

COM encompasses all the services shown in the first column on the far right side of Figure 1.1; COM+ encompasses the services in the second column. The COM+ library within the operating system provides the necessary glue, or plumbing services, between components that enables them to communicate and operate in a standard way. The services provided by the COM library are interoperability, location transparency, security, networking, and base services. Each is discussed in detail next. COM+ adds queued components, load balancing, in-memory database, and event service. The following two items compose the Distributed Operating Environment:

- **Interoperability**—For component technology to work, a consistent process of binary capability discovery must exist. Components should be able to query other components and, through a process of elimination, find whether requested behavior exists. COM provides access to this process via the QueryInterface mechanism of the IUnknown interface present in all components.
- **Location Transparency**—In a distributed environment like DNA, a component should not be aware of its physical location. Also, it should not have to hard-code the physical location of other components it wants to use. Of course, someone must know where components live. In COM this is the Windows Registry. The Registry enables DNA applications to execute as if they were in their own local environment even though they can really be spread out all over the Internet.

### Security

Security is not to be taken lightly when working with DNA. Real exposure and threats exist when distributing a system over an intranet, or worse, the Internet.

Security can be divided into two main parts: client and server. For a client, there is the threat of executing downloaded binary images, components or otherwise, which expose the machine to viruses, Trojan horses, or blatant loss of data. These threats can be mitigated with the use of virus-detection software, certificate key technology, and a CA (Certificate Authority) to authenticate trusted sources. There is still no 100% guarantee of security because, even when certificates are authenticated, there is always a small chance of impersonation (a snooping entity claiming to be a trusted one, not to be confused with MTS Impersonation, which is discussed in later chapters).

For a typical enterprisewide DNA system, this is not normally a major concern because a physically isolated and firewalled intranet is used for the distributed environment, and any break-ins are likely to come from the inside (for which there is no known deterrent).

For a server, a security breach can have more profound consequences. A breach at the server level can create all kinds of problems including network-wide destruction of data and intellectual property theft. Windows NT Server provides government-approved, C2-level security at the kernel and file-system levels to help protect the server, but usually this is not enough. A middle network layer is required.

Between the client and server lie network security protocols like Secure Sockets Layer (SSL), TCP/IP firewalls, DCOM, or server-side, product-specific security (like MTS/MSMQ), depending on the communication medium.

DCOM security is discussed at length in Part III, “Component Management and Transactions” and TCP/IP flavors are beyond the scope of this book, but their documentation is widely available.

MSMQ and MTS also have powerful security systems, including encryption, which are covered in suggested parts of this book.

Despite all this security on the client and server, DNA applications are not immune to security breaches. No electronic system is infallible. Always have a contingency backup plan for your DNA system in case of electronic vandalism or theft. Nightly backups should always be performed, and spreading out tiers as physical machines will provide fault-tolerance. That is, one machine houses all presentation code, another machine serves application components, and a third machine houses all storage and Web servers.

> **Tip:**
>
> For the utmost top-secret, confidential electronic information, the only way to keep it secure is to keep the machine physically isolated: behind locked doors and off at work. Even so, always keep in mind that there is no such thing as impenetrable security. Given enough time and resources, all forms of security can be broken, hacked, cracked, or otherwise rendered useless. Keep your data safe.
>
> Fortunately, COM+ comes with a robust security model. Developers can easily take advantage of it without a lot of extra code.

### Networking

Networking is essential to a distributed system. In DNA, there are several high-level protocols you can use to network an application: COM+, DCOM, MSMQ, HTTP, and so on. All of them encapsulate the low-level layers of a network stack (like TCP/IP), which is very beneficial. The more encapsulation you can take advantage of, the more maintainable and reusable your DNA systems will be.

MSMQ, although not a network protocol, does enable applications to communicate with each other over a network. MSMQ can be configured to use any popular protocols like TCP/IP, but encapsulates all the protocol's communication details with a simple send/receive-style API. MSMQ is covered in detail in later sections of the book.

### Base Services

Other services required to make components work can be bundled in these categories—thread management, transactions, synchronization support, component registration, debugging, and so on.

We cannot take for granted the base COM services provided by the operating system. If all components had to carry code to understand the different threading models or participate in transaction contexts, the resulting component would be very bloated and slow. Furthermore, if components are hard-coded with base services like security, they would quickly become incompatible with other components in future security platforms.

The base services are essential for providing a backdrop in which components can be free to move about without concerns of networking or operating system implementation.

For example, the COM base services in a UNIX environment will certainly be implemented differently from those in NT or Windows 95. If a component is COM-compliant, it can interoperate across heterogeneous environments because the base services handle any compatibility issues. A component simply makes a call to a base service's API and lets the operating system do the rest.

The rest of this book focuses on these base services and how to take advantage of them.

### Queued Components

Imagine that an application invokes a COM object on a remote server. If that server is unreachable for whatever reason, there's a problem with the communication (or lack thereof). Does the client keep trying until the remote server comes online? Or does the client abort its process entirely? These questions have plagued DCOM developers.

The answer to the problem lies in one of the new COM+ runtime services, known as queued components. This service allows a client object to make calls to a remote object, even if it's not currently reachable. The calls are recorded by a system utility, transmitted to the server through asynchronous protocols, and played back by another system utility into the server-side COM object when the server machine becomes available.

This takes the headache out of talking to remote objects because developers don't have to worry about their current state. If they're not reachable, the transaction will eventually be consummated.

### Event Service

Suppose you have a system containing data that changes periodically, and refreshing the data on remote objects when the data changes is important if not essential. Without a special mechanism to signal data changes, you have to rely on a system of polling and retrieval when a change is reported.

COM+ adds something new named event service. It classifies programs in two ways: publishers and subscribers. A publisher provides information updates. A subscriber receives the information updates as notifications. The event service of COM+ provides an easy way for subscribers to sign up to receive these notifications from publishers, and for publishers to locate and make calls to their subscribers.
