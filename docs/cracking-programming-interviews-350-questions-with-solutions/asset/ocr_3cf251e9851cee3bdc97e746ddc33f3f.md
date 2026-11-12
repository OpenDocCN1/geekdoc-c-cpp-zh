algorithm should, moreover, be such that the number of computational steps required is proportional to the logarithm of the number of vertices of the polygon.

# Solution

For a simple polygon Z, we use the notations in.Z, on.Z, and out.Z as shorthands for the conditions

+   - x is in the interior of Z,
+   - x is on the boundary of Z,
+   - x is in the exterior of Z respectively.

Furthermore, we assume the availability of a three-valued function p.e yielding the clockwise position of the point x with respect to a directed line e:

+   - p.e = 1 if x is on the clockwise side of e,
+   - p.e = 0 if x is on e, and
+   - p.e = −1 if x is on the counterclockwise side of e.

To begin with, we give an algorithm that is linear in the number of vertices of u. With e in the domain of the clockwise directed boundary lines of u, we have on account of u's convexity

+   - in.u ≡ e : p.e = 1
+   - on.u ≡ e : p.e ≥ 0 ∧ e : p.e = 0
+   - out.u ≡ e : p.e = −1

The position of x with respect to u is now computed by computing the minimum of the p values : in.u, on.u, and out.u then correspond to this minimum being equal to 1, 0, and −1 respectively.

For a logarithmic solution we propose to bisect the polygon until a triangle is left. The question then is how to bisect precisely and under control of which invariant.

Let V be a convex polygon (no three vertices collinear, and the vertices being given clockwise, but we will not repeat that all the time), with at least four vertices. For y and z two nonadjacent vertices of V we conclude on account of V's convexity that the interior of the line segment yz is in the interior of V. The line connecting y and z divides V into two convex polygons V0 and V1. Now we can state