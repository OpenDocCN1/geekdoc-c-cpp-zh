# Introduction to C++

When the preprocessor expands the f macro, it replaces #s with the name of the argument, and that, str. Then the program displays: str = text

The ## operator is used to merge identifiers together. It is not allowed to appear in the beginning or at the end of the sequence. If it identifies a macro parameter, the preprocessor first replaces it with the value of the argument and then passing others. For example:

```
#include <iostream> // Example 15.9

#define f(a) s##u##m##a

int sum(int a, int b);

int main() {
    int i, j;

    std::cout << "Enter numbers: ";
    std::cin >> i >> j;
    std::cout << f(i, j) << '\n';
    return 0;
}

int sum(int a, int b) {
    return a+b;
}
```

When the preprocessor expands the f macro, because the character a has the same name with the argument, the preprocessor replaces a with the value of the argument, that is, 1, and then merges value with the s, u, and m characters. Therefore, f1(i, j) is expanded to sum1(i, j) and the program uses sum1() to display the sum of the two inputs.

# PREPROCESSOR DIRECTIVES
CONDITIONAL COMPILATION

This section discusses the preprocessor directives that allow the conditional compilation of a part of the program. The conditional compilation can be very useful in many situations, for example, when debugging the program, to monitor the program execution or maintain multiple versions of the same program.

# #if, #else, #elif, and #endif Directives

The #if and #endif directives are used to define which parts of a program will be compiled, depending on the value of an expression. The general syntax is:

```
#if expression
... /* block of statements. */
#endif
```

The expression is a constant integer expression which is not allowed to include sizeof, casts, or enum constants. If its value is true, the preprocessor keeps the block of statements to be compiled.