
If we need to add two numbers, we can do it easily.

```csharp
int answer = add(10, 4),
```

If we need to add four numbers, we have no problems either.

```csharp
int answer = add(10, 4, 5, 12);
```

So why are optional parameters dangerous? Because sometimes default values have unintended consequences. For instance, you don't want to make a divide method and default the parameters to 0. Someone would call it and get an undefined division by zero error. Setting the optional values in addall to 1 inside the method would be bad.

```csharp
public static int add(int z, int y, int x = 0, int w = 0,
    int v = 1)
    //CLEARLY don't want this
    return z + y + x + w + v;
```

And sometimes problems can be very subtle, so use optional parameters carefully. In instance, say you have a base class, and then a derived class that implements the base, like this:

```csharp
public abstract class Base
{
    public virtual void SomeFunction(int x = 0)
    {...}
}
```

```csharp
public sealed class Derived
{
    public override void SomeFunction(int x = 1)
    {...}
}
```

What happens if you declare a new instance?

```csharp
Base ex1 = new Base();
ex1.SomeFunction();                  // SomeFunction (0)
Base ex2 = new Derived();
ex2.SomeFunction();                  // SomeFunction (0)
Derived ex3 = new Derived();
ex3.SomeFunction();                  // SomeFunction (1)
```

## 784 Optional Parameters

What happened here? Depending on how you implement the classes, the default value for the optional parameter is set differently. The first example, ex1, is an implementation of Base, and the default optional parameter is 0. In the second example, ex2 is cast to a type of Derived (which is legal, Derived is a subclass of Base) and the default value is also 0. However, in the third example, Derived is instantiated directly and the default value is 1. This is not particularly expected behavior, though I have to admit that I am not sure WHAT expected behavior is in a case like this. No matter how you slice it, it's a gotcha and something to watch out for.

## Reference types

New reference types are implemented with

- Class
- Interface
- Delegate

These need to be built before you use them; class itself isn't a reference type, but, the Calendar class is.

There are three built-in reference types in the .NET Framework:

- String (who knows why this isn't a static type)
- Object
- Dynamic

You can pass a reference type into a method just like you can pass a static type. You still use it inside the method like any other variable.

But can reference types be passed, like static types? Let's try. For instance, if we have a Schedule method for our Calendar class, we could pass in the CourseId or we could pass in the whole Course. It all depends on how we structure the application.

```csharp
public class Course {
    public int CourseId;
    public string Name;
    public void Course(int id, string name)
{
  CourseId = id;
  Name = name;
}
public class Calendar
{
    public static void Schedule(int course)
    {
    }
    public static void Schedule(Course course)
    {
      //Something interesting happens here
    }
}
```

In this example, we have an overloaded method for Schedule — one that accepts a CourseId and one that accepts a Course reference type. The second is a reference type, because Course is a class, rather than a static type, like the Integer of the CourseId.

What we want the second Schedule method to support an optional Course parameter? Say, if I just want to create a New Course by default if I omit the parameter. This would be similar to setting a static integer to "0" or whatever, wouldn't it?

```csharp
public static void Schedule(Course course) = New
{
  //Implementation here
}
```

This isn't allowed, however. Visual Studio allows optional parameters on static types, and the compiler tells you. If I want to do this, I have to accept the CourseId in the method.

## Output parameters

As I discussed, output parameters change the value of the variable. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword. Output parameters are marked in the method signature with the out keyword.

## Overload Resolution

Problems begin when you have optional arguments and overloaded methods in the method signature. Because C# allows for differently named overloads, things can get hairy. Take for example:

```csharp
class Course {
    public void New(object course)
    { }
    public void New(int courseId)
    {
}
```

Try calling the New method with something like:

```csharp
Course course = new Course();
course.New(10);
```

Here, the runtime picks the second overload because 10 matches better int than an object. The same is true when dealing with overloaded methods with optional parameters. The tiebreaker goes to the overload with the fewest casts required to make it.

## Chapter 3: Helping Out with Interop

In This Chapter

- Using Dynamic
- Deploying without primaryop assemblies
- Skipping the ref statement

The Component Object Model, usually called COM, is a standard for the language of software bits at the binary level. Because it is binary, it is language-neutral, which was Microsoft's goal when the company introduced COM in 1993. COM is a language-neutral way to implement objects in a lot of different environments.

COM is an umbrella for a lot of different technologies in the Microsoft world. OLE, OX, COM+, and DCOM are all versions of the same idea — just implemented in different ways.

The problem with COM is networking. Although a thorough explanation is outside the scope of this book, it is important to understand that Microsoft's answer to broadly distributed applications was less than good. DCOM, or Distributed COM, was fraught with problems.

When XML Web services entered the scene in the late 1990s with SOAP, COM just put a wrapper around COM that translated to and from SOAP. In the background, however, they were planning a more sophisticated messaging system for Windows. That eventually became ASP.NET Web services, and then WCF in its latest iteration.

What applications could be so Neanderthal? How about Microsoft Office. Yup — Microsoft Office is the big, and it is why C# 4.0 includes a bunch of COM interoperability features, collectively called Interop Improvements.
