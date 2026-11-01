# BINDING

A binding describes how a service wants to communicate. With binding, you can specify the following features:

+   - Transport protocol
+   - Security
+   - Encoding format
+   - Transaction flow
+   - Reliability
+   - Shape change
+   - Transport upgrade

A binding is composed of multiple binding elements that describe all binding requirements. You can create a custom binding or use one of the predefined bindings that are shown in the following table.

| STANDARD BINDING | DESCRIPTION |
|---|---|
| BasicHttpBinding | BasicHttpBinding is the binding for the broadest interoperability, the first-generation Web services. Transport protocols used are HTTP or HTTPS; security is available only from the transport protocol. |
| WSHttpBinding | WSHttpBinding is the binding for the next-generation Web services, platforms that implement SOAP extensions for security, reliability, and transactions. The transports used are HTTP or HTTPS; for security the WS-Security specification is implemented; transactions are supported, as has been described, with the WS-Coordination, WS-AtomicTransaction, and WS-BusinessActivity specifications; reliable messaging is supported with an implementation of WS-ReliableMessaging. WS-Profile also supports MTOM (Message Transmission Optimization Protocol) encoding for sending attachments. You can find specifications for the WS-* standards at http://www.oasis-open.org. |
| WS2007HttpBinding | WS2007HttpBinding derives from the base class WSHttpBinding and supports security, reliability, and transaction specifications defined by OASIS (Organization for the Advancement of Structured Information Standards). |
| WSHttpContextBinding | WSHttpContextBinding derives from the base class WSHttpBinding and adds support for a context without using cookies. This binding adds a ContextBindingElement to exchange context information. |
| WebHttpBinding | This binding is used for services that are exposed through HTTP requests instead of SOAP requests. This is useful for scripting clients — for example, ASP.NET AJAX. |
| WSFederationHttpBinding | WSFederationHttpBinding is a secure and interoperable binding that supports sharing identities across multiple systems for authentication and authorization. |
| WSDualHttpBinding | The binding WSDualHttpBinding, in contrast to WSHttpBinding, supports duplex messaging. |
| NetTcpBinding | All standard bindings prefixed with the name Net use a binary encoding used for communication between .NET applications. This encoding is faster than the text encoding with WSxxx bindings. The binding NetTcpBinding uses the TCP/IP protocol. |
| NetTcpContextBinding | Similar to WSHttpContextBinding, NetTcpContextBinding adds a ContextBindingElement to exchange context with the SOAP header. |
| NetPeerTcpBinding | NetPeerTcpBinding provides a binding for peer-to-peer communication. |