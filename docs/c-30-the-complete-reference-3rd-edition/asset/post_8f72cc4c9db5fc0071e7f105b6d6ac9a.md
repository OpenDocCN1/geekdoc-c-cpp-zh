
When the constructor is executed, the overloaded constructor that matches the parameter list specified by parameter-list2 is first executed. Then, if there are any statements inside the original constructor, they are executed. Here is an example:

```
// Demonstrate invoking a constructor through this.

using System;

class XYCoord {
    public int x, y;

    public XYCoord() : this(0, 0) {
        Console.WriteLine("Inside XYCoord()");
    }

    public XYCoord(XYCoord obj) : this(obj.x, obj.y) {
        Console.WriteLine("Inside XYCoord(obj)");
    }

    public XYCoord(int i, int j) {
        Console.WriteLine("Inside XYCoord(int, int)");
        x = i;
        y = j;
    }
}

class OverloadConsDemo {
    static void Main() {
        XYCoord t1 = new XYCoord();
        XYCoord t2 = new XYCoord(8, 9);
        XYCoord t3 = new XYCoord(t2);

        Console.WriteLine("t1.x, t1.y: " + t1.x + ", " + t1.y);
        Console.WriteLine("t2.x, t2.y: " + t2.x + ", " + t2.y);
        Console.WriteLine("t3.x, t3.y: " + t3.x + ", " + t3.y);
    }
}
```

The output from the program is shown here:

```
Inside XYCoord(int, int)
Inside XYCoord()
Inside XYCoord(int, int)
Inside XYCoord(int, int)
Inside XYCoord(obj)
t1.x, t1.y: 0, 0
t2.x, t2.y: 8, 9
t3.x, t3.y: 8, 9
```

Here is how the program works. In the XYCoord class, the only constructor that actually initializes the x and y fields is XYCoord(int, int). The other two constructors simply invoke XYCoord(int, int) through this. For example, when object t1 is created, its constructor, XYCoord(), is called. This causes this(0, 0) to be executed, which in this case translates into a call to XYCoord(0, 0). The creation of t2 works in similar fashion.

One reason why invoking overloaded constructors through this can be useful is that it can prevent the unnecessary duplication of code. In the foregoing example, there is no reason for all three constructors to duplicate the same initialization sequence, which the use of this avoids. Another advantage is that you can create constructors with implied “default arguments” that are used when these arguments are not explicitly specified. For example, you could create another XYCoord constructor as shown here:

```
public XYCoord(int x) : this(x, x) { }
```

This constructor automatically defaults the y coordinate to the same value as the x coordinate. Of course, it is wise to use such “default arguments” carefully because their misuse could easily confuse users of your classes.

## Object Initializers

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

Here, the names of the fields are explicitly specified along with their initial values. This results in a default instance of MyClass being constructed (by use of the implicit default constructor) and then Count and Str are given the specified initial values.

It is important to understand that the order of the initializers is not important. For example, obj could have been initialized as shown here:

```
MyClass obj = new MyClass { Str = "Testing", Count = 100 };
```

In this statement, the initialization of Str precedes the initialization of Count. In the program, it was the other way around. However, in either case, the end result is the same.

Here is the general form of object initialization syntax:

```
new class-name { name = expr, name = expr, name = expr, ... }
```

Here, name specifies the name of a field or property that is an accessible member of class-name. Of course, the type of the initializing expression specified by expr must be compatible with the type of field or property.

Although you can use object initializers with a named class (such as MyClass in the example), you usually won’t. In general, you will use the normal constructor call syntax when working with named classes. As mentioned, object initializers are most applicable to anonymous types generated by a LINQ expression.

## The Main( ) Method

Up to this point, you have been using one form of Main(). However, it has several overloaded forms. Some can be used to return a value, and some can receive arguments. Each is examined here.

### Return Values from Main( )

When a program ends, you can return a value to the calling process (often the operating system) by returning a value from Main(). To do so, you can use this form of Main():

```
static int Main()
```

### Pass Arguments to Main( )

Many programs accept what are called command-line arguments. A command-line argument is the information that directly follows the program’s name on the command line when it is executed. For C# programs, these arguments are then passed to the Main() method. To receive the arguments, you must use one of these forms of Main():

```
static void Main(string[] args)
static int Main(string[] args)
```

The string array passed to Main() is called args. The length of the args array will be equal to the number of command-line arguments, which might be zero.

For example, the following program displays all of the command-line arguments that it is called with:

```
// Display all command-line information.
using System;
class CLDemo {
    static void Main(string[] args) {
        Console.WriteLine("There are " + args.Length +
            " command-line arguments.");
        Console.WriteLine("They are:");
        for(int i=0; i < args.Length; i++)
            Console.WriteLine(args[i]);
    }
}
```

If CLDemo is executed like this:

```
CLDemo one two three
```

you will see the following output:

```
There are 3 command-line arguments.
They are:
one
two
three
```

To understand the way that command-line arguments can be used, consider the next program. It uses a simple substitution cipher to encode or decode messages. The message to be encoded or decoded is specified on the command line. The cipher is very simple: To encode a word, each letter is incremented by 1. Thus, A becomes B, and so on. To decode, each letter is decremented. Of course, such a cipher is of no practical value, being trivially easy to break. But it does provide an enjoyable pastime for children.

```
// Encode or decode a message using a simple substitution cipher.
using System;
class Cipher {
    static int Main(string[] args) {
        // See if arguments are present.
        if(args.Length < 2) {
            Console.WriteLine("Usage: encode/decode word1 [word2...wordN]");
            return 1; // return failure code
        }
        // If args present, first arg must be encode or decode.
```
