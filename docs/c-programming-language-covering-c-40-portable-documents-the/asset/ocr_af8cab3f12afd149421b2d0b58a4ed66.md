+   - If T is a class-type:
+     - A new instance of class T is allocated. If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown and no further steps are executed.
+     - All fields of the new instance are initialized to their default values (§5.2).
+     - The instance constructor is invoked according to the rules of function member invocation (§7.5.4). A reference to the newly allocated instance is automatically passed to the instance constructor and the instance can be accessed from within that constructor as this.
+   - If T is a struct-type:
+     - An instance of type T is created by allocating a temporary local variable. Since an instance constructor of a struct-type is required to definitely assign a value to each field of the instance being created, no initialization of the temporary variable is necessary.
+     - The instance constructor is invoked according to the rules of function member invocation (§7.5.4). A reference to the newly allocated instance is automatically passed to the instance constructor and the instance can be accessed from within that constructor as this.

# 7.6.10.2 Object Initializers

An object initializer specifies values for zero or more fields or properties of an object.

```
object-initializer:
  { member-initializer-list , }
  { member-initializer-list , }

member-initializer-list:
  member-initializer
  member-initializer-list , member-initializer

member-initializer:
  identifier = initializer-value

initializer-value:
  expression
  object-or-collection-initializer
```

An object initializer consists of a sequence of member initializers, enclosed by { and } tokens and separated by commas. Each member initializer must name an accessible field or property of the object being initialized, followed by an equals sign and an expression, object initializer, or collection initializer. It is an error for an object initializer to include