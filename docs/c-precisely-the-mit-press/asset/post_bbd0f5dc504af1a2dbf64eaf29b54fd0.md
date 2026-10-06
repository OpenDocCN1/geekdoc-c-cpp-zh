
# Expressions 67

**Example 77** Assignment: Implicit and Automatic Explicit Conversion
The assignment d = 12 performs an implicit conversion from int to double. The assignment b=252+1 performs an automatic (explicit but invisible) conversion from int to byte because 252+1 is a compile constant within the range 0...255 of byte, but the assignment b=255+5 is illegal because it is not within that range. The assignment b+=2 is illegal because the right-hand side b+2 has type int, but b=(b+2) is illegal because the right-hand side has type byte. The assignment b+=2 is illegal because it is equivalent to the preceding one, and 2 is within the range of byte, but b=257 is illegal because 257

```csharp
double d;
d = 12;
// implicit conversion from int to double
byte b;
b = 252 + 1;
// Legal: 252 + 1 is a compile-time constant
// Illegal: 255 + 5 is too large
b += b + 2;
// Legal: b+2 has type int
b=(byte)(b + 2);
// Legal: right-hand side has type byte
b += 2;
// Legal: equivalent to b = (byte)(b + 2)
// Illegal: b = 257 is not in range of byte
```

**Example 78** Compound Assignment Operators
Compute the product of all array xs.

```csharp
static double Multiply(double[] xs) {
    double prod = 1.0;
    for (int i = 0; i<xs.Length; i++)
        prod *= xs[i]; // Equivalent to prod = prod * xs[i]
    return prod;
}
```

**Example 79** The Conditional Expression
Return the absolute value of Absolute(double x) always non-negative.

```csharp
static double Absolute(double x) {
    return (x >= 0 ? x : -x);
}
```

**Example 80** Nested Conditional Expressions
Nested conditional expressions are useful for making three-way comparisons, as in a Compare method (section 27.3). Note that the conditional operator (?) associates to the right. Implementing Compare by computing the value v1-v2 does not work because the subtraction overflow.

```csharp
class LongComparer : IComparer<long> {
    public int Compare(long v1, long v2) {
        return v1 < v2 ? -1 : v1 > v2 ? 1 : 0;
    }
}
```

# 12.9 Object Expression

The object creation expression

```csharp
new C (actual-list)
```

creates a new object of non-abstract constructor call to initialize the actual-list, a (possibly empty) comma-separated list of expressions, matches the argument types in actual-list,

The actual-list is evaluated from left to right to obtain a list of arguments. These argument values are bound to the constructor's parameters, an object of the class is created in the computer's store, instance fields get default initial values according to their type, a base constructor is called (explicitly or implicitly: see examples 62 and 98), all field initializers are executed in order of appearance, and finally the constructor is executed to initialize the object. The value of the constructor expression is the newly created object, which is C.

# 12.10 Object Initializer (C# 3.0)

An initializer immediately follows a constructor call to initialize the fields or properties of the newly created object or struct instance. Thus its purpose is similar to that of an array initialization (section 9.1). If the constructor takes no arguments, the complete syntax, including the constructor call, is this:

```csharp
new C { x1 = e1, ..., xn = en }
```

If the constructor takes arguments, the syntax is this:

```csharp
new C (actual-list) { x1 = e1, ..., xn = en }
```

In either case, the xi must name accessible fields or properties of the object, and each ej must be an expression (example 81) or a nested object initializer or collection initializer (example 82). Nested initializers are not allowed on fields or properties of struct type. The ej cannot refer to the newly created object. At run-time the constructor is called, each ej is evaluated from left to right, and its value is assigned to the corresponding field or property xi.

# 12.11 Collection Initializers (C# 3.0)

A collection initializer immediately follows a constructor call and adds items to the new collection. If the constructor takes no arguments, the complete syntax, including the constructor, is:

```csharp
new C { { e1, ..., en }, { e1, ..., en }, ... }
```

If the constructor takes arguments, the syntax is this:

```csharp
new C (actual-list) { { e1, ..., en }, { e1, ..., en }, ... }
```

In either case, the newly created collection must implement System.Collections.Enumerable and the ej must be expressions. Each inner group will be grouped to call a Add(e1, ..., en) method on the collection. The usual overloading resolution is to determine which Add method to call. When n = 1 and the eij do not contain an assignment operator, the inner braces may be omitted.

# Example 81 Object Initializer

An object initializer is used to initialize variable p1 of class Point (example 61). This has the same effect as the three-stage initialization of Point p2. The initialization of p3 first calls the constructor Point (Point) and then changes the value of field y to 17. This has the same effect as the two-stage initialization of Point p4.

```csharp
Point p1 = new Point { x = 10, y = 12 };
Point p2 = new Point(); p2.x = 10; p2.y = 12; // Equivalent to p1 initialization
Point p3 = new Point(p1) { y = 17 };
Point p4 = new Point(p1); p4.y = 17; // Equivalent to p3 initialization
```

# Example 82 Nested Object Initializers

A Rectangle object has an upper left and a lower right corner, declared as automatically implemented properties (section 10.15) called U1 and Lr. A Rectangle r1 can be initialized using these properties. Moreover, by using r2, one can use nested object initializers. This has the same effect as the five-stage initialization of r3. We work only because the Rectangle( ) constructor initializes U1 and Lr with Point objects; otherwise the dereferencing r3.U1 and so on would cause NullReferenceException.

```csharp
public class Rectangle {
    public Point U1 { get; set; }
    public Point Lr { get; set; }
}
Rectangle r1 = new Rectangle { U1 = new Point(10, 12), Lr = new Point(20, 20) };
Rectangle r2 = new Rectangle { U1 = new Point { x = 10, y = 12 }, Lr = new Point { x = 20, y = 20 } };
Rectangle r3 = new Rectangle(); r3.U1 = new Point(10, 12); r3.Lr = new Point(20, 20);
```

# Example 83 Collection Initializer

Variable list1 is initialized by the collection initializer. This has the same effect as the five-stage initialization of list2. The Dictionary<K,V> (section 27.7) shows a case where adding a key-value pair to the dictionary, the inner braces may be omitted.

```csharp
List<int> list1 = new List<int> { 2, 3, 5 };
List<int> list2 = new List<int> { 2 }; list2.Add(3); list2.Add(5);
Dictionary<int,String> list3 = new Dictionary<int,String> { { 1, "one" }, { 2, "two" }, { 5, "five" } };
Dictionary<int,String> list4 = new Dictionary<int,String> { 1, "one", 2, "two", 5, "five" };
```

# 12.12 Struct Value Expression

To create and initialize a value of struct type (section 14), use the struct value expression:

```csharp
new $(actual-list)
```

It creates a new value of struct type and then calls that constructor $ whose signature matches the argument types in actual-list, a possibly empty comma-separated list of expressions.

The actual-list is evaluated from left to right to obtain a list of arguments. If this is empty, the default constructor is called; otherwise a matching constructor is found, and the argument values are bound to the constructor's parameters. A value of type $ is created in the computer's store, a base class constructor is implicitly called, and the finally constructor is executed to initialize the struct value. The value of the constructor call is the newly created struct value, whose type is $.

# 12.13 Instance Test Expression

The instance test e is t whether of e can be converted to t by a reference conversion, a boxing conversion, or an unboxing conversion. It is evaluated by first evaluating to a value v. If v is not null and is a reference to an object of class C, where C can be converted to t, the result is true; otherwise, if e evaluates to a value that can be boxed or unboxed to obtain a value of t, the result is true; otherwise if e has reference type and the result is false. The instance test considers only reference conversions, boxing conversions, and unboxing conversions (section 5.3), but not user-defined conversions (section 10.18) or conversions between simple types (section 5.3.1).

The type t may be a struct type or another value type. This is useful if expression v has reference type, possibly being a reference to a boxed value (section 14.1); if v had value type too, the expression would be either constant true or constant false.

# 12.14 Instance Test and Cast Expression

The expression x as t is equivalent to a combined test and cast: (x is t ? (t)x : (t)null) but evaluates x only once. It has type. The type t must be a reference type.
