
referenced. At the same time, there are certain limitations to the static constructor as in the following:

- Static constructors are parameterless.
- Static constructors can’t be overloaded.
- There is no accessibility specified for Static constructors.

In the following example, the customer class has a static constructor that initializes the static field, and this constructor is called when the class is referenced in the Main() at line 26 as in the following.

```
using System;
namespace oops
{
    class customer
    {
        // Member Variables
        static private int x;
        //constructor for static initializing fields
        static customer()
        {
            x = 10;
        }
        //method for get static field
        static public void getData()
        {
            Console.WriteLine(x);
        }
        //Entry point
        static void Main(string[] args)
        {
            //static Method calling
            customer.getData();
        }
    }
}
```

## Destructors

The purpose of the destructor method is to get rid of unused objects and resources. Destructors are not called during garbage collection. Similar to a constructor, the destructor has the same name as the class, except a destructor is prefixed with a tilde (~). There are some limitations to destructors as in the following:

- Destructors are parameterless.
- A destructor can’t be overloaded.
- Destructors are not inherited.
- Destructors can cause performance and efficiency implications.

The following is an implementation of a destructor and dispose method. First of all, we are initializing the fields via constructor, doing some calculations on that data, and sending it to the console. But at line 9, we are introducing

```
y = 0;
}
//destructor
~customer()
{
    Dispose();
}
//Entry point
static void Main(string[] args)
{
    //instance created
    customer obj = new customer();

    obj.getData();
}
}
```

## Function Overloading

Function overloading runs multiple implementations of the same function in a class. Overloaded methods have the same name but different specific signature. The number of parameters, types of parameters, or both should not be the same. A function can’t be overloaded on the basis of a dissimilar return type alone:

```
using System;
namespace oops
{
    class funOverload
    {
        public string name;

        //overloaded functions
        public void setName(string last)
        {
            name = last;
        }

        public void setName(string first,
        string last)
        {
            name = first + " " + last;
        }

        public void setName(string first,
        string middle, string last)
        {
            name = first + " " + middle +
        " " + last;
        }

        //Entry point
        static void Main(string[] args)
        {
            funOverload obj = new funOverload();

            obj.setName("barack");
            obj.setName("barack ","obama ");
            obj.setName("barack ","hussein","obama");
        }
    }
}
```

At lines 3, 4, and 5, we are defining three methods with the same name but with different parameters. In the Main(), you create an instance of the class and call the functions setName() via obj at lines 7, 8, and 9, then IntelliSense will show forward signatures automatically.

## Virtual Methods

By declaring a base class function as virtual, you allow the function to be overridden in any derived class. The idea behind a virtual function is to redefine the implementation of the base class method in the derived class as needed. If a method is virtual in the base class, then we need to give the override keyword in the derived class. Neither member fields nor static functions can be declared as virtual. To demonstrate with an example:

```
using System;
namespace oops
{
    class myBase
    {
        //virtual function
        public virtual void VirtualMethod()
        {
            Console.WriteLine("virtual method defined in the base class");
        }
    }

    class myDerived : myBase
    {
        // redefining the implementation of base class method
        public override void VirtualMethod()
        {
            Console.WriteLine("virtual method defined in the Derived class");
        }
    }
    class virtualClass
    {
        static void Main(string[] args)
        {
            // class instance
            new myDerived().VirtualMethod();
            Console.ReadKey();
        }
    }
}
```

## Hiding Methods

If a method with the same signature is declared in both base and derived classes, but the methods are not declared as virtual and overridden, respectively, then the derived class version is said to hide the base class version. In most cases, you would need to override methods rather than hide them. Otherwise, .NET automatically generates a warning.

In the following example, we are defining a VirtualMethod() in the myBase class but not overriding it in the derived class, so in that case, the compiler will generate a warning. The compiler will think that you are hiding the base class method. So to overcome that problem, if you prefix the new keyword in the derived class method, then the compiler will select the most derived version method:

```
using System;
namespace oops
{
    class myBase
    {
        //virtual function
        public virtual void VirtualMethod()
        {
            Console.WriteLine("virtual method defined in the base class");
        }
    }

    class myDerived : myBase
    {
        // hiding the implementation of base class method
        public new void VirtualMethod()
        {
            Console.WriteLine("virtual method defined in the Derived class");

            //still access the base class method
            base.VirtualMethod();
        }
    }
    class virtualClass
    {
        static void Main(string[] args)
        {
            // class instance
            new myDerived().VirtualMethod();
            Console.ReadKey();
        }
    }
}
```

## Abstract Classes

C# allows both classes and functions to be declared using the abstract keyword. You can’t make an instance of an abstract class. An abstract member has its own signature, but does not have a function body, and they should be overridden in any non-abstract derived class. Abstract classes exist primarily for inheritance. Member functions, properties, and indexers can be abstract. A class with one or more abstract members must be abstract as well. However, static members can’t be abstract.

In the following example, we are declaring an abstract class Employees with a method displayData() that does not have an implementation. Then we implement the displayData() body in the derived class. One point to be mentioned here is that we have to prefix the abstract method with the override keyword in the derived class.¹¹

```
using System;
namespace oops
{
    //abstract class
    public abstract class Employees
```

classes are not extensible, so in that case, those classes are marked as sealed:

```
using System;
namespace oops
{
    sealed class SealedClass
    {
        void myfunv();
    }

    public class test : SealedClass // wrong. will give a compilation error
    {
    }
}
```

## Interface

An interface is a set of related functions that must be implemented in a derived class. Interfaces are similar to abstract classes. First, both types must be inherited; second, you cannot create an instance of either. Although there are several differences as in the following:

- An Abstract class can contain some implementations, but an interface can’t.
- An Interface can only inherit other interfaces, but abstract classes can inherit from other classes and interfaces.
- An Abstract class can contain constructors and destructors, but an interface can’t.
- An Abstract class contains fields, but interfaces don’t.

```
static void Main(string[] args)
{
    test obj = new test();
    obj.methodA();
    obj.methodB();
}
}
```

## ENCAPSULATION AND INHERITANCE

Encapsulation is defined as the wrapping up of data under a single unit. It is the mechanism that stitches together code and the data it manipulates. Differently, encapsulation is a protective shield that stops the data from being accessed by the code outside this shield.

Technically in encapsulation, the variables or data of a class are hidden from any other class and can be obtained only through any member function of its class in which they are declared.

Encapsulation can be attained by: Declaring all the variables in the class as private and using C# Properties in the class to set and get the values of variables. For example:

```
// C# program to illustrate encapsulation
using System;

public class DemoEncap {

    // private variables declared
    // these can only be accessed by
    // public methods of class
```
