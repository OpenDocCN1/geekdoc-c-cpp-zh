# # Using different endpoints

The whole point of WCF is that you can write one service and have IIS accept a lot of different protocols on the same code. Sure, we can do SOAP, which we do in ASMX. We can also do a lot of other protocols. Here is the breakdown of all the different endpoints, according to MSDN:

+   * BasicHttpBinding: A binding that is suitable for communicating with WS-Basic Profile conformant Web services (for example, ASMX-based services). This binding uses HTTP as the transport and text/XML as the default encoding.

+   * WSHttpBinding: A secure and interoperable binding that is suitable for non-duplex service contracts.

+   * DualHttpBinding: A secure and interoperable binding that is suitable for duplex service contracts or communication through SOAP intermediaries.

+   * WSFederationBinding: A secure and interoperable binding that supports the WS-Federation protocol that enables organizations that are in a federation to efficiently authenticate and authorize users.

+   * NetTcpBinding: A secure and optimized binding for cross-machine communication between WCF applications.

+   * NetNamedPipeBinding: A secure, reliable, optimized binding that is suitable for on-machine communication between WCF applications.

+   * NetMmqBinding: A queued binding that is suitable for cross-machine communication between WCF applications.

+   * NetPeerTcpBinding: A binding that enables secure, multiple machine communication.

+   * MsmIntegrationBinding: A binding that is suitable for cross-machine communication between a WCF application and existing Message Queuing applications.

+   * BasicHttpPostBinding: A binding that is suitable for communicating with WS-Basic Profile conformant Web services that enables HTTP cookies to be used for exchange context.

+   * NetTcpBinding: A secure and optimized binding for cross-machine communication between WCF applications that enables SOAP headers to be used for exchange context.

+   * HttpBinding: A binding used to configure endpoints for WCF Web services that are exposed through HTTP requests instead of SOAP messages.

+   * WSHttpBinding: A secure and interoperable binding that is suitable for non-duplex service contracts that enables SOAP headers to be used to exchange context.

When do you use what? If you want to use .NET applications, or the layers of a single application, then use NetTcpBinding. If you are cross-platform communicating, then use WSHttpBinding.

Only if for some reason those don't work do you start looking into the others. Or, and remember that you may have many endpoints of the same service. Don't use SOAP for a data layer. Just make a separate SOAP layer if you need cross-platform support.

| Book VII Chapter 3 | Building Web Services with WCF |