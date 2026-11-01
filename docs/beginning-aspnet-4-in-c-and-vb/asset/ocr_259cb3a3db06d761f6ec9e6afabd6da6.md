# Manual Deployment

You can deploy the assembly manually with the command-line utility .NET Services installation tool `regsvcs.exe`. Starting the command

```
regsvcs SimpleServer.dll
```

registers the assembly `SimpleServer` as a COM+ application and configures the included components according to their attributes; it also creates a type library that can be used by COM clients accessing the .NET component.

After you've configured the assembly, you can start the Component Services Explorer by selecting Administrative Tools › Component Services. In the left tree view of this application, you can select Component Services › Computers › My Computer › COM+ Applications to verify that the application was configured.

![](bbox=[0.08, 0.5, 0.85, 0.6])

# Creating an Installer Package

With the Component Services Explorer, you can create Windows installer packages for server or client systems. An installer package for the server includes the assemblies and configuration settings to install the application on a different server. If the serviced component is invoked from applications running on different systems, a proxy must be installed on the client system. The installer package for the client includes assemblies and configuration for proxies.

To create an installer package, you can start the Component Services Explorer, select the COM+ application, select the menu options Action › Export, and click the Next button in the first dialog. The dialog shown in Figure 51-4 opens. Within this box you can export either a Server application or an Application proxy. With the option Server application you can also configure to Export user identities with roles. This option should be selected only if the target system is in the same domain as the system where the package is created, because the configured user identities are put into the installer package. With Application proxy, an installer package for the client system is created.

![](bbox=[0.45, 0.6, 0.9, 0.88])

![](bbox=[0.08, 0.9, 0.85, 0.97])

To install the proxy, you have to start `setup.exe` from the installer package. Be aware that an application proxy cannot be installed on the same system where the application is installed. After installation of the application proxy, you can see an entry in Component Services Explorer that represents the application proxy. With the application proxy the only option that can be configured is the name of the server in the Activation tab, as discussed in the next section.