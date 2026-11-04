
The following code shows invoking the Divide() method. The items of the tuple can be accessed with the properties Item1 and Item2;

```csharp
var result = Divide(5, 2);
Console.WriteLine("result of division: {0}, remainder: {1}",
    result.Item1, result.Item2);
```

In case you have more than eight items that should be included in a tuple, you can use the Tuple class definition with eight parameters. The last template parameter is named TRest to indicate that you must pass a tuple itself. That way you can create tuples with any number of parameters.

To demonstrate this functionality:

```csharp
public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest>
```

Here, the last template parameter is a tuple type itself, so you can create a tuple with any number of items:

```csharp
var tuple = Tuple.Create<string, string, string, int, int, int, double,
    Tuple<int, int>>(
    "Stephanie", "Alina", "Nagel", 2009, 6, 2, 1.37,
    Tuple.Create<int, int>(52, 3490));
```

## THE DYNAMIC TYPE

The dynamic type allows you to write code that will bypass compile time type checking. The compiler will assume that whatever operation is defined for an object of type dynamic is valid. If that operation isn't valid, the error won't be detected until runtime. This is shown in the following example:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var staticPerson = new Person();
        dynamic dynamicPerson = new Person();
        staticPerson.GetFullName("John", "Smith");
        dynamicPerson.GetFullName("John", "Smith");
    }
}
class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string GetFullName()
    {
        return string.Concat(FirstName, " ", LastName);
    }
}
```

This example will not compile because of the call to staticPerson.GetFullName(). There isn't a method on the Person object that takes two parameters, so the compiler raises the error. If that line of code were to be commented out, the example would compile. If executed, a runtime error would occur. The exception that is raised is `RuntimeBinderException`. The `RuntimeBinder` is the object in the runtime that evaluates the call to see if `Person` really does support the method that was called.

Unlike the `var` keyword, an object that is defined as `dynamic` can change type during runtime. Remember, when the `var` keyword is used, the determination of the object's type is delayed. Once the type is defined, it can't be changed. Not only can you change the type of a dynamic object, you can change it many times. This differs from casting an object from one type to another. When you cast an object you are creating a new object with a different but compatible type. For example, you cannot cast an `int` to a `Person` object. In the following example, you can see that if the object is a `dynamic` object, you can change it from `int` to `Person`:

![](img/7954dcc7dd1d929d072aec8e9531b6cc_11_0.png)

```csharp
dynamic dyn;

dyn = 100;
Console.WriteLine(dyn.GetType());
Console.WriteLine(dyn);

dyn = "This is a string";
Console.WriteLine(dyn.GetType());
Console.WriteLine(dyn);

dyn = new Person() { FirstName = "Bugs", LastName = "Bunny" };
Console.WriteLine(dyn.GetType());
Console.WriteLine("{0} {1}", dyn.FirstName, dyn.LastName);
```

*Pro C# 4.0 9780470502259 code snippet DynamicProgram.cs*

Executing this code would show that the `dyn` object actually changes type from `System.Int32` to `System.String` to `Person`. If `dyn` had been declared as an `int` or `string`, the code would not have compiled.

There are a couple of limitations to the dynamic type. A dynamic object does not support extension methods. Anonymous functions (Lambda expressions) also cannot be used as parameters to a dynamic method call, thus LINQ does not work well with dynamic objects. Most LINQ calls are extension methods and Lambda expressions are used as arguments to those extension methods.

## Dynamic Behind the Scenes

So what's going on behind the scenes to make this happen? C# is still a statically typed language. That hasn't changed. Take a look at the IL (Intermediate Language) that's generated when the `dynamic` type is used.

First, this is the example C# code that you're looking at:

```csharp
using System;

namespace DeCompile
{
    class Program
    {
        static void Main(string[] args)
```

```csharp
{
    StaticClass staticObject = new StaticClass();
    DynamicClass dynamicObject = new DynamicClass();
    Console.WriteLine(staticObject.IntValue);
    Console.WriteLine(dynamicObject.DynValue);
    Console.ReadLine();
}

class StaticClass
{
    public int IntValue = 100;
}

class DynamicClass
{
    public dynamic DynValue = 100;
}
```

You have two classes, StaticClass and DynamicClass. StaticClass has a single field that returns an int. DynamicClass has a single field that returns a dynamic object. The Main method just creates these objects and prints out the value that the methods return. Simple enough.

Now comment out the references to the DynamicClass in Main like this:

```csharp
static void Main(string[] args)
{
    StaticClass staticObject = new StaticClass();
    //DynamicClass dynamicObject = new DynamicClass();
    Console.WriteLine(staticObject.IntValue);
    //Console.WriteLine(dynamicObject.DynValue);
    Console.ReadLine();
}
```

Using the ildasm tool, you can look at the IL that is generated for the Main method:

```text
.method private hidebysig static void Main(string[] args) cil managed
{
  .entrypoint
  // Code size       26 (0x1a)
  .maxstack  1
  .locals init ([0] class DeCompile.StaticClass staticObject)
  IL_0000:  nop
  IL_0001:  newobj     instance void DeCompile.StaticClass::.ctor()
  IL_0006:  stloc.0
  IL_0007:  ldloc.0
  IL_0008:  ldfld      int32 DeCompile.StaticClass::IntValue
  IL_000d:  call       void [mscorlib]System.Console::WriteLine(int32)
  IL_0012:  nop
  IL_0013:  call       string [mscorlib]System.Console::ReadLine()
  IL_0018:  pop
  IL_0019:  ret
} // end of method Program::Main
```

Without going into the details of IL but just looking at this section of code, you can still pretty much tell what's going on. Line 0001, the StaticClass constructor, is called. Line 0008 calls the IntValue field of StaticClass. The next line writes out the value.

Now comment out the StaticClass references and uncomment the DynamicClass references:

```csharp
static void Main(string[] args)
{
    //StaticClass staticObject = new StaticClass();
    DynamicClass dynamicObject = new DynamicClass();
    Console.WriteLine(staticObject.IntValue);
    //Console.WriteLine(dynamicObject.DynValue);
    Console.ReadLine();
}
```

Compile the application again and this is what gets generated:

```text
.method private hidebysig static void  Main(string[] args) cil managed
{
    .entrypoint
    // Code size       121 (0x79)
    .maxstack  9
    .locals init ( [0] class DeCompile.DynamicClass dynamicObject,
    (1) class [Microsoft.CSharp]Microsoft.CSharp.RuntimeBinder.
CSharpArgumentInfo[]
    CS$0$0000)
    IL_0000:  nop
    IL_0001:  newobj     instance void DeCompile.DynamicClass::.ctor()
    IL_0006:  stloc.0
    IL_0007:  ldsfld    class [System.Core]System.Runtime.CompilerServices.CallSite`1
    <class [mscorlib]
System.Action`3<class
[System.Core]System.Runtime.CompilerServices.CallSite,class [mscorlib]
System.Type,object>> DeCompile.Program/'<Main>o__SiteContainer0':::'<p__Site1'
    IL_000c:  brtrue.s   IL_004d
    IL_000e:  ldloca.s   IL_004d
    IL_000f:  ldloc.0
    IL_0010:  ldstr    "WriteLine"
    IL_0014:  ldtoken  DeCompile.Program
    IL_0019:  call     class [mscorlib]System.Type [mscorlib]System.
Type::GetTypeFromHandle
    (valuetype [mscorlib]System.RuntimeTypeHandle)
    IL_001e:  ldnull
    IL_0021:  ldc.i4.2
    IL_0022:  newarr    [Microsoft.CSharp]Microsoft.CSharp.RuntimeBinder.
CSharpArgumentInfo[]
    IL_0025:  stloc.1
    IL_0026:  ldloc.1
    IL_0027:  ldc.i4.0
    IL_0028:  ldnull
    IL_002a:  newobj    instance void [Microsoft.CSharp]Microsoft.CSharp.
RuntimeBinder
.CSharpArgumentInfo::.ctor(valuetype [Microsoft.CSharp]Microsoft.CSharp.
RuntimeBinder
