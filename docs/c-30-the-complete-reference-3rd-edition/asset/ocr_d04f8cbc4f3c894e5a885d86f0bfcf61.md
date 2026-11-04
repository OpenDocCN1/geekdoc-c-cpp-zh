One reason why invoking overloaded constructors through this can be useful is that it can prevent the unnecessary duplication of code. In the foregoing example, there is no reason for all three constructors to duplicate the same initialization sequence, which the use of this avoids. Another advantage is that you can create constructors with implied “default arguments” that are used when these arguments are not explicitly specified. For example, you could create another XYCoord constructor as shown here:

```
public XYCoord(int x) : this(x, x) { }
```

This constructor automatically defaults the y coordinate to the same value as the x coordinate. Of course, it is wise to use such “default arguments” carefully because their misuse could easily confuse users of your classes.

# Object Initializers

C# 3.0 added a new feature called object initializers that provides another way to create an object and initialize its fields and properties. (See Chapter 10 for a discussion of properties.) Using object initializers, you do not call a class’ constructor in the normal way. Rather, you specify the names of the fields and/or properties to be initialized, giving each an initial value. Thus, the object initializer syntax provides an alternative to explicitly invoking a class’ constructor. The primary use of the object initializer syntax is with anonymous types created in a LINQ expression. (Anonymous types and LINQ are described in Chapter 19.) However, because the object initializers can be used (and occasionally are used) with a named class, the fundamentals of object initialization are introduced here.

Let’s begin with a simple example:

```
// A simple demonstration that uses object initializers.

using System;

class MyClass
{
    public int Count;
    public string Str;
}

class ObjInitDemo
{
    static void Main()
    {
        // Construct a MyClass object by using object initializers.
        MyClass obj = new MyClass { Count = 100, Str = "Testing" };

        Console.WriteLine(obj.Count + " " + obj.Str);
    }
}
```

This produces the following output:

```
100 Testing
```

As the output shows, the value of obj.Count has been initialized to 100 and the value of obj.Str has been initialized to “Testing”. Notice, however, that MyClass does not define any explicit constructors, and that the normal constructor syntax has not been used. Rather, obj is created using the following line:

```
MyClass obj = new MyClass { Count = 100, Str = "Testing" };
```