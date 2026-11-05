
// Create a class derived from Media.
class Book : Media {
    public Book() {
        Console.WriteLine("Constructing Book.");
    }
}

// Create a class derived from Book.
class Booklet : Book {
    public Booklet() {
        Console.WriteLine("Constructing Booklet.");
    }
}

class OrderOfConstructorCall {
    static void Main() {
        Booklet bkl = new Booklet();
    }
}

Input

Nil

## Output

```
Constructing Media.
Constructing Book.
Constructing Booklet.
```

## 2. Calling base class constructor in C#

During inheritance, if the base class contains only parameterized constructor, then derived class must contain a parameterized constructor even if it doesn't need one. In this case while creating parameterized constructor in derived class, one should specify the parameters required for derived class along with the parameters required for base class constructor and to pass arguments to base class constructor, using the keyword "base" at the end of parameterized constructor declaration in derived class preceded with ":".

If one derives a class from a base class and want to pass data from the constructor of the derived class to the constructor of the base class, it is necessary to call base constructor.

In the inheritance hierarchy, always the base class constructor is called first. In c#, the base keyword is used to access the base class constructor as shown below.

```
class Acc
{
private string accCode;
private string accName;
private string accDescription;
private double accBalance;

public Acc(string cd, string nm, string descrip, double bal)
{
    accCode = cd;
    accName = nm;
    accDescription = descrip;
    accBalance = bal;
}
public Acc()
{

}

class LoanAcc : Acc
{
    private string accAddr;
    private string accContact;
    public LoanAcc(string cd, string nm, string descrip, double bal, string adr, string cont)
        : base(cd, nm, descrip, bal)
    {
        accAddr = adr;
        accContact = cont;
    }

    public LoanAcc()
        : base()
    {

    }
}

/* The above two constructors are written to initialize base class members. The
parameterless constructor of the base class is executed when the class is instantiate
without passing any parameters. The other base class constructor is executed when
parameters are passed while instantiating the object. */
```

## 3. Private Constructors

Private constructors are the constructors with the "private" access modifier. If there is private constructor in the class, then, one can neither create the object of the class, nor can inherit the class.

There can be public constructors along with the private constructors in the class and the public constructors can access the private constructors from within the class through constructor chaining.

```csharp
public class DemoClass
{
    private DemoClass()
    {
        Console.WriteLine("This is no parameter Constructor");
    }

    public DemoClass(int var):this()
    {
        Console.WriteLine("This is one parameter Constructor");
    }
}
....
}

//object of DemoClass is created as below.

DemoClass ob = new DemoClass(10);
//The above statement works fine, but the statement
DemoClass ob = new MyClass();

raises an error :
'Constructors.DemoClass.DemoClass()' is inaccessible due to its protection level
```

## When to use class with only private constructor

It is possible to have the class with only the private constructors. Main use is in the case when there are only static members in the class and class would never be instantiated.

## 4. Initialization in Static Constructors

- 1. A static constructor is used to initialize any static data, or to perform a particular action that needs to be performed once only.
- 2. Static constructor is called automatically before the first instance is created or any static members are referenced.
- 3. There can be only one static constructor in the class as overloading needs the two methods to be different in terms of methods definition, which cannot be done with static Constructors.
- 4. The static constructor should be without parameters, as it is going to be called by CLR, there is no way to pass the parameters to it from program, if required.

5. It can only access the static members of the class because non-static members in the class are specific to the object instance. So static constructor, if allowed to work on non-static members, will reflect the changes in all the object instances, which is not possible.

6. There should be no access modifier in static constructor definition because the call to the static method is made by the CLR and not by the object.

```
class ConstructorCall
{
// Static constructor

    static ConstructorCall ()
    {
    // static constructor is called first then instance constructor.

        Console.WriteLine("Static constructor is being in process.");
    }

//instance constructor
public ConstructorCall ()
{

    Console.WriteLine("Instance constructor invoked");
}

}

class OrderOfConstructors
{
public static void Main()
{
    ConstructorCall ct =new ConstructorCall();
}

}
```

Input
Nil

## Output

```
Static constructor is being in process.
Instance constructor invoked
```

## 5. Order of Finalizers(or destructors) in inheritance hierarchy

Destructor execution follows the opposite approach as that of constructor execution order; the derived class destructor is called first then the base class. Destructor implicitly calls Finalize on the base class of object.

### Example

```csharp
using System;

public class Base
{
    ~Base()
    {
        Console.WriteLine("Base destructor called");
    }
}

public class Derived : Base
{
    ~Derived()
    {
        Console.WriteLine("Derived destructor called");
    }
}

public class MainClass
{
    static void Main()
    {
        Derived derived = new Derived();
    }
}

Input
Nil
```

## Output

```
```text
Derived destructor called
Base destructor called
```
```

## 9.1.7 What is not being Inherited ?

**Sealed and abstract classes are never inherited.**

**Constructor and destructor are never inherited.**

## 9.1.8 Application of Inheritance

Situation where in inheritance is useful in the application

- 1. When there are classes that have certain common and certain uncommon properties then inheritance is handy to encapsulate common features in base class.
- 2. A new class need the properties of some existing class which provides extension to it.
- 3. To implement relationships amongst the objects, which are, is-a, is-a-kind, is-a-like.
- 4. To implement more general class or to implement more specialized class is the main goal of inheritance. This in turn provides combination of multiple classes.

## 9.2 Polymorphism and Runtime Behaviours

### Concept

- 1. The term polymorphism (from the Greek meaning "having multiple forms") in OO is the characteristic of being able to assign a different meaning or application to same statement or something, in different contexts – programmatically, to allow a variable to refer to more than one type of object.

### Explanation

- 2. Polymorphism provides following features
- - It allows to invoke methods of derived class through base class reference during runtime.
- - It has the ability for classes to provide different implementations of methods that are called through the same name.

- 3. Polymorphism is of two types namely,
- 1. Compile time polymorphism/Overloading
- 2. Runtime polymorphism/Overriding

![](img/3005a4307e6d8f3bb7e76eea28a92357_278_0.png)

## 4. Compile Time Polymorphism (Static polymorphism)

Compile time polymorphism is implemented using method and operator overloading. It is also termed as early binding.

In method overloading method performs the different task using different input parameters.

## 5. Runtime Time Polymorphism (Dynamic polymorphism)

C# provides runtime polymorphism through inheritance, overriding and virtual method.

Inheritance-based polymorphism allows to define method in a base class and override it in derived class with implementation. Thus, if a base class object that can hold derived class objects, polymorphism, when properly used, allows to call a method that will work differently according to the type of derived class the object belongs to.

Many times method overriding is called runtime polymorphism. It is also termed as late binding.

When overriding a method, the behavior of the method is changed for the derived class.

Overloading a method simply involves having another method with the same prototype.

It should be clearly remembered that method overloading and method overriding are different, unrelated concepts.

Method overloading has nothing to do with inheritance or virtual methods.

## 6. Method overloading – Why and When

- 1. Method overloading is used in situation where it is required that a class method performs some task, but there is more than one possibility for what information is supplied to the method that carries out the task.
- 2. Overloading a method should be considered when for some reason there are a couple of methods that take different parameters, but conceptually do the same thing. OOP would strongly recommend it as a good programming practice.
- 3. Keeping the same method name, method overloading can be achieved,
- - By changing the number of parameters used.
- - By changing the order of parameters.
- - By using different data types for the parameters.
- 4. While doing method overloading there are certain restrictions that the compiler imposes.

The basic rule is that overloaded methods must be different in their signature, which means the name and the number and type of parameters. This is necessary for compiler to distinguish the overloaded methods.
