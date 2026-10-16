|  | adds a `ContextBindingElement` to exchange context information. The context binding element was needed with Windows Workflow Foundation (WF) 3.0. |
| `WebHttpBinding` | This binding is used for services that are exposed through HTTP requests instead of SOAP requests. This is useful for scripting clients—for example, ASP.NET AJAX. |
| `WSFederationHttpBinding` | `WSFederationHttpBinding` is a secure and interoperable binding that supports sharing identities across multiple systems for authentication and authorization. |
| `WSDualHttpBinding` | The binding `WSDualHttpBinding`, in contrast to `WSHttpBinding`, supports duplex messaging. |
| `NetTcpBinding` | All standard bindings prefixed with the name `Net` use a binary encoding used for communication between .NET applications. This encoding is faster than the text encoding with WSxxx bindings. The binding `NetTcpBinding` uses the TCP/IP protocol. |
| `NetTcpContextBinding` | Similar to `WSHttpContextBinding`, `NetTcpContextBinding` adds a `ContextBindingElement` to exchange context with the SOAP header. |
| `NetHttpBinding` | This is a new binding since .NET 4.5 to support the Web Socket transport protocol. |
| `NetPeerTcpBinding` | `NetPeerTcpBinding` provides a binding for peer-to-peer communication. |
| `NetNamedPipeBinding` | `NetNamedPipeBinding` is optimized for communication between different processes on the same system. |
| `NetMsmqBinding` | The binding `NetMsmqBinding` brings queued communication to WCF. Here, the messages are sent to the message queue. |
| `MsmqIntegrationBinding` | `MsmqIntegrationBinding` is the binding for existing applications that uses message queuing. In contrast, the binding `NetMsmqBinding` requires WCF applications on both the client and server. |
| `CustomBinding` | With a `CustomBinding` the transport protocol and security requirements can be completely customized. |