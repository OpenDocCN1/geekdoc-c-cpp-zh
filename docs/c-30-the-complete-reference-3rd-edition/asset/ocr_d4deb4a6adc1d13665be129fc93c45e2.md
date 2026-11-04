```
Console.WriteLine();
Console.WriteLine("Info for t2: ");
t2.ShowStyle();
t2.ShowDim();
Console.WriteLine("Area is " + t2.Area());
}
```

In this version, the properties Width and Height provide access to the private members, pri_width and pri_height, which actually store the values. Therefore, even though pri_width and pri_height are private to TwoDShape, their values can still be set and obtained through their corresponding public properties.

When referring to base and derived classes, sometimes the terms superclass and subclass are used. These terms come from Java programming. What Java calls a superclass, C# calls a base class. What Java calls a subclass, C# calls a derived class. You will commonly hear both sets of terms applied to a class of either language, but this book will continue to use the standard C# terms. C++ also uses the base-class/derived-class terminology.

# Using Protected Access

As just explained, a private member of a base class is not accessible to a derived class. This would seem to imply that if you wanted a derived class to have access to some member in the base class, it would need to be public. Of course, making the member public also makes it available to all other code, which may not be desirable. Fortunately, this implication is untrue because C# allows you to create a protected member. A protected member is public within a class hierarchy, but private outside that hierarchy.

A protected member is created by using the protected access modifier. When a member of a class is declared as protected, that member is, with one important exception, private. The exception occurs when a protected member is inherited. In this case, a protected member of the base class becomes a protected member of the derived class and is, therefore, accessible to the derived class. Therefore, by using protected, you can create class members that are private to their class but that can still be inherited and accessed by a derived class.

Here is a simple example that uses protected:

```
// Demonstrate protected.

using System;

class B {
    protected int i, j; // private to B, but accessible by D

    public void Set(int a, int b) {
        i = a;
        j = b;
    }

    public void Show() {
        Console.WriteLine(i + " " + j);
    }
}
```