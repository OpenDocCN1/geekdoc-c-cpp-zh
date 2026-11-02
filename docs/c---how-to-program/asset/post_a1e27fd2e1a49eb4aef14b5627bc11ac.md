
Replace true with 1, false with 0 and bool with the keyword `_Bool`. Figure E.5 uses a function named isEven (lines 29–37) that returns a bool value of true if the function’s argument is even and false if it’s odd.

```c
// Fig. E.5: figE_05.c
// Using the type bool and the values true and false in C99.
#include <stdio.h>
#include <stdbool.h> // allows the use of bool, true, and false

bool isEven(int number); // function prototype

int main(void)
{
    // loop for 2 inputs
    for (int i = 0; i < 2; ++i) {
        printf("Enter an integer: ");
        int input; // value entered by user
        scanf("%d", &input);

        bool valueIsEven = isEven(input); // determine if input is even

        // determine whether input is even
        if (valueIsEven) {
            printf("%d is even \n\n", input);
        }
        else {
            printf("%d is odd \n\n", input);
        }
    }
}

// isEven returns true if number is even
bool isEven(int number)
{
    if (number % 2 == 0) { // is number divisible by 2?
        return true;
    }
    else {
        return false;
    }
}
```

```text
Enter an integer: 34
34 is even

Enter an integer: 23
23 is odd
```

**Fig. E.5** | Using the type bool and the values true and false in C99.

Line 16 declares a bool variable named valueIsEven. Lines 13–14 in the loop prompt for and obtain the next integer. Line 16 passes the input to function isEven (lines 29–37). Function isEven returns a value of type bool. Line 31 determines whether the argument is divisible by 2. If so, line 32 returns true (i.e., the number is even); otherwise, line 35 returns false (i.e., the number is odd). The result is assigned to bool variable valueIsEven in line 16. If valueIsEven is true, line 20 displays a string indicating that the value is even. If valueIsEven is false, line 23 displays a string indicating that the value is odd.

## E.5 Implicit int in Function Declarations

[This section can be read after Section 5.5.]

Prior to C99, if a function does not have an explicit return type, it implicitly is assumed to return an int. In addition, if a function does not specify a parameter type, that type implicitly becomes int. Consider the program in Fig. E.6.

```c
// Fig. E.6: figE_06.c
// Using implicit int prior to C99
#include <stdio.h>

returnImplicitInt(); // prototype with unspecified return type
int demoImplicitInt(x); // prototype with unspecified parameter type

int main(void)
{
    // assign data of unspecified return type to int
    int x = returnImplicitInt();

    // pass an int to a function with an unspecified type
    int y = demoImplicitInt(82);

    printf("x is %d\n", x);
    printf("y is %d\n", y);
}

returnImplicitInt()
{
    return 77; // returning an int when return type is not specified
}

demoImplicitInt(x)
{
    return x;
}
```

**Fig. E.6** | Using implicit int prior to C99.

When this program is run in compilers that are not C99 compliant, no compilation errors or warning messages occur and the program executes correctly. C99 disallows the use of the implicit int, requiring that C99-compliant compilers issue either a warning or an error. On C99-compliant compilers this program generates warnings or errors. Figure E.7 shows the warning messages from GNU gcc 4.9.2.

```text
test.c:5:1: warning: data definition has no type or storage class
returnImplicitInt(); // prototype with unspecified return type
^
test.c:5:1: warning: type defaults to 'int' in declaration of 'returnImplicitInt'
test.c:6:1: warning: parameter names (without types) in function declaration
int demoImplicitInt(x); // prototype with unspecified parameter type
^
test.c:20:1: warning: return type defaults to 'int'
returnImplicitInt()
^
test.c: In function 'demoImplicitInt':
test.c:25:5: warning: type of 'x' defaults to 'int'
demoImplicitInt(x)
^
```

**Fig. E.7** | Warning messages for implicit int produced by gcc.

## E.6 Complex Numbers

[This section can be read after Section 5.3.]

The C99 standard introduced support for complex numbers and complex arithmetic. The program of Fig. E.8 performs basic operations with complex numbers. We compiled and ran this program on the LLVM compiler in Apple's Xcode 6:

```c
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

**Fig. E.8** | Using complex numbers in C99. (Part 1 of 2.)

2. In GNU gcc, the function cpow (line 13 in Fig. E.8) is not supported. Microsoft Visual C++ supports the complex-number features defined by the C++ standard, not those from C99.

```text
a is 32.123000 + 24.456000i
b is 23.789000 + 42.987000i
a + b is: 55.912000 + 67.443000i
a - b is: 8.334000 - 18.531000i
a * b is: -302.822025 + 2198.639851i
a / b is: 0.752119 - 0.331050i
a ^ b is: -17857.051995 + 1365.613958i
```

**Fig. E.8** | Using complex numbers in C99. (Part 2 of 2.)

For C99 to recognize complex, we include the `<complex.h>` header (line 4). This will expand the macro `complex` to the keyword `_Complex`—a type that reserves an array of exactly two elements, corresponding to the complex number's *real part* and *imaginary part*.

Having included the header file in line 4, we can define variables as in lines 8–10 and 12–13. We define each of the variables *a*, *b*, *c*, *sum* and *pwr* as type `double complex`. We also could have used `float complex` or `long double complex`.

The arithmetic operators also work with complex numbers. The `<complex.h>` header also defines several math functions, for example, `cpow` in line 13. You can also use the operators `!`, `++`, `--`, `&&`, `||`, `==`, `!=` and unary `&` with complex numbers.

Lines 17–21 output the results of various arithmetic operations. The *real part* and the *imaginary part* of a complex number can be accessed with functions `creal` and `cimag`, respectively, as shown in lines 15–21. In the output string of line 21, we use the symbol `^` to indicate exponentiation.

## E.7 Additions to the Preprocessor

[This section can be read after Chapter 13.]

C99 adds features to the C preprocessor. The first is the `_Pragma` operator, which functions like the `#pragma` directive introduced in Section 13.6. `_Pragma ("tokens")` has the same effect as `#pragma tokens`, but is more flexible because it can be used inside a macro definition. Therefore, instead of surrounding each usage of a compiler-specific pragma by an `#if` directive, you can simply define a macro using the `_Pragma` operator once and use it anywhere in your program.

Second, C99 specifies three standard pragmas that deal with the behavior of floating-point operations. The first token in these standard pragmas is always `STDC`; the second is one of `FENV_ACCESS`, `FP_CONTRACT` or `CX_LIMITED_RANGE`, and the third is `ON`, `OFF` or `DEFAULT` to indicate whether the given pragma should be enabled, disabled, or set to its default value, respectively. The `FENV_ACCESS` pragma is used to inform the compiler which portions of code will use functions in the C99 `<fenv.h>` header. On modern desktop systems, floating-point processing is done with 80-bit floating-point values. If `FP_CONTRACT` is enabled, the compiler may perform a sequence of operations at this precision and store the final result into a lower-precision `float` or `double` instead of reducing the precision after each operation. Finally, if `CX_LIMITED_RANGE` is enabled, the compiler is allowed to use the standard mathematical formulas for complex operations such as multiplying or dividing. Because floating-point numbers are *not* stored exactly, using the normal mathematical definitions can result in *overflow* where the numbers get larger than the floating-point type can represent, even if the operands and result are below this limit.
