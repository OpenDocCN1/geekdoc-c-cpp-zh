
## Interfaces, Structures, and Enumerations

This chapter discusses one of C#'s most important features: the *interface*. An *interface* defines a set of methods that will be implemented by a class. An *interface* does not, itself, implement any method. Thus, an *interface* is a purely logical construct that describes functionality without specifying implementation.

Also discussed in this chapter are two more C# data types: *structures* and *enumerations*. *Structures* are similar to classes except that they are handled as value types rather than reference types. *Enumerations* are lists of named integer constants. Structures and enumerations contribute to the richness of the C# programming environment.

### Interfaces

In object-oriented programming it is sometimes helpful to define what a class must do, but not how it will do it. You have already seen an example of this: the abstract method. An abstract method declares the return type and signature for a method, but provides no implementation. A derived class must provide its own implementation of each abstract method defined by its base class. Thus, an abstract method specifies the *interface* to the method, but not the *implementation*. Although abstract classes and methods are useful, it is possible to take this concept a step further. In C#, you can fully separate a class' *interface* from its implementation by using the keyword *interface*.

Interfaces are syntactically similar to abstract classes. However, in an interface, no method can include a body. That is, an interface provides no *implementation* whatsoever. It specifies what must be done, but not how. Once an interface is defined, any number of classes can implement it. Also, one class can implement any number of interfaces.

To implement an interface, a class must provide bodies (*implementations*) for the methods described by the *interface*. Each class is free to determine the details of its own *implementation*. Thus, two classes might implement the same *interface* in different ways, but each class still supports the same set of methods. Therefore, code that has knowledge of the *interface* can use objects of either class since the *interface* to those objects is the same. By providing the *interface*, C# allows you to fully utilize the “one interface, multiple methods” aspect of polymorphism.

Interfaces are declared by using the interface keyword. Here is a simplified form of an interface declaration:

```
interface name {
    ret-type method-name1(param-list);
    ret-type method-name2(param-list);
    // ...
    ret-type method-nameN(param-list);
}
```

The name of the interface is specified by name. Methods are declared using only their return type and signature. They are, essentially, abstract methods. As explained, in an interface, no method can have an implementation. Thus, each class that includes an interface must implement all of the methods. In an interface, methods are implicitly public, and no explicit access specifier is allowed.

Here is an example of an interface. It specifies the interface to a class that generates a series of numbers.

```
public interface ISeries {
    int GetNext(); // return next number in series
    void Reset(); // restart
    void SetStart(int x); // set starting value
}
```

The name of this interface is ISeries. Although the prefix I is not necessary, many programmers prefix interfaces with I to differentiate them from classes. ISeries is declared public so that it can be implemented by any class in any program.

In addition to methods, interfaces can specify properties, indexers, and events. Events are described in Chapter 15, and we will be concerned with only methods, properties, and indexers here. Interfaces cannot have data members. They cannot define constructors, destructors, or operator methods. Also, no member can be declared as static.

### Implementing Interfaces

Once an interface has been defined, one or more classes can implement that interface. To implement an interface, the name of the interface is specified after the class name in just the same way that a base class is specified. The general form of a class that implements an interface is shown here:

```
class class-name : interface-name {
    // class-body
}
```

The name of the interface being implemented is specified in interface-name. When a class implements an interface, the class must implement the entire interface. It cannot pick and choose which parts to implement, for example.

A class can implement more than one interface. When a class implements more than one interface, specify each interface in a comma-separated list. A class can inherit a base class and also implement one or more interfaces. In this case, the name of the base class must come first in the comma-separated list.

The methods that implement an interface must be declared public. The reason for this is that methods are implicitly public within an interface, so their implementation must also be public. Also, the return type and signature of the implementing method must match exactly the return type and signature specified in the interface definition.

Here is an example that implements the ISeries interface shown earlier. It creates a class called ByTwos, which generates a series of numbers, each two greater than the previous one.

```
// Implement ISeries.
class ByTwos : ISeries {
    int start;
    int val;

    public ByTwos() {
        start = 0;
        val = 0;
    }

    public int GetNext() {
        val += 2;
        return val;
    }

    public void Reset() {
        val = start;
    }

    public void SetStart(int x) {
        start = x;
        val = start;
    }
}
```

As you can see, ByTwos implements all three methods defined by ISeries. As explained, this is necessary since a class cannot create a partial implementation of an interface.

Here is a class that demonstrates ByTwos:

```
// Demonstrate the ByTwos interface.

using System;

class SeriesDemo {
    static void Main() {
        ByTwos ob = new ByTwos();

        for(int i=0; i < 5; i++)
            Console.WriteLine("Next value is " +
              ob.GetNext());

        Console.WriteLine("\nresetting");
        ob.Reset();
        for(int i=0; i < 5; i++)
            Console.WriteLine("Next value is " +
              ob.GetNext());
    }
}
```

```
Console.WriteLine("\nStarting at 100");
ob.SetStart(100);
for(int i=0; i < 5; i++)
    Console.WriteLine("Next value is " +
        ob.GetNext());
}
```

To compile **SeriesDemo**, you must include the files that contain **ISeries**, **ByTwos**, and **SeriesDemo** in the compilation. The compiler will automatically compile all three files to create the final executable. For example, if you called these files **ISeries.cs**, **ByTwos.cs**, and **SeriesDemo.cs**, then the following command line will compile the program:

```
>csc SeriesDemo.cs ISeries.cs ByTwos.cs
```

If you are using the Visual C++ IDE, simply add all three files to your C# project. One other point: It is perfectly valid to put all three of these classes in the same file, too.

The output from this program is shown here:

```
Next value is 2
Next value is 4
Next value is 6
Next value is 8
Next value is 10

Resetting
Next value is 2
Next value is 4
Next value is 6
Next value is 8
Next value is 10

Starting at 100
Next value is 102
Next value is 104
Next value is 106
Next value is 108
Next value is 110
```

It is both permissible and common for classes that implement interfaces to define additional members of their own. For example, the following version of **ByTwos** adds the method **GetPrevious()**, which returns the previous value:

```
// Implement ISeries and add GetPrevious().
class ByTwos : ISeries {
    int start;
    int val;
    int prev;

    public ByTwos() {
        start = 0;
        val = 0;
        prev = -2;
    }
```

```
public int GetNext() {
    prev = val;
    val += 2;
    return val;
}

public void Reset() {
    val = start;
    prev = start - 2;
}

public void SetStart(int x) {
    start = x;
    val = start;
    prev = val - 2;
}

// A method not specified by ISeries.
public int GetPrevious() {
    return prev;
}
```

Notice that the addition of **GetPrevious()** required a change to the implementations of the methods defined by **ISeries**. However, since the interface to those methods stays the same, the change is seamless and does not break preexisting code. This is one of the advantages of interfaces.

As explained, any number of classes can implement an **interface**. For example, here is a class called **Primes** that generates a series of prime numbers. Notice that its implementation of **ISeries** is fundamentally different than the one provided by **ByTwos**.

```
// Use ISeries to implement a series of prime numbers.
class Primes : ISeries {
    int start;
    int val;

    public Primes() {
        start = 2;
        val = 2;
    }

    public int GetNext() {
        int i, j;
        bool isprime;

        val++;
        for(i = val; i < 1000000; i++) {
            isprime = true;
            for(j = 2; j <= i/j; j++) {
                if((i%j)==0) {
                    isprime = false;
                    break;
                }
            }
        }
    }
}
