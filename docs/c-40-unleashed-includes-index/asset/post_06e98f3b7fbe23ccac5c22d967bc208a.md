
Finalizers (sometimes referred to as destructors) deal with cleanup logic that's executed upon destruction of an object. Although not necessary for pure managed code, the use of finalizers is important when native resources need to be released because they are beyond the control of the garbage collector. To enable the user to clean up an object prior to its automatic destruction by the garbage collector, the IDisposable interface can be implemented.

In Chapter 13, you look at a last set of members that can be declared on a type. In particular, you explore the concept of operator overloading and user-defined conversions between objects of different types.

## CHAPTER 13

### Operator Overloading and Conversions

### IN THIS CHAPTER

- Operators 603
- Conversions 627

One set of members declared on a type is left to be discussed: operator overloads and user-defined conversions. All of those types of members are defined as a special kind of static methods that can be invoked through various built-in language constructs.

Operator overloading comes in handy when defining types that have natural meanings for operations such as addition, logical operators, and whatnot. A good example is a Vector type. User-defined conversions are typically related to objects that represent some kind of value. In such a case, it might make sense to define conversions between different types of values—that is, from an angle in degrees to one in radians.

### Operators

We're almost at the end of our journey through the world of class and struct members. Possibly the most powerful member type (but not quite as powerful as the same notion in languages such as C++) are operator overloads. Basically, operator overloads are special static methods that can be invoked as a result of using operator syntax such as +, && (a very special one consisting of two operator invocations, as you will see), ==, and so on.

Using this feature, it becomes possible to provide more natural-looking and convenient syntax for various operators a type can support on its instances. Vectors are a great example of this:

```
Vector v1 = new Vector(1, 2, 3);
Vector v2 = new Vector(3, 2, 1);
Vector allFour = v1 + v2;   // (4, 4, 4)
Vector larger  = v1 * 4;    // (4, 8, 12)
int dotProduct = v1 * v2;   // 10
```

### POWERFUL TOOLS ARE WEAPONS, TOO

A powerful tool's main drawback is its potential to be used as a weapon. Overloading of operators is one of those tools. Although physicists will drool at the sight of operator overloading, it might not be obvious to people reading your code what's meant by the nonstandard use of an operator. Even the simple Vector sample shown in this section can be interpreted ambiguously: Does * mean dot product or cross product (recall that you can't overload by return type)?

### Defining Operators

The definition of an operator looks like a public static method that uses the operator keyword to indicate its specialized nature. Unary operators should take exactly one single parameter, whereas binary ones should take two. None of the parameters can be passed by reference or as an output parameter. The return type does have restrictions for certain operators, too.

As an example, consider the Vector class again. This time we'll define a set of useful operators:

```
class Vector
{
    private int _x, _y, _z;
    ...

    // Whitespace is allowed between "operator" and "-".
    public static Vector operator -(Vector vector)
    {
        return new Vector(-vector._x, -vector._y, -vector._z);
    }

    public static Vector operator +(Vector left, Vector right)
    {
        return new Vector(
            left._x + right._x, left._y + right._y, left._z + right._z);
    }

// We choose the dot product to show a different return type.
public static int operator *(Vector left, Vector right)
{
    return left._x * right._x + left._y * right._y + left._z * right._z;
}

// For a scalar product, just one of the operands has to be a Vector.
public static Vector operator *(Vector vector, int scale)
{
    return new Vector(
        vector._x * scale, vector._y * scale, vector._z * scale);
}
}
```

Notice that with the unary arithmetic negation operator and the binary arithmetic addition operator it's not yet possible to do binary arithmetic subtraction unless you write the following:

```
Vector difference = v1 + -v2;
```

To enable proper subtraction as a single-step operation, you'll want to define such an operator, too.

### How Operators Are Found

For an operator to be valid, at least one of its parameters should be the same as the declaring type (or, for structs, the nullable variant of it). This requirement is related to the way operators are searched for by the compiler, scanning static methods defined on operand types that participate in the operator's signature. Note that none of the operators have certain fixed properties such as "commutativity" (for example, where a + b and b + a always yield the same result). As a result, our overload of multiplication of a Vector with an integer value works only one way:

```
Vector okay = v1 * 4;
Vector fail = 4 * v1;
```

Because the compiler can't find a binary arithmetic addition operator accepting the two specified operand types on either System.Int32 or Vector, it bails out. To enable the second use, you must define a second operator that accepts the operands in the order that's desired. Obviously, the operator's implementation can invoke another's:

```
public static Vector operator *(int scale, Vector vector)
{
    return vector * scale;
}
```

The act of locating the best possible candidate operator follows principles similar to method overload resolution. In particular, operators defined on more-derived types will be better candidates than ones defined on less-derived types. This is illustrated here with the (limitedly useful) unary plus operator:

```
class Bar
{
    public static Bar operator +(Bar b)
    {
        return b;
    }
}
```

```
class Foo : Bar
{
    public static Foo operator +(Foo f)
    {
        return f;
    }
}
```

The first line of the following example will call Bar's operator, while the second line is turned into a call to Foo's operator. As you can see, the operator on the most derived type wins in that case. Hovering over the + token in Visual Studio will, in fact, reveal which operator is picked:

```
Bar b = +new Bar();
Foo f = +new Foo();
```

### Nullability and Lifted Operators

![](img/a16f85e62ce9bdc527f4b09dbfe26092_635_0.png)

Introduced in .NET 2.0, nullability allows for the use of struct values in conjunction with a null value. As a short recap, the ? suffix can be appended to a value type name to create the nullable variant of it. This enables you to write code like this:

```
int? a = 42;
if (a != null) // Really a.HasValue
    Console.WriteLine("Value = " + a /*.Value */);

int? b = null;
if (b == null)
    Console.WriteLine("Null");
```

As with most changes that touch the type system of the runtime (and hence languages taking advantage of its features), nullability had quite an impact on the language. In the context of operators, the concept of lifted operators was introduced. The idea is this: Instead of requiring predefined and user-defined operators to operate both on value type parameters as well as their nullable forms, it suffices to define such operators for the plain value types only. By means of the concept of lifting, operators like these become readily available on the nullable forms.

For example, the binary arithmetic addition operator can operate on two int operands but is available on nullable int operands, as well, through lifting. If any of the operands are null values, the result will be null, too. If both are non-null, their contained values are unwrapped, added together, and wrapped back into a nullable int:

```
int? a = 3, b = 5, c = null;
```

```
// Will print 8. The type of a + b is by itself an int?
Console.WriteLine(a + b);
```

```
// All of those will simply print an empty line since the results are null.
Console.WriteLine(a + c);
Console.WriteLine(c + b);
Console.WriteLine(c + c);
```

Lifted operators include unary operators +, -, !, ~, ++, and --; binary operators +, -, *, /, %, <<, >>, &, |, and ^; as well as relational and equality operators <, <=, >, >=, ==, and !=.

Most of the unary and binary lifted operators return null if (one of their) operands is null, with the exception of | and &, which follow three-valued logic principles. (For example, use of | on true and null will produce null.)

The relational operators return false if any of the operands is null. Equality operators consider null to be equal to null. This is aligned with the behavior for reference types where two null references are equal.

Because of the lifted operator feature, the following struct's user-defined operators can be used on the struct's nullable form, as well:

```
struct Vector
{
    private int _x, _y;
    
    public Vector(int x, int y)
    {
        _x = x; _y = y;
    }
    
    public static Vector operator +(Vector left, Vector right)
    {
        return new Vector(left._x + right._x, left._y + right._y);
    }
```
