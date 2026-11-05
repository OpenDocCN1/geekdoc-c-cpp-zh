
```csharp
{
    // Skip if 2
    if (number == 2)
        continue;

    // Stop iteration if 5
    if (number == 5)
        break;

    Console.Write(number + ", ");
}

// Prints: 1, 3, 4,
```

[Live Demo on .NET Fiddle](https://dotnetfiddle.net/)

Notice that the order of iteration is guaranteed *only* for certain collections such as arrays and List, but **not** guaranteed for many other collections.

† While `IEnumerable` is typically used to indicate enumerable collections, `foreach` only requires that the collection expose publicly the `object GetEnumerator()` method, which should return an object that exposes the `bool MoveNext()` method and the `object Current { get; }` property.

## Section 52.20: dynamic

The `dynamic` keyword is used with dynamically typed objects. Objects declared as `dynamic` forego compile-time static checks, and are instead evaluated at runtime.

```csharp
using System;
using System.Dynamic;

dynamic info = new ExpandoObject();
info.Id = 123;
info.Another = 456;

Console.WriteLine(info.Another);
// 456

Console.WriteLine(info.DoesntExist);
// Throws RuntimeBinderException
```

The following example uses `dynamic` with Newtonsoft's library Json.NET, in order to easily read data from a deserialized JSON file.

```csharp
try
{
    string json = @"{ 'x' : 10, y : ""ho"" }";
    dynamic deserializedJson = JsonConvert.DeserializeObject(json);
    int x = deserializedJson.x;
    string y = deserializedJson.y;
    // int z = deserializedJson.z; // throws RuntimeBinderException
}
catch (RuntimeBinderException e)
{
    // This exception is thrown when a property
    // that wasn't assigned to a dynamic variable is used
}
```

returning). For example:

```csharp
try
{
    connection.Open();
    return connection.Get(query);
}
finally
{
    connection.Close();
}
```

The statement `connection.Close()` will execute before the result of `connection.Get(query)` is returned.

## Section 52.22: void

The reserved word `void` is an alias of `System.Void` type, and has two uses:

- 1. Declare a method that doesn't have a return value:

```csharp
public void DoSomething()
{
    // Do some work, don't return any value to the caller.
}
```

A method with a return type of `void` can still have the `return` keyword in its body. This is useful when you want to exit the method's execution and return the flow to the caller:

```csharp
public void DoSomething()
{
    // Do some work...

    if (condition)
        return;

    // Do some more work if the condition evaluated to false.
}
```

- 2. Declare a pointer to an unknown type in an unsafe context.

In an unsafe context, a type may be a pointer type, a value type, or a reference type. A pointer type declaration is usually `type* identifier`, where the type is a known type - i.e `int* myInt`, but can also be `void* identifier`, where the type is unknown.

Note that declaring a `void` pointer type is [discouraged by Microsoft](#).

## Section 52.23: namespace

The `namespace` keyword is an organization construct that helps us understand how a codebase is arranged. Namespaces in C# are virtual spaces rather than being in a physical folder.

```csharp
namespace StackOverflow
{
    namespace Documentation
    {
        namespace CSharp.Keywords
        {
```

```csharp
public class Program
{
    public static void Main()
    {
        Console.WriteLine(typeof(Program).Namespace);
        //StackOverflow.Documentation.CSharp.Keywords
    }
}
```

Namespaces in C# can also be written in chained syntax. The following is equivalent to above:

```csharp
namespace StackOverflow.Documentation.CSharp.Keywords
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine(typeof(Program).Namespace);
            //StackOverflow.Documentation.CSharp.Keywords
        }
    }
}
```

## Section 52.24: ref, out

The `ref` and `out` keywords cause an argument to be passed by reference, not by value. For value types, this means that the value of the variable can be changed by the callee.

```csharp
int x = 5;
ChangeX(ref x);
// The value of x could be different now
```

For reference types, the instance in the variable can not only be modified (as is the case without `ref`), but it can also be replaced altogether:

```csharp
Address a = new Address();
ChangeFieldInAddress(a);
// a will be the same instance as before, even if it is modified
CreateANewInstance(ref a);
// a could be an entirely new instance now
```

The main difference between the `out` and `ref` keyword is that `ref` requires the variable to be initialized by the caller, while `out` passes that responsibility to the callee.

To use an `out` parameter, both the method definition and the calling method must explicitly use the `out` keyword.

```csharp
int number = 1;
Console.WriteLine("Before AddByRef: " + number); // number = 1
AddOneByRef(ref number);
Console.WriteLine("After AddByRef: " + number); // number = 2
SetByOut(out number);
Console.WriteLine("After SetByOut: " + number); // number = 34

void AddOneByRef(ref int value)
{
    value++;
}
void SetByOut(out int value)
{
    value = 34;
}
```

Live Demo on .NET Fiddle

The following does not compile, because out parameters must have a value assigned before the method returns (it would compile using ref instead):

```csharp
void PrintByOut(out int value)
{
    Console.WriteLine("Hello!");
}
```

### using out keyword as Generic Modifier

out keyword can also be used in generic type parameters when defining generic interfaces and delegates. In this case, the out keyword specifies that the type parameter is covariant.

> Covariance enables you to use a more derived type than that specified by the generic parameter. This allows for implicit conversion of classes that implement variant interfaces and implicit conversion of delegate types. Covariance and contravariance are supported for reference types, but they are not supported for value types. - MSDN

```
//if we have an interface like this
interface ICovariant<out R> { }

//and two variables like
ICovariant<Object> iobj = new Sample<Object>();
ICovariant<String> istr = new Sample<String>();
// then the following statement is valid
// without the out keyword this would have thrown error
iobj = istr; // implicit conversion occurs here
```

## Section 52.25: base

The base keyword is used to access members from a base class. It is commonly used to call base implementations of virtual methods, or to specify which base constructor should be called.

### Choosing a constructor

```csharp
public class Child : SomeBaseClass {
    public Child() : base("some string for the base class")
    {
    }
}
public class SomeBaseClass {
    public SomeBaseClass()
    {
        // new Child() will not call this constructor, as it does not have a parameter
    }
    public SomeBaseClass(string message)
    {
        // new Child() will use this base constructor because of the specified parameter in Child's constructor
        Console.WriteLine(message);
    }
}
```

### Calling base implementation of virtual method

```csharp
public override void SomeVirtualMethod() {
    // Do something, then call base implementation
    base.SomeVirtualMethod();
}
```

It is possible to use the base keyword to call a base implementation from any method. This ties the method call directly to the base implementation, which means that even if new child classes override a virtual method, the base implementation will still be called so this needs to be used with caution.

```csharp
public class Parent
{
    public virtual int VirtualMethod()
    {
        return 1;
    }
}

public class Child : Parent
{
    public override int VirtualMethod() {
        return 11;
    }

    public int NormalMethod()
    {
        return base.VirtualMethod();
    }

    public void CallMethods()
    {
        Assert.AreEqual(11, VirtualMethod());

        Assert.AreEqual(1, NormalMethod());
        Assert.AreEqual(1, base.VirtualMethod());
    }
}

public class GrandChild : Child
{
    public override int VirtualMethod()
    {
        return 21;
    }

    public void CallAgain()
    {
        Assert.AreEqual(21, VirtualMethod());
        Assert.AreEqual(11, base.VirtualMethod());
    }
}
```
