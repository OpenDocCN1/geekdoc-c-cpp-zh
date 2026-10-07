```
}
private string _Id;
}
```

By using private on the setter, the property appears as read-only to classes other than Employee. From within Employee, the property appears as read/write, so you can assign the property within the class itself. When specifying an access modifier on the getter or setter, take care that the access modifier is more restrictive than the access modifier on the property as a whole. It is a compile error, for example, to declare the property as private and the setter as public.

# Guidelines

+   DO apply appropriate accessibility modifiers on implementations of getters and setters on all properties.
DO NOT provide set-only properties or properties with the setter having broader accessibility than the getter.

# Properties and Method Calls Not Allowed as ref or out
Parameter Values

C# allows properties to be used identically to fields, except when they are passed as ref or out parameter values. ref and out parameter values are internally implemented by passing the memory address to the target method. However, because properties may not have a backing field or can be read-only or write-only, it is not possible to pass the address for the underlying storage. As a result, you cannot pass properties as ref or out parameter values. The same is true for method calls. Instead, when code needs to pass a property or method call as a ref or out parameter value, the code must first copy the value into a variable and then pass the variable. Once the method call has completed, the code must assign the variable back into the property.