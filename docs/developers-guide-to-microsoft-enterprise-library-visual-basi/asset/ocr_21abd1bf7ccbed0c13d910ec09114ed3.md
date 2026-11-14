This appendix discusses some of the more advanced topics that will help you to obtain the maximum benefit from Enterprise Library in terms of creating objects and managing the dependency injection container. It includes the following:

+   - Loading configuration information into a Unity container
+   - Viewing the registrations in the container
+   - Populating entire object graphs at application startup
+   - Maintaining a reference to the container in request-based applications
+   - Using an alternative service locator or dependency injection container

These topics provide information about how you can use the more sophisticated dependency injection approach for creating instances of Enterprise Library objects, as described in Chapter 1, “Introduction.” If you have decided not to use this approach, and you are using the Enterprise Library service locator and its **GetInstance** method to instantiate Enterprise Library types, they are not applicable to your scenario.

# Loading Configuration Information into a Unity Container

Unlike many applications, and unlike the application blocks within Enterprise Library, Unity does not automatically load configuration information when it starts. This is intentional; it means that you can load configuration information into one or more new or existing containers, including containers that you create as a hierarchy of parent and child containers.

This also means that you can exert considerable control over how requests for types are handled. For example, you can use multiple containers to specify dependencies for different parts of your application, while allowing requests that cannot be satisfied in a child container to pass up through the hierarchy of parent containers until a suitable registration is found.

It also means that you can load configuration information from different sources. A typical example is loading configuration from a file other than App.config or Web.config, or by adding registrations programmatically—by for example—reading them from a database and applying them to the container.

The Unity container class exposes the **LoadConfiguration** method that you can use to populate a container. You can call this method with no parameters to read a <unity>