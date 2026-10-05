If not, the block is removed and the compiler won't see it. Notice that if the expression is an undefined identifier, the #if directive evaluates to false. For example:

```
#if NUM
```

If NUM is not defined, the outcome is false, while the value of #if !NUM is true. If NUM is defined value 0, #if NUM evaluates to false and #if !NUM to true.

The #else directive is used in conjunction with the #if directive to define a block of statements that will be compiled if the value of the expression is false.

```
#if expression
    /* block of statements A */
#else
    /* block of statements B */
#endif
```

For example, in the following program, the #else part will be compiled because NUM is greater than 0:

```
#include <iostream> // Example 15.10

#define NUM 10

int main()
{
    #if NUM < 0
        std::cout << "Seg_1\n";
    #else
        std::cout << "Seg_2\n";
    #endif
    return 0;
}
```

Therefore, the program displays Seg_2. Notice that if the definition of NUM was missing, the program would display Seg_2, too.
Since nested comments are not allowed, it is not possible to put in comments of a program that contains comments. To do that, we can use the #if directive. For example:

```
#if 0
    /* Comment. */
    /* Code. */
    /* Another comment. */
#endif
```

The #elif directive can be used with #if, #ifdef, and #ifndef directives to define multiple compilation paths. For example:

```
#if expression_A
    /* block of statements A */
#elif expression_B
    /* block of statements B */
#else
    /* block of statements N */
#endif
```