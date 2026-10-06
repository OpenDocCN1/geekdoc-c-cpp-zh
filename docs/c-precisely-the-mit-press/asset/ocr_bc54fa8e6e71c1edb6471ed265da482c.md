# Example 87 Field Access

This example illustrate static and instance access in the classes B, C, and D (example 50). Note that the field referred to by an expression of o.nf is determined by the compile-time type of expression o, not the run-time class of the object to which o evaluates.

```
C cl = new C(100);          // cl has type C; object has class C
B bl = cl;               // bl has type B; object has class C
Print(cl.sf, B.sf);        // Prints 102 121
Print(cl.nf, bl.nf);      // Prints 100 120
C c2 = new C(200);         // c2 has type C; object has class C
B b2 = c2;               // b2 has type B; object has class C
Print(cl.sf, b2.sf);      // Prints 200 120
Print(cl.nf, bl.nf);
D d3 = new D(300);         // d3 has type D; object has class D
C c3 = d3;               // c3 has type C; object has class D
B b3 = d3;               // b3 has type B; object has class D
Print(d.sf, C.sf, B.sf);  // Prints 304 340 361
Print(d3.nf, c3.nf, b3.nf); // Prints 300 340 360
```

# Example 88 Using When Referring to Shadowed Fields

A common use of this is to refer to fields (this.x and this.y) that have been shadowed by parameters (x and y), especially in constructors, as in the Point class (example 43).

```
class Point {
    protected internal int x, y;
    public Point(int x, int y) { this.x = x; this.y = y; }
n
```

# Example 89 Using this to Pass the Current Object to a Method

In the APoint class (example 44), the current object reference is used in the constructor to add the newly created object to the generic list allpoints, and it is used in the method GetIndex to look up the current object in the list.

```
public class APoint {
    private static List<APoint> allpoints = new List<APoint>();
    private int x, y;
    public APoint(int x, int y) {
        allpoints.Add(this); this.x = x; this.y = y;
    }
    public int GetIndex() {
        return allpoints.IndexOf(this);
    }
}
```