With this code in place, we can write the following user code, invoking the explicit operator by means of cast syntax. This code assumes we have a decent ToString defined on the two types such that we can inspect the result easily.

```
var pt = new CartesianPoint(1, 1);
Console.WriteLine(pt);
Console.WriteLine((PolarPoint)pt);
Console.WriteLine((CartesianPoint)(PolarPoint)pt);
```

Try substituting the Cartesian coordinates on the first line with some other values to see the round-tripping behavior of the first line. For quite a few values, you'll see the original value being printed to the screen again. However, because of rounding errors, you might see slight differences from time to time (for example, for a Cartesian point with (0, 1) as its coordinates):

(0, 1)
(1, 1.5707963267949)
(6.12303176911189E-17, 1)

This is nothing but floating-point imprecision, where the X-coordinate of the result really is a zero value, hidden by some incredibly small noise. However, it illustrates nicely why we shouldn't have used an implicit conversion here. Figure 13.7 shows a user-defined conversion to be nothing but a special op_Explicit (or op_Implicit) method.

![](bbox=[0.08, 0.55, 0.55, 0.85])

FIGURE 13.7 An explicit conversion gets implemented as an op_Explicit method.

Use of implicit conversions is less generally applicable and is restricted to some more specialized scenarios. One is where a type acts as a wrapper around a value of another type (for example, a FilterBoolean that has some special semantics implemented behind custom-defined operator s), but whose representation can always be turned into a regular CLR Boolean (or maybe a nullable form thereof). The opposite direction for the conversion is often also applicable: