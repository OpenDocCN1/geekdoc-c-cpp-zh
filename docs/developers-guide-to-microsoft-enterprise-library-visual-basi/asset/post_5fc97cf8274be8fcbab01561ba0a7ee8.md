
## ENTERPRISE LIBRARY OBJECTS, FACADES, AND FACTORIES

Each of the application blocks in Enterprise Library contains one or more core objects that you typically use to access the functionality of that block. An example is the Exception Handling Application Block, which provides a facade named **Exception Manager** that exposes the methods you use to pass exceptions to the block for handling.

The following table lists the commonly used objects for each block.

| Application Block | Non-static Instance or Factory |
| :--- | :--- |
| Caching | ICacheManager |
| Cryptography | CryptographyManager |
| Data Access | Database |
| Exception Handling | ExceptionManager |
| Logging | LogWriter<br>TraceManager |
| Security | ISecurityCacheProvider<br>IAuthorizationProvider |
| Validation | ValidatorFactory<br>ConfigurationValidatorFactory<br>AttributeValidatorFactory<br>ValidationAttributeValidatorFactory |

There are also task-specific objects in some blocks that you can create directly in your code in the traditional way using the operator. For example, you can create individual validators from the Validation Application Block, or log entries from the Logging Application Block. We show how to do this in the examples for each application block chapter.

To use the features of an application block, all you need to do is create an instance of the appropriate object, facade, or factory listed in the table above and then call its methods. The behavior of the block is controlled by the configuration you specified, and often you can carry out tasks such as exception handling, logging, caching, and encrypting values with just a single line of code. Even tasks such as accessing data or validating instances of your custom types require only a few lines of simple code. So, let's look at how you create instances of the Enterprise Library objects you want to use.

## CREATING INSTANCES OF ENTERPRISE LIBRARY TYPES

In this release of Enterprise Library, there are two recommended approaches to creating instances of the Enterprise Library objects. The decision as to which you use is based solely on the way you decide to architect your application. You can use the simple approach of obtaining instances using the Enterprise Library service locator, which provides access to the Unity container that holds the Enterprise Library configuration information. Alternatively, if you are already a DI convert, you can take charge of the entire process by creating and populating a container and using it to create and manage both Enterprise Library objects and your own custom types. We'll look at both approaches next.

### The Simple Approach — Using the Enterprise Library Service Locator

When you initially create an instance of an Enterprise Library type in your application code, the underlying mechanism reads your configuration information into a container and exposes it to your code through a service locator that is initialized as part of the Enterprise Library configuration mechanism. This service locator provides methods that you can call at any point in your application code to obtain configured instances of any Enterprise Library type.

For example, if you are using the Logging Application Block, you can obtain a reference to a LogWriter using a single line of code, and then call its Write method to write your log entry to the configured targets, as shown here.

```
Dim writer = EnterpriseLibraryContainer.Current.GetInstance(Of LogWriter)()
writer.Write("I'm a log entry created by the Logging block.")
```

> Notice that this code uses type inference by omitting the variable type name keyword. The variable will assume the type returned by the assignment; this technique can make your code more maintainable.

If you configured more than one instance of a type for a block, such as more than one Database for the Data Access Application Block, you can specify the name when you call the GetInstance method. For example, you may configure an Enterprise Library Database instance named Customers that specifies a Microsoft SQL Server® database, and a separate Database instance named Products that specifies a different type of database. In this case, you specify the name of the object you want to resolve when you call the GetInstance method, as shown here.

```
Dim customerDb _
    = EnterpriseLibraryContainer.Current.GetInstance(Of Database)("Customers")
```

You don't have to initialize the block, read configuration information, or do anything other than call the methods of the service locator. For many application scenarios, this simple approach is ideal for obtaining instances of the Enterprise Library types you want to use.

### The Sophisticated Approach — Accessing the Container Directly

If you want to take advantage of design patterns such as Dependency Injection and Inversion of Control in your application, you will probably already be considering the use of a dependency injection mechanism to decouple your components and layers, and to resolve types. If this is the case, the more sophisticated approach to incorporating Enterprise Library into your applications will fit well with your solution architecture.

Instead of allowing Enterprise Library to create, populate, and expose a default container that holds just Enterprise Library configuration information, you can create the container and populate it yourself—and hold onto a reference to the container for use in your application code. This not only allows you to obtain instances of Enterprise Library objects, it also lets you use the container to implement dependency injection for your own custom types. Effectively, the container itself becomes your service locator.

For example, you can create registrations and mappings in the container that specify features such as the dependencies between the components of your application, mappings between types, the values of parameters and properties, interception for methods, and deferred object creation.

You may be thinking that all of these wondrous capabilities will require a great deal of code and effort to achieve; however, they don't. To initialize and populate the default Unity container with the Enterprise Library configuration information and make it available to your application, only a single line of code is required. It is shown here:

```
Dim theContainer = New UnityContainer() _
.AddNewExtension(Of EnterpriseLibraryCoreExtension)()
```

Now that you have a reference to the container, you can obtain an instance of any Enterprise Library Application Block by calling the container methods directly. For example, if you are using the Logging Application Block, you can obtain a reference to a LogWriter using a single line of code, and then call its Write method to write your log entry to the configured targets.

```
Dim writer = theContainer.Resolve(Of LogWriter)()
writer.Write("I'm a log entry created by the Logging block!")
```

And if you configured more than one instance of a type for a block, such as more than one database for the Data Access Application Block, you can specify the name when you call the Resolve method, as shown here:

```
Dim customerDb = theContainer.Resolve(Of Database)("Customers")
```

You may have noticed the similarity in syntax between the **Resolve** method and the **GetInstance** method we used earlier. Effectively, when you are using the default Unity container, the **GetInstance** method of the service locator simply calls the **Resolve** method of the Unity container. It therefore makes sense that the syntax and parameters are similar. Both the container and the service locator expose other methods that allow you to get collections of objects, and there are both generic and non-generic overloads that allow you to use the methods in languages that do not support generics.

One point to note if you choose this more sophisticated approach to using Enterprise Library in your applications is that you should import two additional namespaces into your code. These namespaces include the container and core extension definitions:

- Microsoft.Practices.EnterpriseLibrary.Common.Configuration.Unity
- Microsoft.Practices.Unity
