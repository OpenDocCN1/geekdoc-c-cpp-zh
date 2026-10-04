
You can even adjust the access levels of the get and set portions of an accessor individually. Suppose that you don’t want to expose the set accessor outside your class — it’s for internal use only. You can write the property like this:

```
internal string Name { get; private set; }
```

The AccessorPropertyShortcuts example at csharp102.info illustrates this usage.

# Getting Your Objects Off to a Good Start — Constructors

Controlling class access is only half the problem: An object needs a good start in life if it is to grow. A class can supply an initialization method that the application calls to get things started, but the application could forget to call the method. The class starts out with garbage, and the situation gets no better after that. If you want to hold the class accountable, you have to ensure that it has a chance to start out correctly.

C# solves that problem by calling the initialization method for you — for example:

```
MyObject mo = new MyObject();
```

In other words, this statement not only grabs an object from a special memory area, but it also initializes that object’s members.

Keep the terms class and object separate in your mind. Cat is a class. My cat Striper is an object of class Cat.

# The C#-Provided Constructor

C# keeps track of whether a variable has been initialized and doesn’t allow you to use an uninitialized variable. For example, the following code chunk generates a compile-time error:

```
public static void Main(string[] args)
{
    int n;
    double d;
    double calculatedValue = n + d;
}
```

C# tracks the fact that the local variables n and d haven’t been assigned a value and doesn’t allow them to be used in the expression. Compiling this tiny program generates these compiler errors:

```
Use of unassigned local variable 'n'
Use of unassigned local variable 'd'
```

By comparison, C# provides a *default constructor* that initializes the *data members* of an object to:

- 0 for numbers
- false for Booleans
- null for object references

Consider the following simple program example:

```c
using System;
namespace Test
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // First create an object.
            MyObject localObject = new MyObject();
            Console.WriteLine("localObject.n is {0}", localObject.n);
            if (localObject.nextObject == null)
            {
                Console.WriteLine("localObject.nextObject is null");
            }
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
    public class MyObject
    {
        internal int n;
        internal MyObject nextObject;
    }
}
```

This program defines a class `MyObject`, which contains both a simple data member `n` of type `int` and a reference to an object, `nextObject` (both declared `internal`). The `Main()` method creates a `MyObject` and then displays the initial contents of `n` and `nextObject`.

The output from executing the program appears this way:

```
localObject.n is 0
localObject.nextObject is null
Press Enter to terminate...
```

When the object is created, C# executes a small piece of code that the compiler provides to initialize the object and its members. Left to their own devices, the data members `localObject.n` and `nextObject` would contain random, garbage values.

![](img/6df7bb88e9302e98442acc219cfbd7fc_296_0.png)

The code that initializes values when they’re created is the default constructor. It “constructs” the class, in the sense of initializing its members. Thus C# ensures that an object starts life in a known state: all zeroes. This concept affects only data members of the class, not local variables in a method.

# Replacing the Default Constructor

Although the compiler automatically initializes all instance variables to zeroes, for many classes (probably most classes), all zeroes isn’t a valid state. Consider the following BankAccount class from earlier in this chapter:

```csharp
public class BankAccount
{
    private int _accountNumber;
    private double _balance;
    // ...other members
}
```

Although an initial balance of 0 is probably okay, an account number of 0 definitely isn’t the hallmark of a valid bank account.

At this point in the chapter, the BankAccount class includes the InitBankAccount() method to initialize the object. However, this approach puts too much responsibility on the application software using the class. If the application fails to invoke the InitBankAccount() method, the bank account methods may not work, through no fault of their own.

![](img/6df7bb88e9302e98442acc219cfbd7fc_296_1.png)

A class shouldn’t rely on external methods such as InitBankAccount() to start the object in a valid state.

To work around this problem, you can have your class provide its own explicit class constructor that C# calls automatically when the object is created. The constructor could have been named Init(), Start(), or Create(), but C# requires the constructor to carry the name of the class. Thus a constructor for the BankAccount class appears this way:

```csharp
public void Main(string[] args)
{
    BankAccount ba = new BankAccount();  // This invokes the constructor.
}
public class BankAccount
{
    // Bank accounts start at 1000 and increase sequentially.
    private int _accountNumber;
    private double _balance;
    // ...
}
```
