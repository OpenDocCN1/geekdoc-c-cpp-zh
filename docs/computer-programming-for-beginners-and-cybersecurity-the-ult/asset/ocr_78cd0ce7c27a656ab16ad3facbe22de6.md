Local variables are those that are defined within the methods, blocks, or constructors. These variables are declared and instantiated inside the method and are destroyed once the method had been carried out.

# Instance variables

Instance variables are those that are inside a class but outside of the methods. They are initialized at the same time as the class. They can be accessed from a method, block, or constructor of that specific class.

A class can contain as many methods as necessary to obtain the values it needs. For example, the Cat class has three methods: running(), sleeping(), and jumping().

# Constructors

A constructor is a method which is used to initialize an object. A class must contain at least one constructor.

The following are the important rules for constructors:

The name of the constructor should match the name of the class

It should have no explicit return type.

# Types of Constructors

+   - Default or no-arg constructor
+   - Parameterized constructor
+   - Default Constructor

A constructor without a parameter is called default constructor.

Here’s the syntax:

```
ClassName() {}
```

# Parameterized Constructor

A parameterized constructor is a constructor with parameters. It is used to supply values to specific objects.