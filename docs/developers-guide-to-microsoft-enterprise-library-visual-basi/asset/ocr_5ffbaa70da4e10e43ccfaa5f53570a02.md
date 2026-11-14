```
Public Class MyNewObject
    Public Sub New(<Dependency("CustomerDB")> customers As Database)
        ' code to use the resolved Database instance here
    End Sub
End Class
```

If your class has multiple constructors, and you want to specify the one Unity will use, you apply the InjectionConstructor attribute to that constructor, as shown in the code excerpt that follows. If you do not specify the constructor to use, Unity chooses the most complex (usually the one with the most parameters). This technique is useful if the most complex constructor has parameters that Unity cannot resolve.

```
Public Class MyNewObject
    Public Sub New(defaultDB As Database, departmentName As String)
        ...
    End Sub
    <InjectionConstructor> _
    Public Sub New(defaultDB As Database)
        ...
    End Sub
End Class
```

# PROPERTY (SETTER) INJECTION

Property (setter) injection can populate one or more properties of your custom classes at run time. Unlike constructor injection, property injection does not occur by default. You must specify the dependency using a configuration file, programmatically at run time, or by applying an attribute to the property that holds the dependent type.

# Design-Time Configuration

To define property injection using a configuration file, you simply specify the names of the properties that Unity should populate within the register element. If you want Unity to resolve the type specified by the property, you need do no more than that. If you want to specify a value, you can include this within the property element. If you want Unity to use a named registration within the container to resolve the type, you include the dependencyName attribute in the property element. Finally, if you want to resolve a type that is compatible with the property name, such as resolving an interface type for which you have named mappings already registered in the container, you specify the type to resolve using a dependencyType attribute.

The following excerpt from a configuration file specifies dependency injection for three public properties of a type named MyOtherObject. Unity will resolve whatever type the BusinessComponent property of the MyOtherObject type is defined as through the container and inject the result into that property. It will also inject the string