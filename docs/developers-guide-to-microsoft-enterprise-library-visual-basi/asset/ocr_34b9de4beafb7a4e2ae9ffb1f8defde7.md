The default behavior of Enterprise Library is to create a new Unity container, create a new configurator for the container, and then read the configuration information from the application's default configuration file (App.config or Web.config). The following code extract shows the process that occurs.

```
```vb
Dim container = New UnityContainer()
Dim configurator = New UnityContainerConfigurator(container)

' Read the configuration files and set up the container.
EnterpriseLibraryContainer.ConfigureContainer(container, _
    ConfigurationSourceFactory.Create())

' The container is now ready to resolve Enterprise Library objects
```
```

The task of the configurator is to translate the configuration file information into a series of registrations within the container. Enterprise Library contains only the **Unity ContainerConfigurator**, though you can write your own to suit your chosen container, or obtain one from a third party.

An alternative approach is to create a custom implementation of the **IServiceLocator** interface that may not use a configurator, but can read the application configuration and return the appropriate fully populated Enterprise Library objects on demand.

See http://commonservicelocator.codeplex.com for more information about the **IServiceLocator** interface.

To keep up with discussions regarding alternate configuration options for Enterprise Library, see the forums on CodePlex at http://www.codeplex.com/entlib/Thread/List.aspx.