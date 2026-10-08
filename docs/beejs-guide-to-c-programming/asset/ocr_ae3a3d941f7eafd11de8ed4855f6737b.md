# Chapter 13

# Scope

Scope is all about what variables are visible in what contexts.

# 13.1 Block Scope

This is the scope of almost all the variables devs define. It includes what other languages might call “function scope”, i.e. variables that are declared inside functions.

The basic rule is that if you've declared a variable in a block delimited by squirrelly braces, the scope of that variable is that block.

If there's a block inside a block, then variables declared in the inner block are local to that block, and cannot be seen in the outer scope.

Once a variable's scope ends, that variable can no longer be referenced, and you can consider its value to go into the great bucket¹ in the sky.

An example with nested scope:

```
#include <stdio.h>

int main(void)
{
    int a = 12;           // Local to outer block, but visible in inner block

    if (a == 12) {
        int b = 99;      // Local to inner block, not visible in outer block

        printf("%d %d\n", a, b); // OK: "12 99"
    }

    printf("%d\n", a);      // OK, we're still in a's scope
    printf("%d\n", b);      // ILLEGAL, out of b's scope
}
```

> ¹https://en.wikipedia.org/wiki/Bit_bucket