service and capability, are largely implicit in the structure of the WSDL namespace (this will be discussed in detail later). The interface contract encompasses the interface definition but, as was discussed in Chapter 6, there is a lot more to the contract than just the interface definition. The interface contract may encompass multiple WSDLs, particularly if the best practice recommendation (Chapter 7) of only having one interface per WSDL is followed. In the ensuing discussion, unless explicitly stated otherwise, the term service is a reference to the abstract service concept, not the WSDL definition.

# Why Are Names Important?

When you use a service, that service and its operations need to be readily identifiable and distinguishable from other services and operations. This is accomplished by giving a unique name to each abstract service and, within the service, to each port type (interface) and operation of that service. Unique names are also required for the messages, data structures, and other artifacts used in the definition of the service interface. When you use JMS destinations (queues and topics), it is also important to distinguish them from other destinations. This gives you the flexibility to move these destinations to other EMS servers.

There are two significant challenges that you will encounter when creating names:

+   1. Ensuring that each name is reasonably descriptive
+   2. Ensuring that each name is unique

Naming standards establish how names are structured and organized and how (by whom) uniqueness is guaranteed, and thus determine how both challenges are addressed.

# Names Are Difficult to Change

Unfortunately, once established, names tend to become deeply embedded in service providers, service consumers, and the components that mediate interactions between the two. Thus changing established names is expensive—often prohibitively so. You are going to be stuck with the names you choose for a long time, so it is worth an investment of time in considering the standards that govern their structure.