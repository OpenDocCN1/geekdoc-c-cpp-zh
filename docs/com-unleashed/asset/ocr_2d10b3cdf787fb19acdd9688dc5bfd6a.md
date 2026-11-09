and administrators fail to provide it, your program is not going to work. I'm holding out for a type-library–style definition that could accompany components on their deployment, much like IDL transactional attributes do, but no such feature now exists.

User authentication on a local machine or domain effectively guards resources so that only authorized users can access them. This falls short in a Distributed Computing Environment (DCE), where there is communication across a disparate set of topologies and machines. For this reason, the Remote Procedure Call (RPC) was given a security API all its own to provide the extra security a DCE requires.

COM+ is designed and implemented as a layer on top of Microsoft’s RPC implementation supporting complex interactions between independently created software objects. While it reuses many of RPC’s advanced features, including authentication and privacy services, COM+ also adds another layer of security to the RPC API.

# SSPI

The Microsoft Security Support Provider Interface (SSPI) is the well-defined common API for obtaining integrated security services for authentication, message integrity, message privacy, and security quality of service for any distributed application protocol. Application protocol designers can take advantage of this interface to obtain different security services without modification to the protocol itself.

The SSPI provides an abstraction layer between application-level protocols and security protocols. The following are some of the ways to use SSPI services:

+   - Traditional socket-based applications can call SSPI routines directly and implement the application protocol that carries SSPI security-related data, using request and response messages.
+   - COM+ applications provide the best level of integrated security features. Applications can use DCOM to call security options, which are implemented using authenticated RPC and SSPI at lower levels. Applications do not call SSPI APIs directly.
+   - Winsock 2.0 extends the Windows Sockets interface to enable transport providers to expose security features. This approach integrates the SSPI security provider into the network stack and provides both security and transport services through a common interface.

WinInet is an application protocol interface that is designed to support Internet security protocols, such as Secure Sockets Layer (SSL), over Internet protocols. The implementation of WinInet security support uses the SSPI interface to the Secure Channel (Windows NT implementation of SSL) security provider.