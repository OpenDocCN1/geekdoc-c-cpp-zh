# Expressions 79

Example 96 Pass by Value and Pass by Reference for Classes and Struct Types
The call M(pcl, ref pc2, psl, ref ps2 passes an object reference, a reference to a variable holding
an object reference, a struct value, and a reference to a variable holding a struct value.

```
Point pcl = new Point(55, 555), pc2 = new Point(66, 666);
SPoint psl = new SPoint(77, 777), ps2 = new SPoint(88, 888);
M(pcl, ref pc2, psl, ref ps2);
...
```

```
static void M(Point pc1, ref Point pc2, SPoint psl, ref SPoint ps2) {
pc1.x = 97;
pc2 = new Point(16, 17);
ppc1.x = pc2;
ps1.x = 98;
ps1 = new SPoint(18, 19);
ps2.x = 99;
}
```

The solid arrows show the state before the method call; the dashed arrows are references caused by
parameter passing; and the dotted arrows show the state after method return.

![](bbox=[0.178, 0.455, 0.762, 0.715])

When M returns, its parameters pc1, pc2, psl, and ps2 are discarded. In Main, the ref
arguments pc2 and ps2 have been modified. The by-value arguments pc1 and psl are unmodified, but a
field of the object pointed to by pc1 has been modified.