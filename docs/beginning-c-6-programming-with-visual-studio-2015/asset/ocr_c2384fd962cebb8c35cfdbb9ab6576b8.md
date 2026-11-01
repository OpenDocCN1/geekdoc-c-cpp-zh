consequences of this implementation is that a service can broadcast messages to multiple clients simultaneously.

+   - **Named pipe** — Enables you to communicate with WCF services that are on the same machine as the calling code, but reside in a separate process.
+   - **MSMQ** — Microsoft Message Queuing is a queuing technology that enables messages sent by an application to be routed through a queue to arrive at a destination. MSMQ is a reliable messaging technology that ensures that a message sent to a queue will reach that queue. MSMQ is also inherently asynchronous, so a queued message will be processed only when messages ahead of it in the queue have been processed and a processing service is available.

These protocols often enable you to establish secure connections. For example, you can use the HTTPS protocol to establish an SSL connection across the Internet. TCP offers extensive possibilities for security in a local network by using the Windows security framework. UDP doesn't support security.

In order to connect to a WCF service, you must know where it is. In practice, this means knowing the address of an endpoint.

# Addresses, Endpoints, and Bindings

The type of address you use for a service depends on the protocol that you are using. Service addresses are formatted for the three protocols described in this chapter (MSMQ is not covered) as follows:

+   - **HTTP** — Addresses for the HTTP protocol are URLs of the familiar form http://<server>:<port>/<service>. For SSL connections, you can also use https://<server>:<port>/<service>. If you are hosting a service in IIS, <service> will be a file with a .svc extension. IIS addresses will probably include more subdirectories than this example — that is, more sections separated by / characters before the .svc file.
+   - **TCP** — Addresses for TCP are of the form net.tcp://<server>:<port>/<service>.
+   - **UDP** — Addresses for UDP are of the form soap.udp://<server>:<port>/<service>. Certain <server> values are required for multicast communications, but this is beyond the scope of this chapter.
+   - **Named pipe** — Addresses for named pipe connections are similar but have no port number. They are of the form net.pipe://<server>/<service>.

The address for a service is a base address that you can use to create addresses for endpoints representing operations. For example, you might have an operation at net.tcp://<server>:<port>/<service>/operation1.

For example, imagine you create a WCF service with a single operation that has bindings for all three of the protocols listed here. You might use the following base addresses:

```
http://www.mydomain.com/services/amazingservices/mygreatservice.svc
net.tcp://myhugserver:8080/mygreatservice
net.pipe://localhost/mygreatservice
```