```
<register type="IMyType" mapTo="MyImplementingType"
...
name="Special Customer Object">
</register>
```

# Run-Time Configuration

You can configure injection for the default or a specific constructor at run time by calling the RegisterType method of the Unity container. This approach also gives you a great deal of control over the process. The following code registers the MyNewObject type with a singleton (container-controlled) lifetime.

```
myContainer.RegisterType(Of MyNewObject)(New ContainerControlledLifetimeManager())
```

If you want to create a named registration, you add the name as the first parameter of the RegisterType method, as shown here.

```
myContainer.RegisterType(Of MyNewObject)("Special Customer Object", _
New ContainerControlledLifetimeManager()))
```

If you want to create a mapping, you specify the mapped type as the second generic type parameter, as shown here.

```
myContainer.RegisterType(Of IMyType, MyImplementingType)( _
"Special Customer Object", _
New ContainerControlledLifetimeManager()))
```

If you need to specify the value of the constructor parameters, such as a String type (which Unity cannot create unless you register a String instance with the container), or specify which constructor Unity should choose, you include an instance of the Injection Constructor type in your call to the RegisterType method. For example, the following creates a registration named Special Customer Object for the MyNewObject type as a singleton, specifies that Unity should resolve the type of the parameter named defaultDB and inject the result, and that Unity should inject the string value “Customer Service” into the parameter named departmentName.

```
myContainer.RegisterType(Of MyNewObject)( _
"Special Customer Object", _
New ContainerControlledLifetimeManager(), _
New InjectionConstructor(GetType(Database), "Customer Service") _
)
```

# Configuration with Attributes

When you specify just the type in a constructor parameter, as shown earlier, the container will return the default concrete implementation of that type as defined in the registrations within the container. To specify a named registration when using constructor injection, you can add the Dependency attribute to the parameter definition, as shown below.