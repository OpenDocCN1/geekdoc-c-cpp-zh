```
public Rectangle(Point a, Point b) {
    this.a = a;
    this.b = b;
}
public Point A {
    get { return a; }
    set { a = value; }
}
public Point B {
    get { return b; }
    set { b = value; }
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

the assignments are all invalid, since r.A and r.B are not variables.

# 7.17.2 Compound assignment

If the left operand of a compound assignment is of the form E.P or E[E,] where E has the compile-time type dynamic, then the assignment is dynamically bound (§7.2). In this case the compile-time type of the assignment expression is dynamic, and the resolution described below will take place at run-time based on the run-time type of E.

An operation of the form x op= y is processed by applying binary operator overload resolution (§7.3.4) as if the operation was written x op y. Then,

+   - If the return type of the selected operator is implicitly convertible to the type of x, the operation is evaluated as x = x op y, except that x is evaluated only once.
+   - Otherwise, if the selected operator is a predefined operator, if the return type of the selected operator is explicitly convertible to the type of x, and if y is implicitly convertible to the type of x or the operator is a shift operator, then the operation is evaluated as x = (T) (x op y), where T is the type of x, except that x is evaluated only once.
+   - Otherwise, the compound assignment is invalid, and a binding-time error occurs.

The term “evaluated only once” means that in the evaluation of x op y, the results of any constituent expressions of x are temporarily saved and then reused when performing the assignment to x. For example, in the assignment A()[B()] += C(), where A is a method returning int[], and B and C are methods returning int, the methods are invoked only once, in the order A, B, C.

When the left operand of a compound assignment is a property access or indexer access, the property or indexer must have both a get accessor and a set accessor. If this is not the case, a binding-time error occurs.