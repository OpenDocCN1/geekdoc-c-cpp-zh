```
```csharp
// volume of cube 1
volume = Cube1.height * Cube1.length * Cube1.breadth;
Console.WriteLine("Volume of Cube 1 : {0}", volume);
// volume of cube 2
volume = Cube2.height * Cube2.length * Cube2.breadth;
Console.WriteLine("Volume of Cube 2 : {0}", volume);
Console.ReadKey();
        }
    }
}
```
```

The code will return the following result:

![](bbox=[0.034, 0.33, 0.928, 0.543])

# Encapsulation and Member Functions

A member function for a class is simply a function with a definition or prototype within the definition of the class in the same way as any other function. Such a function can operate on any object of the class in which it is a member, and it can access all the class members for the object.

Member functions are simply the attributes of the object (from a design perspective) and they are defined as *private* so as to implement the concept of encapsulation. We can only access such variables using public member functions. Let’s demonstrate how we can set and access the various members of a class in C#:

```
```csharp
using System;
namespace CubeApplication {
```
```