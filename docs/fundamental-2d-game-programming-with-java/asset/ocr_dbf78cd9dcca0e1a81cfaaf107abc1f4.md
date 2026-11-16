||O + td - C|| = r
\sqrt{(O + td - C)^2} = r
(0 + td - C)^2 - r^2 = 0
[td + (O - C)] * [td + (O - C)] - r^2 = 0
t^2(d * d) + 2t[d * (O - C)] + (O - C) * (O - C) - r^2 = 0

If the d vector is normalized, the dot product of d with itself is one (d x d is 1). Because this equals 1,

t^2(d * d) + 2t[d * (O - C)] + (O - C) * (O - C) - r^2 = 0
t^2(1) + 2t[d * (O - C)] + (O - C) * (O - C) - r^2 = 0
t^2 + 2t[d * (O - C)] + (O - C) * (O - C) - r^2 = 0
let a = 1, b = d * (O - C), and c = (O - C) * (O - C) - r^2

This formula can be rewritten as:

(a)t^2 = (2b)t + (c) = 0

Using the quadratic formula, the solution is:

t = \frac{-(2b) \pm \sqrt{(2b)^2 - 4(a)(c)}}{2a}
t = \frac{-2b \pm \sqrt{4b^2 - 4c}}{2}
t = \frac{-2b \pm \sqrt{4(b^2 - c)}}{2}
t = \frac{-2b \pm 2\sqrt{b^2 - c}}{2}
t = -b \pm \sqrt{b^2 - c}

Where b = d * (O - C) and c = (O - C) * (O - C) - r^2.

The intersection test is coded as follows:

```
private float[] lineCircleIntersection(
Vector2f 0, Vector2f d, Vector2f C, float r ) {
```