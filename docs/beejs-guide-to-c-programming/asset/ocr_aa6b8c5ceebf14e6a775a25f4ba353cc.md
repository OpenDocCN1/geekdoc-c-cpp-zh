# Chapter 36. Complex Numbers

```
printf("x - y = %f + %fi\n", creal(z), cimag(z));

z = x * y;
printf("x * y = %f + %fi\n", creal(z), cimag(z));

z = x / y;
printf("x / y = %f + %fi\n", creal(z), cimag(z));
```

for a result of:

```
x + y = 4.000000 + 6.000000
x - y = -2.000000 + -2.000000
x * y = -5.000000 + 10.000000
x / y = 0.440000 + 0.080000
```

You can also compare complex numbers for equality (or inequality):

```
#include <stdio.h>
#include <complex.h>

int main(void) {
  double complex x = 1 + 2*I;
  double complex y = 3 + 4*I;

  printf("x == y=%d\n", x == y); // 0
  printf("x != y=%d\n", x != y); // 1
}
```

with the output:

```
x == y = 0
x != y = 1
```

They are equal if both components test equal. Note that as all floating point, they could be equal if they're close enough due to rounding error.

# 36.5 Complex Math

Wait! There's more than just simple complex arithmetic!
Here's a summary table of the math functions available to you with complex numbers.

I'm only going to list the double version of each function, but for all of there is a float version that you can get by appending f to the function, and a long double version that you can get by appending l.

For example, the cabs() function for computing the absolute value of a complex number also has cabsf() and cabsl() variants. I'm omitting them for brevity.

# 36.5.1 Trigonometry Functions

> The simplicity of this statement doesn't do justice to the incredible amount of work that goes into simply understanding how floating point actually functions. https://randomasci.wordpress.com/2012/02/25/comparing-floating-point-numbers-2012-edition/