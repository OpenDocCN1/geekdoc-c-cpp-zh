# 10.13.1 Creating Value Types with struct

To demonstrate operator overloading, we’ll define type ComplexNumber (Section 10.13.2). Complex numbers have the form

$\mathrm{realPart} + \mathrm{imaginaryPart} * i$

where i is √−1. Like integers and floating-point numbers, complex numbers are arithmetic types that are commonly used in calculations. As you know, C#’s simple numeric types are value types. To mimic the simple numeric types, we’ll define ComplexNumber as a value type by using a struct (short for “structure”) rather than a class. C#’s simple types like int and double are actually aliases for structures that are defined by the struct System.Int32, a long by System.Int64, a double by System.Double and so on. The operator overloading techniques shown in Section 10.13.2 also can be applied to classes.

# When to Declare a struct Type

Microsoft recommends using classes for most new types, but recommends a struct if:

+   - the type represents a single value—a complex number represents one number that happens to have a real part and an imaginary part.
+   - the size of an object is 16 bytes or smaller—we’ll represent a complex number’s real and imaginary parts using two doubles (a total of 16 bytes).

For the complete list of struct recommendations, see

https://msdn.microsoft.com/library/ms229017

# 10.13.2 Value Type ComplexNumber

Value type ComplexNumber (Fig. 10.14) overloads the plus (+), minus (−) and multiplication (*) operators to enable programs to add, subtract and multiply instances of class ComplexNumber using common mathematical notation. Lines 9–10 define getter-only auto-implemented properties for the ComplexNumber’s Real and Imaginary components.

```
```csharp
// Fig. 10.14: ComplexNumber.cs
// Value type that overloads operators for adding, subtracting
// and multiplying complex numbers.
using System;

public struct ComplexNumber
{
   // read-only properties that get the real and imaginary components
   public double Real { get; }
   public double Imaginary { get; }

   // constructor
   public ComplexNumber(double real, double imaginary)
   {
```
```

**Fig. 10.14** | Value type that overloads operators for adding, subtracting and multiplying complex numbers. (Part 1 of 2.)