type argument is fine for many purposes, sometimes it is useful to limit the types that can be used as a type argument. For example, you might want to create a method that operates on the contents of a stream, including a FileStream or MemoryStream. This situation seems perfect for generics, but you need some way to ensure that only stream types are used as type arguments. You don’t want to allow a type argument of int, for example. You also need some way to tell the compiler that the methods defined by a stream will be available for use. For example, your generic code needs some way to know that it can call the Read() method.

To handle such situations, C# provides constrained types. When specifying a type parameter, you can specify a constraint that the type parameter must satisfy. This is accomplished through the use of a where clause when specifying the type parameter, as shown here:

```
class class-name<type-param> where type-param : constraints { // ...
```

Here, constraints is a comma-separated list of constraints.

C# defines the following types of constraints.

+   - You can require that a certain base class be present in a type argument by using a base class constraint. This constraint is specified by naming the desired base class. There is a variation of this constraint, called a naked type constraint, in which a type parameter (rather than an actual type) specifies the base class. This enables you to establish a relationship between two type parameters.
+   - You can require that one or more interfaces be implemented by a type argument by using an interface constraint. This constraint is specified by naming the desired interface.
+   - You can require that the type argument supply a parameterless constructor. This is called a constructor constraint. It is specified by new().
+   - You can specify that a type argument must be a reference type by specifying the reference type constraint: class.
+   - You can specify that the type argument be a value type by specifying the value type constraint: struct.

Of these constraints, the base class constraint and the interface constraint are probably the most often used, but all are important. Each constraint is examined in the following sections.

# Using a Base Class Constraint

The base class constraint enables you to specify a base class that a type argument must inherit. A base class constraint serves two important purposes. First, it lets you use the members of the base class specified by the constraint within the generic class. For example, you can call a method or use a property of the base class. Without a base class constraint, the compiler has no way to know what type of members a type argument might have. By supplying a base class constraint, you are letting the compiler know that all type arguments will have the members defined by that base class.

The second purpose of a base class constraint is to ensure that only type arguments that support the specified base class are used. This means that for any given base class constraint, the type argument must be either the base class, itself, or a class derived from that base class. If you attempt to use a type argument that does not match or inherit the specified base class, a compile-time error will result.