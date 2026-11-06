```
```csharp
Cube1.setHeight(8.0);

// cube 2 specification
Cube2.setLength(10.0);
Cube2.setBreadth(14.0);
Cube2.setHeight(12.0);
// volume of cube 1
volume = Cube1.getVolume();
Console.WriteLine("Volume of Cube1 is: {0}" ,volume);

// volume of cube 2
volume = Cube2.getVolume();
Console.WriteLine("Volume of Cube2 is: {0}", volume);
Console.ReadKey();
}
}
}
```
```

Here is the output from the code:

```
```text
Volume of Cube1 is: 192
Volume of Cube2 is: 1680
```
```

We used the *setter* methods to set the values of the various attributes of our two cubes. The *getVolume()* function has been called to calculate the volumes of the two cubes.

# ## Constructors

A constructor is simply a special member function of a class that is run anytime that we create new objects of the class. A constructor assumes the class name and it should not have a return type. The following example demonstrates how to use a constructor in C#:

```
```csharp
using System;
```
```