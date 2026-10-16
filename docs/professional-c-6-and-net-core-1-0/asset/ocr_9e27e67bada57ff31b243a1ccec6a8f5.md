```
AddToOutput($" Outstanding issues: {lastModifiedAttribute.Issues}");
}
}
```

# Finally, here is the helper `AddToOutput` method:

```
static void AddToOutput(string message)
{
    outputText.Append("\n" + message);
}
```

# Running this code produces the results shown here:

```
What`s New since Sunday, February 1, 2015

Assembly: VectorClass, Version=1.0.0.0, Culture=neutral,
PublicKeyToken=null
Defined Types:

class Vector
  modified: Saturday, June 6, 2015: updated for C# 6 and .NET
Core
  changes to methods of this class:
System.String ToString()
System.Collections.Generic.IEnumerator`1[System.Double]
GetEnumerator()
  modified: Saturday, June 6, 2015: added to implement
IEnumerable<T>
```

Note that when you list the types defined in the `VectorClass` assembly, you actually pick up two classes: `Vector` and the embedded `VectorEnumerator` class. In addition, note that because the `backDateTo` date of 1 Feb is hard-coded in this example, you actually pick up the attributes that are dated June 6 (when the code was changed to support the Core CLR) but not those dated earlier.

# Using Dynamic Language Extensions for Reflection

Until now you’ve used reflection for reading metadata. You can also use reflection to create instances dynamically from types that aren’t known at compile time. The next sample shows creating an instance of the `Calculator` class without the compiler knowing of this type at compile time. The assembly `CalculatorLib` is loaded dynamically without adding a reference. During runtime, the `Calculator` object is instantiated, and a method is called. After you know how to use the Reflection API, you’ll do the same using the C# `dynamic` keyword. This keyword has been part of the C# language since version 4.

# Creating the Calculator Library

The library that is loaded is a simple Class Library (Package) containing the type `Calculator` with implementations of the `Add` and `Subtract` methods. As the methods are really simple, they are implemented using the expression syntax (code file `CalculatorLib/Calculator.cs`):