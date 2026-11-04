
First of all, note that BigInteger lives outside the triad of BCL assemblies, namely in the System.Numerics assembly. The namespace bearing the same name as this assembly will have to be imported, too, for unqualified use of the struct's name.

To create a new BigInteger value, numerous paths can be taken. One is to invoke a constructor that can take a whole bunch of primitive numeric types, or a byte array that contains the bytes that make up a big integer if you love to deal with low-level representations right from the start. Alternatively, implicit conversions can be used to turn numeric values of primitive types into a BigInteger:

```
BigInteger x = new BigInteger(uint.MaxValue); // 2^32 - 1
BigInteger y = ulong.MaxValue; // 2^64 - 1
```

All expected math-related operators have been overloaded, allowing easy use of the created big integer values. For example, we can simply multiply the preceding:

```
BigInteger z = x * y;
Console.WriteLine(z);
Console.WriteLine(BigInteger.Log(z, 2)); // 95.999 ~= 2^(32 + 64)
```

The use of BigInteger.Log illustrates the availability of Math-alike static methods for various operations on big integer values. The reason they haven't been moved to the Math class is due to framework assembly layering. Adding a BigInteger overload to, say, the Math.Log method would make Math's assembly (mscorlib) dependent on the newly introduced System.Numerics assembly. It would also be the case that references to the new assembly are needed for compilers to have all the information needed to do proper overload resolution.

To illustrate a few other operators available, consider the following implementation of an unlimited-precision factorial computation:

```
BigInteger n = 10000;
BigInteger fac = 1;
for (BigInteger i = 2; i < n; i++)
    fac *= i;

Console.WriteLine(fac);
```

This produces a number of no fewer than 35,656 digits that one couldn't even dream of computing efficiently before .NET 4 without external libraries or a custom (and likely error-prone) implementation of large integer arithmetic. It's left as an exercise for you to spot all the overloaded BigInteger operators used in the preceding code. (Tip: There is more than a handful.)

Static methods on BigInteger include typical Parse and TryParse methods, as well as functions similar to those on the Math class (except for things such as trigonometry). One slightly-unexpected method is GreatestCommonDivisor, which should speak for itself.

## NO C# LITERAL (YET?)

Unfortunately, it's not possible to create a BigInteger value by writing a literal in C# code unless it fits in a 64-bit integral, in which case you're merely creating some primitive value (for example, an Int32) that can be implicitly converted to BigInteger. I would definitely love to see literal support for BigInteger values, which on the flip side would obviously add another dependency to the language, needing a reference to the System.Numerics assembly.

Without this support, you can either use the BigInteger.Parse method to write down the value as a string literal or turn the big integer value into a byte array, which would be more efficient (though, as usual, let measurements be your guide in deciding what to optimize). If you want to go for the latter option, simply use the Parse method once, call ToByteArray on the produced BigInteger value, and turn that byte array into a piece of C# array initializer code:

```
var bs = BigInteger.Parse("12345678901234567890").ToByteArray();
Console.WriteLine("new byte[] { " + string.Join(",", bs) + " }");
```

This would be precisely the kind of code the C# compiler could generate (during compile time) for the use of a BigInteger literal, passing the byte array to one of the BigInteger constructors. For the output of the preceding, this would look like the following:

```
var x = new BigInteger(new byte[] { 210, 10, 31, 235, 140, 169, 84, 171, 0 });
Console.WriteLine(x); // 12345678901234567890
```

If BigIntegers become popular in the C# community, maybe we'll see direct support for them in a future version of the language. Languages that aim more at the scientific computation community, such as F#, do provide direct support today.

## Complex Numbers

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1341_0.png)

While the BCL teams were at it, adding System.Numerics with the BigInteger type, they also added a complex number struct. Because most readers won't have to deal with complex numbers on a day-to-day basis, we restrict ourselves to a small refresher on the concept of complex number in Figure 26.14, as well as a simple code fragment.

Creation of a Complex value can be done in a number of ways. One is to specify real and imaginary parts of the number to the constructor, both of which are typed using double floating-point precision values. Math-savvy readers will recall there's another representation of complex numbers, though, based on polar coordinates. Because this also involves two doubles, one for the radius and one for the angle (in radians), it wasn't possible to provide another constructor because it would end up having the same signature. In lieu of this, a static method called FromPolarCoordinates is provided. Besides those two ways of constructing new complex values, three public read-only fields are provided with commonly used complex numbers:

```
var c1 = new Complex(3.0, 4.0);
var c2 = Complex.FromPolarCoordinates(1.0, Math.PI / 3 /* 60 degrees */);
var c3 = Complex.Zero;
var c4 = Complex.One;
var c5 = Complex.ImaginaryOne;
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1342_0.png)

FIGURE 26.14 Brief recap of complex number theory.

The ToString representation simply prints the real and imaginary parts as the default textual form, also known as the Cartesian coordinates:

```
Console.WriteLine(c1); // (3, 4)
Console.WriteLine(c2); // (0.5, 0.866025403784439) - see Figure 26.14
Console.WriteLine(c3); // (0, 0)
Console.WriteLine(c4); // (1, 0)
Console.WriteLine(c5); // (0, 1)
```

Four instance-level properties are available on Complex values, allowing the two parts of both representations to be queried. For example, the first complex number we wrote down has a radius of five (known as the magnitude) and an angle (known as the phase) that can be derived from the real and imaginary parts using the Atan function:

```
// Magnitude = Math.Sqrt(3.0 * 3.0 + 4.0 * 4.0)   Phase = Math.Atan(4.0 / 3.0)
Console.WriteLine("({0}, {1})", c1.Magnitude, c1.Phase);
```

All sorts of calculations can be done with `Complex` values, thanks to a whole lot of overloaded operators. Conversions exist from primitive number values (and even the `BigInteger` struct) to complex numbers whose imaginary part will be set to zero. We won’t go into detail on all those operations; instead, I encourage you to consult some standard works on number theory if your knowledge of complex numbers has become a bit dusty. Here are a few examples of working with complex numbers:

```csharp
Console.WriteLine(c1);
Console.WriteLine(c2.Real);       // Cosine of angle
Console.WriteLine(c3.Imaginary);  // Sine of angle
Console.WriteLine(c4.Magnitude);  // Radius of circle
Console.WriteLine(c5.Phase);      // Angle in radians
```

```csharp
Console.WriteLine(c1 + c2 * c3 - c4 / c5); // Standard arithmetic
Console.WriteLine(Complex.Pow(c1, c2));   // Refer to theory :-)
Console.WriteLine(Complex.Reciprocal(c3)); // 1 + 0i divided by c
Console.WriteLine(Complex.Negate(c4));    // Flip both signs
Console.WriteLine(Complex.Conjugate(c5)); // Flip imaginary sign
```

With this, we wrap up our discussion about complex numbers. One thing that’s worth mentioning is that the introduction of those numbers as part of the BCL allows for true interoperability between languages that provide them natively and others, like C#, that want to consume such values.

### Generating Random Numbers

A fairly common task is to generate random numbers (for example, to create a random permutation of objects in a collection, to write a lottery application, to generate test input sequences). The `System` namespace contains a `Random` class that’s designed for this purpose, producing what’s known as a *pseudo-random sequence*.

### SECURITY, SECURITY, SECURITY

It can’t be emphasized enough that the `Random` class is not well suited for use in a security-critical context (for example, to provide cryptographic strength random numbers) in part due to its pseudo-random (and hence predictable) nature.

For such uses, the `System.Security.Cryptography` namespace should be put into action, with its `RandomNumberGenerator` base class and derived types. However, when you find yourself creating such random numbers, it’s good to ask why you’re doing it in the first place. If you happen to be implementing some kind of cryptographic algorithm yourself, immediately stop doing so unless you’re a world authority in that field (in that case, I’m incredibly pleased you’re reading this book).

Security and cryptography are things everyone should use when appropriate for the task at hand. At the same time, it’s no good trying to implement such low-level facilities yourself. You’ll find that the `System.Security` namespace and all of its children contain plenty of well-tested and massively reviewed facilities you can readily leverage.
