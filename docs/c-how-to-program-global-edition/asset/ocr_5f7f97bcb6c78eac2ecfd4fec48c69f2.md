```
test.c:5:1: warning: data definition has no type or storage class
returnImplicitInt(); // prototype with unspecified return type
 ^
test.c:5:1: warning: type defaults to 'int' in declaration of 'returnImplicitInt'
test.c:6:1: warning: parameter names (without types) in function declaration
int demoImplicitInt(x); // prototype missing a parameter name type
 ^
test.c:20:1: warning: return type defaults to 'int'
returnImplicitInt()
 ^
test.c: In function 'demoImplicitInt':
test.c:25:5: warning: type of 'x' defaults to 'int'
int demoImplicitInt(x)
 ^
```

Fig. E.7 | Warning messages for implicit int produced by gcc.

# E.6 Complex Numbers

[This section can be read after Section 5.3.]

The C99 standard introduced support for complex numbers and complex arithmetic. The program of Fig. E.8 performs basic operations with complex numbers. We compiled and ran this program on the LLVM compiler in Apple's Xcode 6.2

```
// Fig. E.8: figE_08.c
// Using complex numbers in C99
#include <stdio.h>
#include <complex.h> // for complex type and math functions

int main(void)
{
    double complex a = 32.123 + 24.456 * I; // a is 32.123 + 24.456i
    double complex b = 23.789 + 42.987 * I; // b is 23.789 + 42.987i
    double complex c = 3.0 + 2.0 * I; // c is 3.0 + 2.0i

    double complex sum = a + b; // perform complex addition
    double complex pwr = cpow(a, c); // perform complex exponentiation

    printf("a is %f + %fi\n", creal(a), cimag(a));
    printf("b is %f + %fi\n", creal(b), cimag(b));
    printf("a + b is: %f + %fi\n", creal(sum), cimag(sum));
    printf("a - b is: %f + %fi\n", creal(a - b), cimag(a - b));
    printf("a * b is: %f + %fi\n", creal(a * b), cimag(a * b));
    printf("a / b is: %f + %fi\n", creal(a / b), cimag(a / b));
    printf("a ^ b is: %f + %fi\n", creal(pwr), cimag(pwr));
}
```

Fig. E.8 | Using complex numbers in C99. (Part 1 of 2.)

2. In GNU gcc, the function cpow (line 13 in Fig. E.8) is not supported. Microsoft Visual C++ supports the complex-number features defined by the C++ standard, not those from C99.