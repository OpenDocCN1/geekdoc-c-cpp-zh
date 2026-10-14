```
{
    container.Dispose();
}
}
```

The Register method contains exactly the same code as before. As this method grows, however, it can be refactored into multiple methods and generally kept neater than it otherwise might be if it was contained in the application entry point.

The Resolve method returns a generic Window, which is a common resolution root for a WPF application. Specifically, the TaskListView is returned because it is the main window for your application. In other application types, such as ASP.NET MVC, there are often multiple resolution roots—one for each controller. The organization of the composition root for MVC and other applications is discussed later in this chapter.

# Imperative vs. declarative registration

The registration code to this point has been written imperatively with procedural calls to methods on a container object. This gives you some advantages: it is easy to read, it is relatively succinct, and it provides a minimum of compile-time checking, such as protection against typographical errors. One disadvantage is that you are tying yourself to an implementation at compile time. If you want to swap out one of your implementations for an alternative, this requires a recompile of the code.

If, instead, you use declarative registration via XML, you can obviate the need for a recompile by moving the decision to configuration time. Listing 9-11 shows Unity’s support for XML registration.

# LISTING 9-11 A section in the application configuration file can describe how interfaces should map to implementations.

Click here to view code image

```
<configuration>
    <configSections>
        <section name="unity"
            type="Microsoft.Practices.Unity.Configuration.UnityConfigurationSection,
Microsoft.Practices.Unity.Configuration" />
    </configSections>
    <appSettings>
        <add key="TaskDatabaseConnectionString" value="Data Source=(local);Initial Catalog=TaskDatabase;Integrated Security=True;Application Name=Task List Editor" />
    </appSettings>
    <unity xmlns="http://schemas.microsoft.com/practices/2010/unity">
        <typeAliases>
            <typeAlias alias="ISettings" type="ServiceInterfaces.ISettings, ServiceInterfaces" />
            <typeAlias alias="ApplicationSettings" type="UI.ApplicationSettings, UI" />
            <typeAlias alias="IObjectMapper" type="ServiceInterfaces.IObjectMapper,
```