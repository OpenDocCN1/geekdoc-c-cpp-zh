then the next generation would appear as follows:

![](bbox=[0.158, 0.116, 0.863, 0.283])

Using the initial configuration shown previously, compute the next four generations.

9.10 A quadrilateral is a four-sided figure. A quadrilateral is a kite if it has two distinct pairs of consecutive sides of the same length. A quadrilateral is a trapezoid if it has at least one pair of parallel sides. A quadrilateral is a parallelogram if both pairs of its opposite sides are parallel. A quadrilateral is a rhombus if its four sides are equal in length. A quadrilateral is a rectangle if its four angles are equal. A square is a square if it has four equal sides and four right angles. Note that a rhombus is a kite and a parallelogram, a parallelogram is a trapezoid, a rectangle is a parallelogram, and a square is a rhombus and a rectangle.

Write a program that, when given the four points forming a quadrilateral, will determine the type of quadrilateral. The program should account for possible round-off error (assume that two sides are equal if the difference between their lengths is less than .00001). Test your program with the following quadrilaterals:

+   (a) Points (0,0), (2,4), (6,0), and (3,2).
+   (b) Points (0,3), (2,5), (4,3), and (2,0).
+   (c) Points (0,0), (3,2), (4,2), and (9,0).
+   (d) Points (0,0), (1,3), (5,3), and (4,0).
+   (e) Points (0,0), (3.5196152), (9.5196152), and (6,0).
+   (f) Points (0,0), (0,4), (2,4), and (2,0).
+   (g) Points (0,2), (4,6), (6,4), and (2,0).
+   (h) Points (0,2), (2,4), (4,2), and (2,0).

Hint: If side 1 contains the points (x1,y1) and (x2,y2) and side 2 contains the points (x3,y3) and (x4,y4), then side 1 is parallel to side 2 if (x2 - x1) * (y4 - y3) is equal to (x4 - x3) * (y2 - y1).

9.11 Write a CLIPS program that can determine if a simple sentence is grammatically correct. The sentence should use the following BNF:

```
<sentence> ::= <verb> <direct-object>
[<indirect-object>]
<direct-object> ::= [<determiner>] <adjective>* <noun>
<indirect-object> ::= <preposition> <direct-object>
<determiner> ::= a | an | the
```