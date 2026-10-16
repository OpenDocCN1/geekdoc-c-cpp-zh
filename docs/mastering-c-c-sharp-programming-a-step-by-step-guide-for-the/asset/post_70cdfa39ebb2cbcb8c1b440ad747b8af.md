
```
Console.WriteLine("These are the constructors in our Customer class:--");
foreach (ConstructorInfo c in constructorInfo)
{
    Console.WriteLine(c);
}
```

The method called GetConstructors() in the Type class will return an array of the ConstructorInfo type – basically, a list of the public constructors that are defined inside the reflected type.

Ok, so now we want to display all the Customer class public methods and, again, we only have the one so all you would see on the console when the program is executed is the one name. To do this, the code would look like this:

```
static void Main(string[] args)
{
    Type type = typeof(Customer);
    MethodInfo[] methodInfo = type.GetMethods();
    Console.WriteLine("The Customer class methods are:--");
    foreach (MethodInfo temp in methodInfo)
    {
        Console.WriteLine(temp.Name);
    }
    Console.Read();
}
```

Note, you may see the names of some extra methods, such as Equals, ToString, GetType, and GetHashCode. That is because those methods were inherited from the class called Object and, as you already know, all classes in .NET will derive from that class because Object is the base class of everything.

The code below shows you how to iterate through a method’s attributes. If you have defined custom attributes of the methods, the method called GetCustomAttributes can be used in the instance of the class called MethodInfo to get the method attributes:

```
foreach (MethodInfo temp in methodInfo)
{
    foreach (Attribute attribute in temp.GetCustomAttributes(true))
    {
        //You usual code will go here
    }
}
```

If you use attributes to decorate business objects in your application, C# reflection can be used to reflect on the type, get the attributes for the type methods, and then do whatever action needs to be performed.

## C# Type Class

The C# Type class is used to represent the type declarations for the interface types, class types, array type, enumeration types, value types, and so on. It is located in the System namespace and inherits the class called System.Reflection.MemberInfo.

Here is a list of the more important properties of the Type class:

| Property | Description |
|---|---|
| Assembly | Retrieves the assembly for the type |
| AssemblyQualifiedName | Retrieves the name of the type that is Assembly qualified |
| Attributes | Retrieve the attributes that are associated with the specified type |
| BaseType | Retrieves the parent or base type |
| Name | Retrieves the fully qualified name of the specified type |
| IsAbstract | Used for checking if the type is an Abstract type |
| IsArray | Used for checking if the type is an Array type |
| IsClass | Used for checking if the type is a Class type |
| IsEnum | Used for checking if the type is an Enum type |
| IsInterface | Used for checking if the type is an Interface type |
| IsNested | Used for checking if the type is a Nested type |
| IsPrimitive | Used for checking if the type is a Primitive type |
| IsPointer | Used for checking if the type is a Pointer type |
| IsNotPublic | Used for checking if the type is not a Public type |
| IsPublic | Used for checking if the type is a Public type |
| IsSealed | Used for checking if the type is a Sealed type |
| IsSerializable | Used for checking if the type is a Serializable type |
| MemberType | Used for checking if the type is a Member type of the Nested Type |
| Module | Retrieves the type's module |
| Name | Retrieves the type's name |
| Namespace | Retrieves the type's namespace |

### C# Type Methods

Below you can find a list of the more important Type class methods:

| Method | Description |
|---|---|
| GetConstructors() | This will return all of the Type's public constructors |
| GetConstructors(BindingFlags) | This will return all the Type’s constructors that have the specified BindingFlags |
| GetFields() | This will return all the Type’s public fields |
| GetFields(BindingFlags) | This will return all the Type’s fields with the specified BindingFlags |
| GetMembers() | This will return all the public members for the Type. |
| GetMembers(BindingFlags) | This will return all the Type’s members with the specified BindingFlags |
| GetMethods() | This will return the Type’s public methods |
| GetMethods(BindingFlags) | This will return all the Type’s methods with the specified BindingFlags |
| GetProperties() | This will return all the Type’s public properties |
| GetProperties(BindingFlags) | This will return all the Type’s properties with the specified BindingFlags |
| GetType() | This will get the current Type |
| GetType(String) | This will get the Type for the specified name |

We’ll finish with a series of examples so you can see how some of these work:

## Get Type

```
using System;
public class ReflectionExample
{
    public static void Main()
    {
        int a = 10;
        Type type = a.GetType();
        Console.WriteLine(type);
    }
}
```

The output would be:

System.Int32

## Get Assembly

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);
        Console.WriteLine(t.Assembly);
    }
}
```

The output would be:

mscorlib, Version=4.0.0.0, Culture=neutral,
PublicKeyToken=b77a5c561934e089

## Print Type Information

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);
        Console.WriteLine(t.FullName);
        Console.WriteLine(t.BaseType);
        Console.WriteLine(t.IsClass);
        Console.WriteLine(t.IsEnum);
        Console.WriteLine(t.IsInterface);
    }
}
```

The output would be:

System.String
System.Object
true
false
false

## Print Constructors

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);

        Console.WriteLine("Constructors of {0} type...", t);
        ConstructorInfo[] ci = t.GetConstructors(BindingFlags.Public | BindingFlags.Instance);
        foreach (ConstructorInfo c in ci)
        {
            Console.WriteLine(c);
        }
    }
}
```

The output would be:

Constructors of System.String type...

Void .ctor(Char*)
Void .ctor(Char*, Int32, Int32)
Void .ctor(SByte*)
Void .ctor(SByte*, Int32, Int32)
Void .ctor(SByte*, Int32, Int32, System.Text.Encoding)
Void .ctor(Char[], Int32, Int32)
Void .ctor(Char[])
Void .ctor(Char, Int32)

## Print Methods

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);
        Console.WriteLine("Methods of {0} type...", t);
        MethodInfo[] ci = t.GetMethods(BindingFlags.Public | BindingFlags.Instance);
        foreach (MethodInfo m in ci)
        {
            Console.WriteLine(m);
        }
    }
}
```

The output would be:

Methods of System.String type...
Boolean Equals(System.Object)
Boolean Equals(System.String)
Boolean Equals(System.String, System.StringComparison)
Char get_Chars(Int32)
Void copyTo(Int32, char[], Int32, Int32)
Char[] ToCharArray()
....

## Print Fields

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);

        Console.WriteLine("Fields of {0} type...", t);
        FieldInfo[] ci = t.GetFields(BindingFlags.Public | BindingFlags.Static | BindingFlags.NonPublic);

        foreach (FieldInfo f in ci)
        {
            Console.WriteLine(f);
        }
    }
}
```

The output would be:
Fields of System.String type...
System.String Empty
Int32 TrimHead
Int32 TrimTail
Int32 TrimBoth
Int32 charPtrAlignConst
Int32 alignConst

## Anonymous Functions

An anonymous function is a function that does not have a name and, in C#, there are two types of them:

- Lambda Expressions
- Anonymous Methods

We use the lambda expression to create an anonymous function.

A lambda expression is an anonymous function that has a sequence of operators or expressions. Every lambda expression must use the lambda operator (=>) which means “becomes” or “goes to”.

The input parameters go on the left side of the operator and an expression or a block of code goes on the right and working with the entry parameters. Normally, a lambda expression is used instead of a delegate, which, if you remember, is a type used for referencing a method or used as a predicate.

### Expression Lambdas

- Parameter => expression
- Parameter-list => expression
- Count => count + 2;
- Sum => sum + 2;
- n => n % 2 == 0

The lambda operator is used to divide lambda expressions into two parts – the input parameter and the body of the lambda. Here’s a simple example:

```
using System;
using System.Collections.Generic;
using System.Linq;
public static class demo
{
    public static void Main()
```
