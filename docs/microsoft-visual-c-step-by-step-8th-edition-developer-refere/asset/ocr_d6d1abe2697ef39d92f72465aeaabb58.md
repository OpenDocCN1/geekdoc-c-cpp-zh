# Overriding the equality operators

If you define operator == and operator != in a class, you should also override the Equals and GetHashCode methods inherited from System.Object (or System.ValueType if you are creating a structure). The Equals method should exhibit exactly the same behavior as operator ==. (You should define one in terms of the other.) The GetHashCode method is used by other classes in the Microsoft .NET Framework. (When you use an object as a key in a hash table, for example, the GetHashCode method is called on the object to help calculate a hash value. For more information, see the .NET Framework reference documentation supplied with Visual Studio 2015.) All this method needs to do is return a distinguishing integer value. Don’t return the same integer from the GetHashCode method of all your objects, however, because this will nullify the effectiveness of the hashing algorithms.

# Implementing operators

In the following exercise, you will develop a class that simulates complex numbers.

A complex number has two elements: a real component and an imaginary component. Typically, a complex number is represented in the form (x + yi), where x is the real component and yi is the imaginary component. The values of x and y are regular integers, and i represents the square root of −1 (hence the reason why yi is imaginary). Despite their rather obscure and theoretical feel, complex numbers have a large number of uses in the fields of electronics, applied mathematics, and physics, and in many aspects of engineering. If you want more information about how and why complex numbers are useful, Wikipedia provides a useful and informative article.

![](bbox=[0.1, 0.68, 0.15, 0.72])

# Note

The Microsoft .NET Framework version 4.0 and later includes a type called Complex in the System.Numerics namespace that implements complex numbers, so there is no real need to define your own version of this type anymore. However, it is still instructive to see how to implement some of the common operators for this type.

You will implement complex numbers as a pair of integers that represent the coefficients x and y for the real and imaginary elements. You will also implement the operators necessary for performing simple arithmetic using complex numbers. The following table summarizes how to perform the four primary arithmetic