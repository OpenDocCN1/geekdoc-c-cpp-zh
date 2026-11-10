# Dual-stack system

A dual-stack system offers the best of both worlds by providing support for both ABAP-based and Java EE-based applications.

ABAP consultants are not directly involved with the installation or maintenance of an application server. This is the role of an SAP Basis consultant. However, because ABAP programs run in the application server, understanding the various components of the application server (and their roles) help to understand the backend process that takes place when an ABAP program is executed.

Discussing all of the components in an application layer is beyond the scope of this book. Therefore, we'll limit our discussion to some of the important components that make up the application layer.

The various components of an SAP system are collectively called *instances*. These instances process user requests, and we can have any number of application server instances.

Some of the major components of the application server instance are as follows:

+   - ICM
+   - ABAP Dispatcher
+   - SAP Web Dispatcher
+   - Gateway
+   - SAP start service
+   - Work processes

Each application server instance can have multiple work processes but can't have more than one ICM, dispatcher, gateway, and SAP start service.

Along with multiple application server instances, there is a special instance called the *ABAP System Central Services* (ASCS) *instance*. The ASCS instance includes the message server, the enqueue server, and a separate start service. The ASCS instance handles managing locks, exchanging messages, and load balancing.

The *message server* takes care of load balancing and communication between multiple instances, whereas the *enqueue server* manages application locks. Application locks ensure that no two users edit the same data at the same time.