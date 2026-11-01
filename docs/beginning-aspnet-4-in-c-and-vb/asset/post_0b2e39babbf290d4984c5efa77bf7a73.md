
Multiplying a vector by a scalar simply means multiplying each component individually by the scalar: for example, 2 * (1.0, 2.5, 2.0) returns (2.0, 5.0, 4.0). The relevant operator overload looks similar to this:

```csharp
public static Vector operator * (double lhs, Vector rhs)
{
    return new Vector(lhs * rhs.x, lhs * rhs.y, lhs * rhs.z);
}
```

code download VectorStructMoreOverloads.sln

This by itself, however, is not sufficient. If a and b are declared as type Vector, it allows you to write code like this:

b = 2 * a;

The compiler will implicitly convert the integer 2 to a double to match the operator overload signature. However, code like the following will not compile:

b = a * 2;

The thing is that the compiler treats operator overloads exactly as method overloads. It examines all the available overloads of a given operator to find the best match. The preceding statement requires the first parameter to be a Vector and the second parameter to be an integer, or something that an integer can be implicitly converted to. You have not provided such an overload. The compiler cannot start swapping the order of parameters, so the fact that you've provided an overload that takes a double followed by a Vector is not sufficient. You need to explicitly define an overload that takes a Vector followed by a double as well. There are two possible ways of implementing this. The first way involves breaking down the vector multiplication operation in the same way that you have done for all operators so far:

```csharp
public static Vector operator * (Vector lhs, double rhs)
{
    return new Vector(lhs.x * rhs, lhs.y * rhs, lhs.z * rhs);
}
```

Given that you have already written code to implement essentially the same operation, however, you might prefer to reuse that code by writing:

```csharp
public static Vector operator * (Vector lhs, double rhs)
{
    return rhs * lhs;
}
```

This code works by effectively telling the compiler that if it sees a multiplication of a Vector by a double, it can simply reverse the parameters and call the other operator overload. The sample code for this chapter uses the second version, because it looks neater and illustrates the idea in action. This version also makes for more maintainable code because it saves duplicating the code to perform the multiplication in two separate overloads. Next, you need to overload the multiplication operator to support vector multiplication. Mathematics provides a couple of ways of multiplying vectors together, but the one we are interested in here is known as the dot product or inner product, which actually gives a scalar as a result. That's the reason for this example, to demonstrate that arithmetic operators don't have to return the same type as the class in which they are defined. In mathematical terms, if you have two vectors (x, y, z) and (X, Y, Z), then the inner product is defined to be the value of x*X + y*Y + z*Z. That might look like a strange way to multiply two things together, but it is actually very useful because it can be used to calculate various other quantities. Certainly, if you ever end up writing code that displays complex 3D graphics, for example using Direct3D or DirectDraw, you will almost certainly find your code needs to work out inner products of vectors quite often as an intermediate step in calculating where to place objects on the screen. What concerns us here is that we want people using your Vector to be able to write double X = a*b to calculate the inner product of two Vector objects (a and b). The relevant overload looks like this:

```csharp
public static double operator * (Vector lhs, Vector rhs)
{
    return lhs.x * rhs.x + lhs.y * rhs.y + lhs.z * rhs.z;
}
```

Now that you understand the arithmetic operators, you can check that they work using a simple test method:

```csharp
static void Main()
{
    // stuff to demonstrate arithmetic operations
    Vector vect1, vect3;
    vect1 = new Vector(1.0, 1.5, 2.0);
    vect2 = new Vector(0.0, 0.0, -10.0);

    vect3 = vect1 + vect2;

    Console.WriteLine("vect1 = " + vect1);
    Console.WriteLine("vect2 = " + vect2);
    Console.WriteLine("vect3 = vect1 + vect2 = " + vect3);
    Console.WriteLine("2*vect3 = " + 2*vect3);
    vect3 += vect2;

    Console.WriteLine("vect3+=vect2 gives " + vect3);

    vect3 = vect1*2;

    Console.WriteLine("Setting vect3=vect1*2 gives " + vect3);

    double dot = vect1*vect3;

    Console.WriteLine("vect1*vect3 = " + dot);
}
```

Running this code (Vectors2.cs) produces the following result:

## VECTORS2

```
vect1 = { 1, 1.5, 2 }
vect2 = { 0, 0, -10 }
vect3 = vect1 + vect2 = { 1, 1.5, -8 }
2*vect3 = { 2, 3, -16 }
vect3+=vect2 gives { 1, 1.5, -18 }
Setting vect3=vect1*2 gives { 2, 3, 4 }
vect1*vect3 = 14.5
```

This shows that the operator overloads have given the correct results, but if you look at the test code closely, you might be surprised to notice that it actually used an operator that wasn't overloaded — the addition assignment operator, +=

```
vect3 += vect2;

Console.WriteLine("vect3 += vect2 gives " + vect3);
```

Although += normally counts as a single operator, it can be broken down into two steps: the addition and the assignment. Unlike the C++ language, C# will not actually allow you to overload the = operator, but if you overload +, the compiler will automatically use your overload of + to work out how to perform a += operation. The same principle works for all the assignment operators such as -=, *=, /=, &=, and so on.

You also need to override the != operator. The simple way to do this is:

```csharp
public static bool operator != (Vector lhs, Vector rhs)
{
    return ! (lhs == rhs);
}
```

As usual, you should quickly check that your override works with some test code. This time you'll define three Vector objects and compare them:

```csharp
static void Main()
{
    Vector vect1, vect2, vect3;

    vect1 = new Vector(3.0, 3.0, -10.0);
    vect2 = new Vector(3.0, 3.0, -10.0);
    vect3 = new Vector(2.0, 3.0, 6.0);

    Console.WriteLine("vect1==vect2 returns " + (vect1==vect2));
    Console.WriteLine("vect1==vect3 returns " + (vect1==vect3));
    Console.WriteLine("vect2==vect3 returns " + (vect2==vect3));

    Console.WriteLine();

    Console.WriteLine("vect1!=vect2 returns " + (vect1!=vect2));
    Console.WriteLine("vect1!=vect3 returns " + (vect1!=vect3));
    Console.WriteLine("vect2!=vect3 returns " + (vect2!=vect3));
}
```

code snippet Vectors3.cs

Compiling this code (the Vectors3.cs sample in the code download) generates the following compiler warning because you haven't overridden Equals() for your Vector. For our purposes here, that does not matter, so we will ignore it.

```
Microsoft (R) Visual C# 2010 Compiler version 4.0.21006.1
for Microsoft (R) .NET Framework version 4.0
Copyright (C) Microsoft Corporation. All rights reserved.

Vectors3.cs(5,11): warning CS0660: 'Brox.ProcSharp.OOCSharp.Vector' defines
    operator == or operator != but does not override Object.Equals(object o)
Vectors3.cs(5,11): warning CS0661: 'Brox.ProcSharp.OOCSharp.Vector' defines
    operator == or operator != but does not override Object.GetHashCode()
```

Running the example produces these results at the command line:

## VECTORS3

```
vect1==vect2 returns True
vect1==vect3 returns False
vect2==vect3 returns False

vect1!=vect2 returns False
vect1!=vect3 returns True
vect2!=vect3 returns True
```

## Which Operators Can You Overload?

It is not possible to overload all the available operators. The operators that you can overload are listed in the following table.

going wrong for certain values — perhaps some loss of data or an exception being thrown — then you should define the cast as explicit.

The syntax for defining a cast is similar to that for overloading operators discussed earlier in this chapter. This is not a coincidence — a cast is regarded as an operator whose effect is to convert from the source type to the destination type. To illustrate the syntax, the following is taken from an example struct named Currency, which is introduced later in this section:

```csharp
public static implicit operator float (Currency value)
{
    // processing
}
```

The return type of the operator defines the target type of the cast operation, and the single parameter is the source object for the conversion. The cast defined here allows you to implicitly convert the value of a Currency into a float. Note that if a conversion has been declared as implicit, the compiler will permit its use either implicitly or explicitly. If it has been declared as explicit, the compiler will only permit it to be used explicitly. In common with other operator overloads, casts must be declared as both public and static.

## Implementing User-Defined Casts

This section illustrates the use of implicit and explicit user-defined casts in an example called SimpleCurrency (which, as usual, is available in the code download). In this example, you define a struct, Currency, which holds a positive USD ($) monetary value. C# provides the decimal type for this purpose, but it is possible you will still want to write your own struct or class to represent monetary values if you want to perform sophisticated financial processing and therefore want to implement specific methods on such a class.

> > *The syntax for casting is the same for structs and classes. This example happens to be for a struct, but would work just as well if you declared Currency as a class.*

Initially, the definition of the Currency struct is:

```csharp
struct Currency
{
    public uint Dollars;
    public ushort Cents;

    public Currency(uint dollars, ushort cents)
    {
        this.Dollars = dollars;
        this.Cents = cents;
    }
}
```
