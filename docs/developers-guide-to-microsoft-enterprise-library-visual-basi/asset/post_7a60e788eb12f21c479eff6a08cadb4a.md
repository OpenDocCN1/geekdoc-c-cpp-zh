
- Add exception handling capabilities by using the exception handling handler.
    This call handler uses the Exception Handling block to implement a consistent
    strategy for handling, replacing, wrapping, and logging exceptions.
- Add authorization capabilities to objects by using the authorization handler.
    This call handler uses the Security block to check if the caller has the required
    permission to execute each call.
- Add performance measurement capabilities by using the performance counter
    handler. This call handler updates Windows® performance counters with each
    call, allowing you to measure performance and monitor target object activity.
- Add custom behavior to objects by creating your own interception call
    handlers.

For more information about using Unity to implement interception, see the documentation installed with Enterprise Library or available online at http://go.microsoft.com/fwlink/?LinkId=188874.

For information on how to use the Policy Injection block facade, see the documentation for version 4.1 of Enterprise Library on MSDN® at http://msdn.microsoft.com/en-us/library/dd139982.aspx.

## Appendix D

## Enterprise Library Configuration Scenarios

The comprehensive configuration capabilities of Enterprise Library—the result of the extensible configuration system and the configuration tools it includes—make Enterprise Library highly flexible and easy to use. The combination of these features allows you to:

- Read configuration information from a wide range of sources.
- Enforce common configuration settings across multiple applications.
- Share configuration settings between applications.
- Specify a core set of configuration settings that applications can inherit.
- Merge configuration settings that are stored in a shared location.
- Create different configurations for different deployment environments.

This appendix provides an overview of the scenarios for using these features and demonstrates how you can apply them in your own applications and environments. More information on the scenarios presented here is provided in the documentation installed with Enterprise Library and available online at http://go.microsoft.com/fwlink/?LinkId=188874.

## About Enterprise Library Configuration

Enterprise Library configuration information is stored in instances of classes that implement the IConfigurationSource interface, and are typically known as configuration sources. Figure 1 shows a high-level view of the two types of information for a configuration source and the different ways that an application's configuration can be defined and applied.

![](img/d7009d38323c3b86f2dfbc5155fbf141_255_0.png)

**FIGURE 1** Configuration sources in Enterprise Library

## EXTERNAL CONFIGURATION

External configuration encompasses the different ways that configuration information can reside in a persistent store and be applied to a configuration source at run time. Possible sources of persistent configuration information are files, a database, and other custom sources. Enterprise Library can load configuration information from any of these stores automatically. To store configuration in a database you can use the SQL configuration source that is available as a sample from the Enterprise Library community site at http://entlib.codeplex.com. You can also specify one or more configuration sources to satisfy more complex configuration scenarios, and create different configurations for different run-time environments. See the section “Scenarios for Advanced Configuration” later in this appendix for more information.

## PROGRAMMATIC SUPPORT

Programmatic support encompasses the different ways that configuration information can be generated dynamically and applied to a configuration source at run time. Typically, in Enterprise Library this programmatic configuration takes place through the fluent interface specially designed to simplify dynamic configuration, or by using the methods exposed by the Microsoft® .NET Framework System.Configuration API.

## Using the Fluent Interfaces

All of the application blocks except for the Validation Application Block and Policy Injection Application Block expose a fluent interface. This allows you to configure the block at run time using intuitive code assisted by Microsoft IntelliSense® in Visual Studio® to specify the providers and properties for the block. The following is an example of configuring an exception policy for the Exception Handling Application Block and loading this configuration into the Enterprise Library container.

```
Dim builder = New ConfigurationSourceBuilder()

builder.ConfigureExceptionHandling() _
    .GivenPolicyWithName("MyPolicy") _
    .ForExceptionTypeOf(Of NullReferenceException)() _
    .LogToCategory("General") _
    .WithSeverity(System.Diagnostics.TraceEventType.Warning) _
    .UsingEventId(9000) _
    .WrapWith(Of InvalidOperationException)() _
    .UsingMessage("MyMessage") _
    .ThenThrowNewException()

Dim configSource = New DictionaryConfigurationSource()
builder.UpdateConfigurationWithReplace(configSource)
EnterpriseLibraryContainer.Current _
    = EnterpriseLibraryContainer.CreateDefaultContainer
```

## Scenarios for Advanced Configuration

The Enterprise Library stand-alone configuration console and the Visual Studio integrated configuration editor allow you to satisfy a range of advanced configuration scenarios based on external configuration sources such as disk files. When you use the configuration tools without specifying a configuration source, they default to using the System Configuration Source to create a single configuration file that contains the entire configuration for the application. Your application will expect this to be named App.config or Web.config (depending on the technology you are using), and will read it automatically.

You can select Add Configuration Settings on the Blocks menu to display the section that contains the default system configuration source. If you click the chevron arrow to the right of the Configuration Sources title to open the section properties pane you can see that this is also, by default, specified as the Selected Source—the configuration source to which the configuration generated by the tool will be written. When an application that uses Enterprise Library reads the configuration, it uses the settings specified for the selected source.

The following sections describe the common scenarios for more advanced configuration that you can accomplish using the configuration tools. Some of these scenarios require you to add additional configuration sources to the application configuration.

## SCENARIO 1: USING THE DEFAULT APPLICATION CONFIGURATION FILE

This is the default and simplest scenario. You configure your application using the configuration tool without adding a Configuration Sources section or any configuration sources. You must specify either your application's App.config or Web.config file when you save the configuration, or use the configuration tool to edit an existing App.config or Web.config file.

## SCENARIO 2: USING A NON-DEFAULT CONFIGURATION STORE

In this scenario, you want to store your configuration in a file or other type of store, instead of in the application's App.config or Web.config file. To achieve this you:

1. Use the configuration tools to add a suitable configuration source to the Configuration Sources section. If you want to use a standard format configuration file, add a file-based configuration source. To store the configuration information in a different type of store, you must install a suitable configuration source. You can use the sample SQL configuration source that is available from the Enterprise Library community site at http://entlib.codeplex.com to store your configuration in a database.

2. Set the relevant properties of the new configuration source. For example, if you are using the built-in file-based configuration source, set the File Path property to the path and name for the configuration file.
