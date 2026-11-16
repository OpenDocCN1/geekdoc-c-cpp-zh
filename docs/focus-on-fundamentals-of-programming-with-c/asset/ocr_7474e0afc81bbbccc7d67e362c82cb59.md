# Arithmetic Expressions as Arguments to Functions

One of the most useful features of C is its ability to allow a function to take an arithmetic expression as an argument. For example, we could have used an arithmetic expression as an argument to the sqrt() function as follows:

```
root1 = (-b + sqrt(b*b-4*a*c)) / (2 * a);
root2 = (-b - sqrt(b*b-4*a*c)) / (2 * a);
```

However, in this example, it's probably better to calculate the discriminant, assign it to a variable, disc, and then use disc in our code so we don't have to perform the calculations for the discriminant twice.

But what if the discriminant is < 0? Then there are no real roots to the quadratic equation. We can have out program make the appropriate test and only perform the calculations for a discriminant that's >= 0:

```
#include <stdio.h>
#include <math.h>
int main (void) {
    int a=1, b=3, c=-4, disc;
    double root1, root2;
    disc = b*b-4*a*c;
    if (disc > 0) {
        root1 = (-b + sqrt(disc)) / (2 * a);
        root2 = (-b - sqrt(disc)) / (2 * a);
        printf("root1 = %0.1lf\n", root1);
        printf("root2 = %0.1lf\n", root2);
    }
    return 0;
}
```