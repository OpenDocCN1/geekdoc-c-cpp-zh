
> ERIC LIPPERT This signature for Join is one of the primary motivators of the “accumulate bounds and then fix to the best one” part of the method type inference algorithm. If the inner key is, say, of type int, and the outer key of type int?, then rather than having type inference fail due to the “contradiction,” it is better to simply pick the more general of the two types. Because every int is an int?, the type inference algorithm would choose int? for K.

## 7.17 Assignment Operators

The assignment operators assign a new value to a variable, a property, an event, or an indexer element.

```
assignment:
    unary-expression assignment-operator expression
```

assignment-operator:
- =
- +=
- -=
- *=
- /=
- %=
- &=
- |=
- ^=
- <<=
- >>= 

The left operand of an assignment must be an expression classified as a variable, a property access, an indexer access, or an event access.

The = operator is called the simple assignment operator. It assigns the value of the right operand to the variable, property, or indexer element given by the left operand. The left operand of the simple assignment operator may not be an event access (except as described in §10.8.1). The simple assignment operator is described in §7.17.1.

The assignment operators other than the = operator are called the compound assignment operators. These operators perform the indicated operation on the two operands, and then assign the resulting value to the variable, property, or indexer element given by the left operand. The compound assignment operators are described in §7.17.2.

The += and -= operators with an event access expression as the left operand are called the event assignment operators. No other assignment operator is valid with an event access as the left operand. The event assignment operators are described in §7.17.3.

The assignment operators are right-associative, meaning that operations are grouped from right to left. For example, an expression of the form a = b = c is evaluated as a = (b = c).

### 7.17.1 Simple Assignment

The = operator is called the simple assignment operator.

If the left operand of a simple assignment is of the form E.P or E[E], where E has the compile-time type dynamic, then the assignment is dynamically bound (§7.2.2). In this case, the compile-time type of the assignment expression is dynamic, and the resolution described below will take place at runtime based on the runtime type of E.

In a simple assignment, the right operand must be an expression that is implicitly convertible to the type of the left operand. The operation assigns the value of the right operand to the variable, property, or indexer element given by the left operand.

The result of a simple assignment expression is the value assigned to the left operand. The result has the same type as the left operand and is always classified as a value.

If the left operand is a property or indexer access, the property or indexer must have a set accessor. If this is not the case, a binding-time error occurs.

The runtime processing of a simple assignment of the form x = y consists of the following steps:

- If x is classified as a variable:
  - x is evaluated to produce the variable.
  - y is evaluated and, if required, converted to the type of x through an implicit conversion (§6.1).

If the variable given by x is an array element of a reference-type, a runtime check is performed to ensure that the value computed for y is compatible with the array instance of which x is an element. The check succeeds if y is null, or if an implicit reference conversion (§6.1.6) exists from the actual type of the instance referenced by y to the actual element type of the array instance containing x. Otherwise, a System.ArrayTypeMismatchException is thrown.

The value resulting from the evaluation and conversion of y is stored into the location given by the evaluation of x.

If x is classified as a property or indexer access:
- The instance expression (if x is not static) and the argument list (if x is an indexer access) associated with x are evaluated, and the results are used in the subsequent set accessor invocation.
- y is evaluated and, if required, converted to the type of x through an implicit conversion (§6.1).
- The set accessor of x is invoked with the value computed for y as its value argument.

The array covariance rules (§12.5) permit a value of an array type A[] to be a reference to an instance of an array type B[], provided an implicit reference conversion exists from B to A. Because of these rules, assignment to an array element of a reference-type requires a run-time check to ensure that the value being assigned is compatible with the array instance. In the example

```
string[] sa = new string[10];
object[] oa = sa;

oa[0] = null;            // Okay
oa[1] = "Hello";       // Okay
oa[2] = new ArrayList(); // ArrayTypeMismatchException
```

the last assignment causes a System.ArrayTypeMismatchException to be thrown because an instance of ArrayList cannot be stored in an element of a string[].

> BILL WAGNER  This point implies that array assignment does not copy the array, but rather adds a new reference to the same storage.

When a property or indexer declared in a struct-type is the target of an assignment, the instance expression associated with the property or indexer access must be classified as a variable. If the instance expression is classified as a value, a binding-time error occurs. Because of §7.6.4, the same rule also applies to fields.

Given the declarations:

```
struct Point
{
    int x, y;
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
    public int X
    {
        get { return x; }
        set { x = value; }
    }
    public int Y
    {
        get { return y; }
        set { y = value; }
    }
}
struct Rectangle
{
    Point a, b;
    public Rectangle(Point a, Point b)
    {
        this.a = a;
        this.b = b;
    }
    public Point A
    {
        get { return a; }
        set { a = value; }
    }
    public Point B
    {
        get { return b; }
        set { b = value; }
    }
}
```

in the example

```
Point p = new Point();
p.X = 100;
p.Y = 100;
Rectangle r = new Rectangle();
r.A = new Point(10, 10);
r.B = p;
```

the assignments to p.X, p.Y, r.A, and r.B are permitted because p and r are variables. However, in the example

```
Rectangle r = new Rectangle();
r.A.X = 10;
r.A.Y = 10;
r.B.X = 100;
r.B.Y = 100;
```

the assignments are all invalid because r.A and r.B are not variables.

> JOSEPH ALBAHARI An early release of the C# 1.0 compiler allowed assignments such as r.A.X = 10—but they failed silently because r.A returns a copy of a Point (i.e., a value) rather than a variable. People found this behavior confusing, so the condition was detected and reported as an error.

> BILL WAGNER This discussion highlights yet another reason why structs should be immutable.

### 7.17.2 Compound Assignment

If the left operand of a compound assignment is of the form E.P or E[E_i], where E has the compile-time type dynamic, then the assignment is dynamically bound (§7.3.2). In this case, the compile-time type of the assignment expression is dynamic, and the resolution described below will take place at runtime based on the runtime type of E.

An operation of the form x op= y is processed by applying binary operator overload resolution (§7.3.4) as if the operation was written x op y. Then,
- If the return type of the selected operator is implicitly convertible to the type of x, the operation is evaluated as x = x op y, except that x is evaluated only once.
- Otherwise, if the selected operator is a predefined operator, if the return type of the selected operator is explicitly convertible to the type of x, and if y is implicitly convertible to the type of x or the operator is a shift operator, then the operation is evaluated as x = T(x op y), where T is the type of x, except that x is evaluated only once.
- Otherwise, the compound assignment is invalid, and a binding-time error occurs.

> PETER SESTOFT The condition of y being implicitly convertible to the type of x in the second item means that the compound operators are more restrictive in C# than in the C, C++, and Java programming languages. In those languages, the assignment x+=0.9 is legal even if variable x has integer type. When x is non-negative, the assignment has no effect; when x is negative, it adds 1 to x. In C#, the assignment is rejected—wisely, in my opinion.

> VLADIMIR RESHETNIKOV A curious consequence of these rules is that the expression x <<= null is legal if the variable x has type int. Of course, it will always throw an exception at runtime.
