```
/// <summary>
/// Indicates whether there is a value or whether
/// the value is "null"
/// </summary>
public bool HasValue { get; set; }
...
}
```

Although this option requires only one implementation of a nullable type, the runtime always boxes value types when setting the Value property. Furthermore, calls to retrieve data from Nullable.Value will not be strongly typed, so retrieving the value type will require a cast operation, which is potentially invalid at runtime.

Neither option is particularly attractive. To deal with dilemmas such as this, C# 2.0 includes the concept of generics. In fact, the nullable modifier, ?, uses generics internally.

# Introducing Generic Types

Generics provide a facility for creating data structures that are specialized to handle specific types when declaring a variable. Programmers define these parameterized types so that each variable of a particular generic type has the same internal algorithm but the types of data and method signatures can vary based on programmer preference.

To minimize the learning curve for developers, C# designers chose syntax that matched the similar templates concept of C++. In C#, therefore, the syntax for generic classes and structures uses the same angle bracket notation to identify the data types on which the generic declaration specializes.

# Using a Generic Class

Listing 11.6 shows how you can specify the actual type used by the generic class. You instruct the path variable to use a Cell type by specifying Cell within angle bracket notation in both the instantiation and the declaration expressions. In other words, when declaring a variable (path in this case) using a generic data type, C# requires the developer to identify the actual type. An example showing the new Stack class appears in Listing 11.6.