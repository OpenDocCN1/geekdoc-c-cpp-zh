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

+   Microsoft.Practices.EnterpriseLibrary.Common.Configuration.Unity

+   Microsoft.Practices.Unity