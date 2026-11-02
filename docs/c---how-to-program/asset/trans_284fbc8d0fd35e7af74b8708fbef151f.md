
将 true 替换为 1，将 false 替换为 0，并将 bool 替换为关键字 `_Bool`。图 E.5 使用了一个名为 isEven 的函数（第 29–37 行），如果该函数的实参为偶数，则返回 bool 值 true；如果为奇数，则返回 false。

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

**图 E.5** | 在 C99 中使用 bool 类型以及 true 和 false 值。

第 16 行声明了一个名为 valueIsEven 的 bool 变量。循环中的第 13–14 行提示并获取下一个整数。第 16 行将输入传递给函数 isEven（第 29–37 行）。函数 isEven 返回一个 bool 类型的值。第 31 行判断实参是否能被 2 整除。如果是，第 32 行返回 true（即该数为偶数）；否则，第 35 行返回 false（即该数为奇数）。结果在第 16 行赋给 bool 变量 valueIsEven。如果 valueIsEven 为 true，第 20 行显示一个表示该值为偶数的字符串。如果 valueIsEven 为 false，第 23 行显示一个表示该值为奇数的字符串。

## E.5 函数声明中的隐式 int

[本节可在第 5.5 节之后阅读。]

在 C99 之前，如果函数没有显式返回类型，则隐式假定其返回 int。此外，如果函数未指定参数类型，则该类型隐式变为 int。请考虑图 E.6 中的程序。

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

**图 E.6** | 在 C99 之前使用隐式 int。

当该程序在不符合 C99 的编译器中运行时，不会出现编译错误或警告消息，并且程序会正确执行。C99 不允许使用隐式 int，要求符合 C99 的编译器发出警告或错误。在符合 C99 的编译器上，该程序会生成警告或错误。图 E.7 显示了 GNU gcc 4.9.2 产生的警告消息。

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

**图 E.7** | gcc 针对隐式 int 产生的警告消息。

## E.6 复数

[本节可在第 5.3 节之后阅读。]

C99 标准引入了对复数和复数算术的支持。图 E.8 中的程序对复数执行基本操作。我们在 Apple 的 Xcode 6 中的 LLVM 编译器上编译并运行了该程序：

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

**图 E.8** | 在 C99 中使用复数。（第 1 部分，共 2 部分。）

2. 在 GNU gcc 中，不支持函数 cpow（图 E.8 中的第 13 行）。Microsoft Visual C++ 支持由 C++ 标准定义的复数特性，而不是 C99 中的那些特性。

```text
a is 32.123000 + 24.456000i
b is 23.789000 + 42.987000i
a + b is: 55.912000 + 67.443000i
a - b is: 8.334000 - 18.531000i
a * b is: -302.822025 + 2198.639851i
a / b is: 0.752119 - 0.331050i
a ^ b is: -17857.051995 + 1365.613958i
```

**图 E.8** | 在 C99 中使用复数。（第 2 部分，共 2 部分。）

为了让 C99 识别 complex，我们包含 `<complex.h>` 头文件（第 4 行）。这会将宏 `complex` 展开为关键字 `_Complex`——该类型保留一个恰好包含两个元素的数组，分别对应复数的*实部*和*虚部*。

在第 4 行包含该头文件后，我们可以像第 8–10 行和第 12–13 行那样定义变量。我们将变量 *a*、*b*、*c*、*sum* 和 *pwr* 分别定义为 `double complex` 类型。我们也可以使用 `float complex` 或 `long double complex`。

算术运算符也适用于复数。`<complex.h>` 头文件还定义了几个数学函数，例如第 13 行中的 `cpow`。你还可以对复数使用运算符 `!`、`++`、`--`、`&&`、`||`、`==`、`!=` 以及一元 `&`。

第 17–21 行输出各种算术运算的结果。复数的*实部*和*虚部*可以分别通过函数 `creal` 和 `cimag` 访问，如第 15–21 行所示。在第 21 行的输出字符串中，我们使用符号 `^` 表示幂运算。

## E.7 预处理器的新增功能

[本节可在第 13 章之后阅读。]

C99 为 C 预处理器增加了功能。第一个是 `_Pragma` 运算符，其作用类似于第 13.6 节介绍的 `#pragma` 指令。`_Pragma ("tokens")` 与 `#pragma tokens` 效果相同，但更灵活，因为它可以在宏定义内部使用。因此，不必用 `#if` 指令包围编译器特定 pragma 的每次使用，你只需使用 `_Pragma` 运算符定义一次宏，即可在程序中的任何位置使用它。

其次，C99 规定了三个标准 pragma，用于处理浮点运算的行为。这些标准 pragma 中的第一个标记始终是 `STDC`；第二个是 `FENV_ACCESS`、`FP_CONTRACT` 或 `CX_LIMITED_RANGE` 之一；第三个是 `ON`、`OFF` 或 `DEFAULT`，分别表示应启用、禁用给定 pragma，还是将其设为默认值。`FENV_ACCESS` pragma 用于告知编译器哪些代码部分将使用 C99 `<fenv.h>` 头文件中的函数。在现代桌面系统中，浮点处理使用 80 位浮点值完成。如果启用 `FP_CONTRACT`，编译器可以以此精度执行一系列运算，并将最终结果存储到精度较低的 `float` 或 `double` 中，而不是在每次运算后都降低精度。最后，如果启用 `CX_LIMITED_RANGE`，则允许编译器对复数运算（例如乘法或除法）使用标准数学公式。由于浮点数*并非*精确存储，使用常规数学定义可能导致*溢出*，即数值变得大于浮点类型所能表示的范围，即使操作数和结果都低于该限制。
