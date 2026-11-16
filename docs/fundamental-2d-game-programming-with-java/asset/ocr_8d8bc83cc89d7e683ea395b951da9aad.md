```
1: Vector2f V = 0.sub( C );
2: float b = d.dot( V );
3: float bb = b*b;
4: float rr = r*r;
5: float WV = V.dot( V );
6: float c = WV - rr;
7: if( bb < c ) return null;
8: float root = (float)Math.sqrt( bb - c );
9: return new float[]{ -b . root, -b + root };
}
```

V = O - C
b = d * (O - C)
bb = b²
rr = r²
VV = V * V
c = (O - C) * (O - C) - r² = V * V - r² = VV - rr

If b² < c, then the number under the radical will be negative, and there is no solution.

root = √(b² - c)

The two solutions returned are (-b + √(b² - c), -b - √(b² - c)).

![](bbox=[0.1, 0.57, 0.5, 0.86])

Figure 15.16
Circle-Line Intersection Example.
© 2014 Timothy Wright.