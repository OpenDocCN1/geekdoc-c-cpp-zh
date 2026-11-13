# FIGURE 2.14 A Function with Const Reference Parameters

# A Function Implementation

```
double distance(const point& p1, const point& p2)
// Postcondition: The value returned is the distance between p1 and p2.
// Library facilities used: cmath
{
    double a, b, c_squared;

    // Calculate differences in x and y coordinates.
    a = p1.get_x( ) - p2.get_x( ); // Difference in x coordinates
    b = p1.get_y( ) - p2.get_y( ); // Difference in y coordinates

    // Use Pythagorean Theorem to calculate the square of the distance between the points.
    c_squared = a*a + b*b;

    return sqrt(c_squared);
}
```

![](bbox=[0.68, 0.18, 0.83, 0.36])

# CLARIFYING THE CONST KEYWORD
Part 3: Const Reference Parameters

A const reference parameter is declared by writing the keyword const before a reference parameter and placing & after the parameter type. The parameter is efficient, but unlike an ordinary reference parameter, the function cannot attempt to make any changes to the value of the parameter.

+   1. DECLARED CONSTANTS: PAGE 12
+   2. CONST MEMBER FUNCTIONS: PAGE 38
+   3. CONST REFERENCE PARAMETERS
+   4. STATIC MEMBER CONSTANTS: PAGE 104
+   5. CONST ITERATORS: PAGE 144
+   6. CONST PARAMETERS THAT ARE POINTERS OR ARRAYS: PAGE 171
+   7. THE CONST KEYWORD WITH A POINTER TO A NODE, AND THE NEED FOR TWO VERSIONS OF SOME MEMBER FUNCTIONS: PAGE 227

Example:
double distance(const point& p1, ...

If you use const reference parameters, be sure to follow the consistency requirements in the Programming Tip on page 73.