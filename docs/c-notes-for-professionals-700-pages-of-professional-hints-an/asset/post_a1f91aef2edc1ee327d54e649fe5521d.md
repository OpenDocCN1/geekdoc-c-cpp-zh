
View Demo

Calling a different constructor of the base class is done by placing : base(args) between the constructor's signature and its body:

```csharp
public class Mammal : Animal
{
    public Mammal(string name) : base(name)
    {
        Console.WriteLine(name + " is a mammal.");
    }
}
```

Calling new Mammal("George the Cat") will now print:

> George the Cat gets born.
> George the Cat is a mammal.

View Demo

### Section 39.7: Finalizers on derived classes

When an object graph is finalized, the order is the reverse of the construction. E.g. the super-type is finalized before the base-type as the following code demonstrates:

```csharp
class TheBaseClass
{
    ~TheBaseClass()
    {
        Console.WriteLine("Base class finalized!");
    }
}

class TheDerivedClass : TheBaseClass
{
    ~TheDerivedClass()
    {
        Console.WriteLine("Derived class finalized!");
    }
}

//Don't assign to a variable
//to make the object unreachable
new TheDerivedClass();

//Just to make the example work;
//this is otherwise NOT recommended!
GC.Collect();

//Derived class finalized!
//Base class finalized!
```

### Section 39.8: Exceptions in static constructors

If a static constructor throws an exception, it is never retried. The type is unusable for the lifetime of the AppDomain. Any further usages of the type will raise a TypeInitializationException wrapped around the original exception.

```csharp
public class Animal
{
    static Animal()
    {
        Console.WriteLine("Static ctor");
        throw new Exception();
    }

    public static void Yawn() {}
}
try
{
    Animal.Yawn();
}
catch (Exception e)
{
    Console.WriteLine(e.ToString());
}
try
{
    Animal.Yawn();
}
catch (Exception e)
{
    Console.WriteLine(e.ToString());
}
```

This will output:

> Static ctor
> 
> System.TypeInitializationException: The type initializer for 'Animal' threw an exception. --->
> System.Exception: Exception of type 'System.Exception' was thrown.

[...]

> System.TypeInitializationException: The type initializer for 'Animal' threw an exception. --->
> System.Exception: Exception of type 'System.Exception' was thrown.

where you can see that the actual constructor is only executed once, and the exception is re-used.

### Section 39.9: Constructor and Property Initialization

Shall the property value's assignment be executed before or after the class' constructor?

```csharp
public class TestClass
{
    public int TestProperty { get; set; } = 2;

    public TestClass()
    {
        if (TestProperty == 1)
        {
            Console.WriteLine("Shall this be executed?");
        }
        if (TestProperty == 2)
        {
            Console.WriteLine("Or shall this be executed");
        }
    }
}
var testInstance = new TestClass() { TestProperty = 1 };
```

In the example above, shall the TestProperty value be 1 in the class' constructor or after the class constructor?

Assigning property values in the instance creation like this:

```csharp
var testInstance = new TestClass() { TestProperty = 1 };
```

Will be executed after the constructor is run. However, initializing the property value in the class' property in C# 6.0 like this:

```csharp
public class TestClass
{
    public int TestProperty { get; set; } = 2;

    public TestClass()
    {
    }
}
```

will be done before the constructor is run.

Combining the two concepts above in a single example:

```csharp
public class TestClass
{
    public int TestProperty { get; set; } = 2;

    public TestClass()
    {
        if (TestProperty == 1)
        {
            Console.WriteLine("Shall this be executed?");
        }

        if (TestProperty == 2)
        {
            Console.WriteLine("Or shall this be executed");
        }
    }
}

static void Main(string[] args)
{
    var testInstance = new TestClass() { TestProperty = 1 };
    Console.WriteLine(testInstance.TestProperty); //resulting in 1
}
```

Final result:

```
"Or shall this be executed"
"1"
```

Explanation:

The TestProperty value will first be assigned as 2, then the TestClass constructor will be run, resulting in printing of

```
"Or shall this be executed"
```

And then the TestProperty will be assigned as 1 due to new TestClass() { TestProperty = 1 }, making the final value for the TestProperty printed by Console.WriteLine(testInstance.TestProperty) to be

```
"1"
```

### Section 39.10: Generic Static Constructors

If the type on which the static constructor is declared is generic, the static constructor will be called once for each unique combination of generic arguments.

```csharp
class Animal<T>
{
    static Animal()
    {
        Console.WriteLine(typeof(T).FullName);
    }
    public static void Yawn() { }
}
Animal<Object>.Yawn();
Animal<String>.Yawn();
```

This will output:

System.Object
System.String

See also How do static constructors for generic types work ?

### Section 39.11: Calling virtual methods in constructor

Unlike C++ in C# you can call a virtual method from class constructor (OK, you can also in C++ but behavior at first is surprising). For example:

```csharp
abstract class Base
{
    protected Base()
    {
        _obj = CreateAnother();
    }

    protected virtual AnotherBase CreateAnother()
    {
        return new AnotherBase();
    }

    private readonly AnotherBase _obj;
}

sealed class Derived : Base
{
    public Derived() { }

    protected override AnotherBase CreateAnother()
    {
        return new AnotherDerived();
    }
}

var test = new Derived();
// test._obj is AnotherDerived
```

If you come from a C++ background this is surprising, base class constructor already sees derived class virtual method table!

**Be careful:** derived class may not been fully initialized yet (its constructor will be executed after base class constructor) and this technique is dangerous (there is also a StyleCop warning for this). Usually this is regarded as bad practice.

## Chapter 40: Access Modifiers

### Section 40.1: Access Modifiers Diagrams

Here are all access modifiers in venn diagrams, from more limiting to more accessible:

| Access Modifier | Diagram |
|---|---|
| private | Venn diagram with Derived and Same Assembly circles overlapping, Me in the overlap, private area highlighted |
| internal | Venn diagram with Derived and Same Assembly circles overlapping, Me in the overlap, Same Assembly area highlighted |
| protected | Venn diagram with Derived and Same Assembly circles overlapping, Me in the overlap, Derived area highlighted |
| protected internal | Venn diagram with Derived and Same Assembly circles overlapping, Me in the overlap, Derived and Same Assembly areas highlighted |

![](img/5da9b5c72747b887ec63f57c832400bf_184_0.png)

![](img/5da9b5c72747b887ec63f57c832400bf_184_1.png)

![](img/5da9b5c72747b887ec63f57c832400bf_184_2.png)

![](img/5da9b5c72747b887ec63f57c832400bf_184_3.png)

![](img/5da9b5c72747b887ec63f57c832400bf_185_0.png)

Below you could find more information.

### Section 40.2: public

The public keyword makes a class (including nested classes), property, method or field available to every consumer:

```csharp
public class Foo
{
    public string SomeProperty { get; set; }

    public class Baz
    {
        public int Value { get; set; }
    }
}

public class Bar
{
    public Bar()
    {
        var myInstance = new Foo();
        var someValue = foo.SomeProperty;
        var myNestedInstance = new Foo.Baz();
        var otherValue = myNestedInstance.Value;
    }
}
```

### Section 40.3: private

The private keyword marks properties, methods, fields and nested classes for use inside the class only:

```csharp
public class Foo
{
    private string someProperty { get; set; }

    private class Baz
    {
        public string Value { get; set; }
    }

    public void Do()
    {
        var baz = new Baz { Value = 42 };
    }
}
```

```csharp
public class Bar
{
    public Bar()
    {
        var myInstance = new Foo();

        // Compile Error - not accessible due to private modifier
        var someValue = foo.someProperty;
        // Compile Error - not accessible due to private modifier
        var baz = new Foo.Baz();
    }
}
```

### Section 40.4: protected internal

The `protected internal` keyword marks field, methods, properties and nested classes for use inside the same assembly or derived classes in another assembly.

> > Assembly 1

```csharp
public class Foo
{
    public string MyPublicProperty { get; set; }
    protected internal string MyProtectedInternalProperty { get; set; }

    protected internal class MyProtectedInternalNestedClass
    {
        private string blah;
        public int N { get; set; }
    }
}

public class Bar
{
    void MyMethod1()
    {
        Foo foo = new Foo();
        var myPublicProperty = foo.MyPublicProperty;
        var myProtectedInternalProperty = foo.MyProtectedInternalProperty;
        var myProtectedInternalNestedInstance =
            new Foo.MyProtectedInternalNestedClass();
    }
}
```

> > Assembly 2

```csharp
public class Baz : Foo
{
    void MyMethod1()
    {
        var myPublicProperty = MyPublicProperty;
        var myProtectedInternalProperty = MyProtectedInternalProperty;
        var thing = new MyProtectedInternalNestedClass();
    }

    void MyMethod2()
```
