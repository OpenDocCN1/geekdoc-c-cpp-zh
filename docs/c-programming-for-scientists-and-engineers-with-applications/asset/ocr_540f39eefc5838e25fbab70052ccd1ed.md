# 6.1 Scope of Variables

The scope of a variable is defined as that part of a program where the name of the variable is known and its storage can be accessed. This depends on where in the program it is declared. If a variable is declared ahead of the definition of the main and all other functions it has global scope. Global scope means the functions can reference the variable name and access its storage. If a variable is declared inside the main, it is local to the main; it has local scope and it can be referenced and accessed by that name only inside the main.

# 6.1.1 Block Structure

The variables declared in a C program have block scope. A block is a collection of statements enclosed between left and right braces. All functions are block structures in C. A variable may be declared outside or inside a block. If a variable is declared outside a block and another variable with the same name is declared inside a block, the name will reference the one inside the block rather than the one declared outside the block while the block is being executed. The variable declared outside is suspended until execution of the block finishes, but it still exists. The following examples show the scope of variables in a block structure.

Example 1

```
#include <stdio.h>
int main() {
    int a = 10;
    printf("a = %d\n", a); /* 1 * */
    int b = 5;
    printf("b = %d\n", b); /* 2 * */
    b = b + 15;
    printf("b = %d\n", b); /* 3 * */
    int c = 40;
    printf("c = %d\n", c); /* 4 * */
}
     = b + 4;
    printf("b = %d\n", b); /* 5 * */
    a = a + 15;
    printf("a = %d\n", a); /* 6 * */
    return 0;
}
```

![](bbox=[0.593, 0.638, 0.913, 0.935])