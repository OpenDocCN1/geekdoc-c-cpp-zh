
## Example 84 Struct Value Creation

There are two ways of creating new values of type Frac (145). The first calls the default argumentless constructor, and the second calls the user-defined constructor Frac (long, long).

```csharp
Frac f1 = new Frac();
Frac f2 = new Frac(1,2);
```

## Example 85 Object Creation and Instance Test

## Example 86 Instance Test and Cast: The As Operator

If parameter o cannot be converted to class Point (43), then the result p is null. The test for null in the if statement checks both that it is non-null and that it is a Point.

```csharp
public static void IsNearPoint(Object o) {
    Point p = o as Point;
    if (p != null && p.x*p.x + p.y*p.y <= 100)
        Console.WriteLine(p + " is a Point near (0,0)");
    else
        Console.WriteLine(o + " is not a Point or not near (0,0)");
}
```

Example 124 shows another use of the as operator.

## 12.15 Field Access Expression

A field access must have one of these four forms:

```csharp
f
C.f
o.f
base.f
```

where C is a class and an expression of reference type. Note that an object of a class may have several fields of the same name f, distinguished by the name of the class that declared the field (see section 10.5 and examples 50 and 87). Field accesses are evaluated as follows:

- A field access of form f refers to a static or instance field of the innermost enclosing class that declares or inherits a field named f.
- A field access of form C.f refers to a static field declared or inherited by class C.
- A field access of form o.f, where expression o has compile-time type C, refers to an instance field declared or inherited by class C. Evaluate the field o is evaluated to obtain an object. The value of o.f is found as the value of the C-field f in object o. Throws NullReferenceException if o is null.
- A field access of form base.f refers to an instance field in the base class of the innermost class whose declaration includes the field expression.

Note the resolution of an instance field access o.f is similar to a non-virtual instance method call o.M(...); see also 12.17:

- In an instance field access o.f, the field referred to is determined by the compile-time type of the object expression o; see example 87.
- In a call to a non-virtual instance method o.M(...), the method is determined by the compile-time type (which must be a class or struct type) of the object expression o; see example 97.
- In a call to a virtual instance method o.M(...), the method is determined by the run-time type (which must be a class) of the object to which o evaluates; see example 97.

## 12.16 The Current Object Reference this

The name this may be used in non-static code to refer to the current object (section 10.1). When non-static code in a given object is executed, the object reference this refers to the object as a whole and is never null. Here, if m is an instance (non-static) member, this.m means the same as m when the member m has not been shadowed by a variable or parameter of the same name.

In a class, this reference is not assignable; in a struct method it is (section 14.2).

## Example 87 Field Access

This example illustrate static and instance access in the classes B, C, and D (example 50). Note that the field referred to by an expression of o.nf is determined by the compile-time type of expression o, not the run-time class of the object to which o evaluates.

```csharp
C cl = new C(100);          // cl has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
```

## Example 88 Using Shadowed Fields

A common use of this is to note that the field referred to by an expression of o.nf is determined by the compile-time type of expression o, not the run-time class of the object to which o evaluates.

```csharp
C cl = new C(100);          // cl has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(100);          // c2 has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
```

## Example 89 Using this to Pass the Current Object

In a class, this reference is not assignable; in a struct method it is (section 14.2).

```csharp
class Point {
    public int x, y;
    public Point(int x, int y) { this.x = x; this.y = y; }
    public override string ToString() { return "(" + x + "," + y + ")"; }
}

class Circle {
    public Point center;
    public int radius;
    public Circle(Point center, int radius) { center = center; radius = radius; }
    public bool ContainsPoint(Point p) {
        int dx = p.x - center.x;
        int dy = p.y - center.y;
        return dx*dx + dy*dy <= radius*radius;
    }
}

void Main() {
    Point p = new Point(0, 0);
    Circle c = new Circle(p, 10);
    if (c.ContainsPoint(new Point(3, 4)))
        Console.WriteLine("Point is a Point near (0,0)");
    else
        Console.WriteLine("Point is not a Point or not near (0,0)");
}
```

## Example 90 Using Type Checking

If parameter o cannot be converted to class Point (43), then the result p is null. The test for null in the if statement checks both that it is non-null and that it is a Point.

```csharp
class Shape { }
static string CheckType(Object o) {
    if (o is Point)
        return "Point";
    else if (o is Circle)
        return "Circle";
    else
        return "Unknown";
}

class Point : Shape {
    public int x, y;
    public Point(int x, int y) { this.x = x; this.y = y; }
}
class Circle : Shape {
    public int radius { get; set; }
}

void Main() {
    Object o = new Point(1,2);
    Console.WriteLine(CheckType(o));
}
```

## 12.17 Method Call

A method call must have one of these four forms:

```
M()
C.M()
o.M()
base.M()
```

where C is a class and an expression of reference type. Note that an object of a class may have several fields of the same name f, distinguished by the name of the class that declared the field (see section 10.5 and examples 50 and 87). Field accesses are evaluated as follows:

- A field access of form f refers to a static or instance field of the innermost enclosing class that declares or inherits a field named f.
- A field access of form C.f refers to a static field declared or inherited by class C.
- A field access of form o.f, where expression o has compile-time type C, refers to an instance field declared or inherited by class C. Evaluate the field o is evaluated to obtain an object. The value of o.f is found as the value of the C-field f in object o. Throws NullReferenceException if o is null.
- A field access of form base.f refers to an instance field in the base class of the innermost class whose declaration includes the field expression.

Note the resolution of an instance field access o.f is similar to a non-virtual instance method call o.M(...); see also 12.17:

- In an instance field access o.f, the field referred to is determined by the compile-time type of the object expression o; see example 87.
- In a call to a non-virtual instance method o.M(...), the method is determined by the compile-time type (which must be a class or struct type) of the object expression o; see example 97.
- In a call to a virtual instance method o.M(...), the method is determined by the run-time type (which must be a class) of the object to which o evaluates; see example 97.

## 12.17.1 Better and Best Method Signature

This section defines the concept of best method signature, used in compile-time overloading resolution (section 12.1.4). When t or u is a non-type, t is better than u if t is implicitly convertible to u or not the other around (section 5.3). For instance, array String[] is better than Object[], which is better than Array, which is better than Object. Any other type of Object is better than Object. Generally, a more specific signature is a better type.

For simple types, rules apply: t is better than u if there is a sequence of (or thin) arguments from t to u in the figure on page 11. For instance, byte is better than short, which is better than int; which is better than long, and so; and byte is better than byte, and so.

When deciding which signature is sig_t=M(t1,...,tn), only positions that correspond to by-value parameters are taken into account; the types of zef and out parameters must match exactly. sig_t is better than sig_u if some t, is better than u, or u is better than t; considering only by-value parameter positions. The method name M and the number n of types must be the same in the signatures. Informally, a better signature is a more specific signature. In a set of signatures there may be one that is better than all other signatures in the set; this is then called a best signature.
