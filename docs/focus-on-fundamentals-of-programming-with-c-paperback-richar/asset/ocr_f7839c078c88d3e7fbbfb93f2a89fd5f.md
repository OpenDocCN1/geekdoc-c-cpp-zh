```
j = labs(-1000000001); // assigns 1000000000 to j
   // Note that's an el after the last zero in
   // the function argument
```

# Quadratic Equation Example

Let's compute the roots of a quadratic equation in x of the form:

ax² + bx + c = 0

We're going to code the quadratic formula: x = (-b ± √(b² - 4ac)) / 2a

```
// quadratic1.c

#include <stdio.h>
#include <math.h>

int main (void) {
    int a=1, b=3, c=-4, disc;
    double root1, root2;

    disc = b*b-4*a*c;
    root1 = (-b + sqrt(disc)) / (2 * a);
    root2 = (-b - sqrt(disc)) / (2 * a);
    printf("root1 = %5.2f\n", root1);
    printf("root2 = %5.2f\n", root2);
    return 0;
}
```

Here's the output:

```
root1 = 1.00
root2 = -4.00
```