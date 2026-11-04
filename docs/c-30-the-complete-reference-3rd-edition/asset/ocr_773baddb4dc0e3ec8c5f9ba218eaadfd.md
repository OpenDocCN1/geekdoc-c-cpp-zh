```
```csharp
if(b==null)
  Console.WriteLine("The cast in b = (B) a is NOT allowed.");
else
  Console.WriteLine("The cast in b = (B) a is allowed");
}
```
```

Here is the output, which is the same as before:

```
```text
The cast in b = (B) a is NOT allowed.
```
```

In this version, the as statement checks the validity of the cast and then, if valid, performs the cast, all in one statement.

# ### Using typeof

Although useful in their own ways, the as and is operators simply test the compatibility of two types. Often, you will need to obtain information about a type. To do this, C# supplies the typeof operator. It retrieves a System.Type object for a given type. Using this object, you can determine the type's characteristics.

The typeof operator has this general form:

```
```csharp
typeof(type)
```
```

Here, type is the type being obtained. The Type object returned encapsulates the information associated with type.

Once you have obtained a Type object for a given type, you can obtain information about it through the use of various properties, fields, and methods defined by Type. Type is a large class with many members, and a discussion is deferred until the next section, where reflection is examined. However, to briefly demonstrate Type, the following program uses three of its properties: FullName, IsClass, and IsAbstract. To obtain the full name of the type, use FullName. IsClass returns true if the type is a class. IsAbstract returns true if a class is abstract.

```
```csharp
// Demonstrate typeof.

using System;
using System.IO;

class UseTypeof {
  static void Main() {
    Type t = typeof(StreamReader);

    Console.WriteLine(t.FullName);

    if(t.IsClass) Console.WriteLine("Is a class.");
    if(t.IsAbstract) Console.WriteLine("Is abstract.");
    else Console.WriteLine("Is concrete.");
  }
}
```
```

This program outputs the following:

```
```text
System.IO.StreamReader
Is a class.
Is concrete.
```
```