```
theDB = value
End Set
End Property
End Class
```

When you apply the **Dependency** attribute without specifying a name, the container will return the type specified as the default (an unregistered registration) or a new instance of that type. To specify a named registration when using property injection with attributes, you include the name as a parameter of the **Dependency** attribute, as shown below.

```
Public Class MyNewObject

Private theDB As Database

<Dependency("LocalDB")> _
Public Property NamedDB() As Database
    Get
        Return theDB
    End Get
    Set(ByVal value As Database)
        theDB = value
    End Set
End Property

End Class
```

# METHOD CALL INJECTION

Method call injection is a less common approach than constructor and property setter injection, but is useful in two specific situations. Firstly, constructor injection only works when you are instantiating new instances of objects (when the constructor is executed), whereas method call injection will work with existing instances of objects. For example, Unity will execute the method when it resolves an instance that is registered as a singleton, or when you call the **BuildUp** method of the container.

Secondly, while property setter injection also works with existing instances, it requires public properties to be exposed. Using method call injection means that you do not need to expose public properties to be able to inject values into existing instances of resolved types.

The usual approach is to expose a public initialization method that takes as parameters the objects you want to resolve and obtain references to. Unity will populate the parameters and then call the method. As the method executes, you store the resolved types in local variables of your class.

Method call injection does not occur by default, and must be configured using a configuration file, programmatically at run time, or by applying an attribute to the method.