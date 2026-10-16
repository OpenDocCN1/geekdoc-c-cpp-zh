
the return type is also a Vector. For this particular override of the addition operator, the return type is the same as the containing class, but that is not necessarily the case, as you see later in this example. The two parameters are the things you are operating on. For binary operators (those that take two parameters), such as the addition and subtraction operators, the first parameter is the value on the left of the operator, and the second parameter is the value on the right.

The implementation of this operator returns a new Vector that is initialized using X, Y, and Z properties from the left and right variables.

C# requires that all operator overloads be declared as public and static, which means they are associated with their class or struct, not with a particular instance. Because of this, the body of the operator overload has no access to non-static class members or the this identifier. This is fine because the parameters provide all the input data the operator needs to know to perform its task.

Now all you need to do is write some simple code to test the Vector struct (code file OperatorOverloadingSample/Program.cs):

```
static void Main()
{
    Vector vect1, vect2, vect3;

    vect1 = new Vector(3.0, 3.0, 1.0);
    vect2 = new Vector(2.0, -4.0, -4.0);
    vect3 = vect1 + vect2;

    WriteLine($"vect1 = {vect1}");
    WriteLine($"vect2 = {vect2}");
    WriteLine($"vect3 = {vect3}");
}
```

Compiling and running this code returns the following result:

```
vect1 = ( 3, 3, 1 )
vect2 = ( 2, -4, -4 )
vect3 = ( 5, -1, -3 )
```

In addition to adding vectors, you can multiply and subtract them and compare their values. In this section, you develop the Vector example further by adding a few more operator overloads. You won’t develop the complete set that you’d probably need for a fully functional Vector type, but you develop enough to demonstrate some other aspects of operator overloading. First, you overload the multiplication operator to support multiplying vectors by a scalar and multiplying vectors by another vector.

Multiplying a vector by a scalar simply means multiplying each component individually by the scalar: for example, 2 * (1.0, 2.5, 2.0) returns (2.0, 5.0, 4.0). The relevant operator overload looks similar to this (code file OperatorOverloadingSample2/Vector.cs):

```
public static Vector operator *(double left, Vector right) =>
    new Vector(left * right.X, left * right.Y, left * right.Z);
```

This by itself, however, is not sufficient. If a and b are declared as type Vector, you can write code like this:

```
b = 2 * a;
```

The compiler implicitly converts the integer 2 to a double to match the operator overload signature. However, code like the following does not compile:

```
b = a * 2;
```

The point is that the compiler treats operator overloads exactly like method overloads. It examines all the available overloads of a given operator to find the best match. The preceding statement requires the first parameter to be a Vector and the second parameter to be an integer, or something to which an integer can be implicitly converted. You have not provided such an overload. The compiler cannot start swapping the order of parameters, so the fact that you’ve provided an overload that takes a double followed by a Vector is not sufficient. You need to explicitly define an overload that takes a Vector followed by a double as well. There are two possible ways of implementing this. The first way involves breaking down the vector multiplication operation in the same way that you have done for all operators so far:

```
public static Vector operator *(Vector left, double right) =>
    new Vector(right * left.X, right * left.Y, right * left.Z);
```

Given that you have already written code to implement essentially the same operation, however, you might prefer to reuse that code by writing the following:

```
public static Vector operator *(Vector left, double right) =>
    right * left;
```

This code works by effectively telling the compiler that when it sees a multiplication of a Vector by a double, it can simply reverse the parameters and call the other operator overload. The sample code for this chapter uses the second version because it looks neater and illustrates the idea in action. This version also makes the code more maintainable because it saves duplicating the code to perform the multiplication in two separate overloads.

Next, you need to overload the multiplication operator to support vector multiplication. Mathematics provides a couple of ways to multiply vectors, but the one of interest here is known as the dot product or inner product, which actually returns a scalar as a result. That’s the reason for this example—to demonstrate that arithmetic operators don’t have to return the same type as the class in which they are defined.

In mathematical terms, if you have two vectors (x, y, z) and (X, Y, Z) then the inner product is defined to be the value of x*X + y*Y + z*Z. That might look like a strange way to multiply two things together, but it is actually very useful because it can be used to calculate various other quantities. If you ever write code that displays complex 3D graphics, such as using Direct3D or DirectDraw, you will almost certainly find that your code needs to work out inner products of vectors quite often as an intermediate step in calculating where to place objects on the screen. What’s relevant here is that you want users of your Vector to be able to write double X = a*b to calculate the inner product of two Vector objects (a and b). The relevant overload looks like this:

```
public static double operator *(Vector left, Vector right) =>
    left.X * right.X + left.Y * right.Y + left.Z * right.Z;
```

Now that you understand the arithmetic operators, you can confirm that they work using a simple test method (code file OperatorOverloadingSample2/Program.cs):

```
static void Main()
{
    // stuff to demonstrate arithmetic operations
    Vector vect1, vect2, vect3;

    vect1 = new Vector(1.0, 1.5, 2.0);
    vect2 = new Vector(0.0, 0.0, -10.0);
    vect3 = vect1 + vect2;

    WriteLine($"vect1 = {vect1}");
    WriteLine($"vect2 = {vect2}");
    WriteLine($"vect3 = vect1 + vect2 = {vect3}");
    WriteLine($"2 * vect3 = {2 * vect3}");
    WriteLine($"vect3 += vect2 gives {vect3 += vect2}");
    WriteLine($"vect3 = vect1 * 2 gives {vect3 = vect1 * 2}");
    WriteLine($"vect1 * vect3 = {vect1 * vect3}");
}
```

Running this code produces the following result:

```
vect1 = ( 1, 1.5, 2 )
vect2 = ( 0, 0, -10 )
vect3 = vect1 + vect2 = ( 1, 1.5, -8 )
2 * vect3 = ( 2, 3, -16 )
vect3 += vect2 gives ( 1, 1.5, -18 )
vect3 = vect1 * 2 gives ( 2, 3, 4 )
vect1 * vect3 = 14.5
```

This shows that the operator overloads have given the correct results; but if you look at the test code closely, you might be surprised to notice that it actually used an operator that wasn’t overloaded—the addition assignment operator, +=:

```
WriteLine($"vect3 += vect2 gives {vect3 += vect2}");
```

Although += normally counts as a single operator, it can be broken down into two steps: the addition and the assignment. Unlike the C++ language, C# does not allow you to overload the = operator; but if you overload +, the compiler automatically uses your overload of + to work out how to perform a += operation. The same principle works for all the assignment operators, such as -=, *=, /=, &=, and so on.

## Overloading the Comparison Operators

As shown earlier in the section “Operators,” C# has six comparison operators, and they are paired as follows:

- == and !=
- > and <
- >= and <=

> NOTE A .NET guideline defines that if the == operator returns true when comparing two objects, it should always return true. That’s why you should only overload the == operator on immutable types.

The C# language requires that you overload these operators in pairs. That is, if you overload ==, you must overload != too; otherwise, you get a compiler error. In addition, the comparison operators must return a bool. This is the fundamental difference between these operators and the arithmetic operators. The result of adding or subtracting two quantities, for example, can theoretically be any type depending on the quantities. You have already seen that multiplying two Vector objects can be implemented to give a scalar. Another example involves the .NET base class System.DateTime. It’s possible to subtract two DateTime instances, but the result is not a DateTime; instead it is a System.TimeSpan instance. By contrast, it doesn’t really make much sense for a comparison to return anything other than a bool.

Apart from these differences, overloading the comparison operators follows the same principles as overloading the arithmetic operators. However, comparing quantities isn’t always as simple as you might think. For example, if you simply compare two object references, you compare the memory address where the objects are stored. This is rarely the desired behavior of a comparison operator, so you must code the operator to compare the value of the objects and return the appropriate Boolean response. The following example overrides the == and != operators for the Vector struct. Here is the implementation of == (code file OverloadingComparisonSample/Vector.cs):

```
public static bool operator ==(Vector left, Vector right)
{
    if (object.ReferenceEquals(left, right)) return true;

    return left.X == right.X && left.Y == right.Y && left.Z == right.Z;
}
```

This approach simply compares two Vector objects for equality based on the values of their components. For most structs, that is probably what you will want to do, though in some cases you may need to think carefully about what you mean by equality. For example, if there are embedded classes, should you simply compare whether the references point to the same object (shallow comparison) or whether the values of
