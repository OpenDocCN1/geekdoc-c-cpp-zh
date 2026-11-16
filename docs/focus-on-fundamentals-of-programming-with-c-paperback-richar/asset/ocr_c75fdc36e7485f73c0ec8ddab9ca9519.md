If the discriminate < 0 then no calculations are performed. Perhaps it would be appropriate to generate some output if the discriminate < 0:

```
// quadratic3.c

#include <stdio.h>
#include <math.h>

int main (void) {
   int a, b, c, disc;
   double root1, root2;

   a = 1;
   b = 3;
   c = 44;

   disc = b*b-4*a*c;
   if (disc > 0) {
      root1 = (-b + sqrt(disc)) / (2 * a);
      root2 = (-b - sqrt(disc)) / (2 * a);
      printf("root1 = %0.1lf\n", root1);
      printf("root2 = %0.1lf\n", root2);
   }
   else {
      printf("The discriminate is < 0. There are no real roots.");
   }
   return 0;
}
```

Here's the output:

```
The discriminate is < 0. There are no real roots.
```

Our use of the above decision statements will be the focus of our next section.