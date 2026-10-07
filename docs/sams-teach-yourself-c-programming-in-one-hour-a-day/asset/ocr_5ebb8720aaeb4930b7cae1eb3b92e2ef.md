# 4. Yes, you need to pass the variable var to print it in a different function.

```
/* Using a local variable */
#include <stdio.h>

void print_value(int var) {

int main( void ) {
    int var = 99;
    print_value( var );

    return 0;
}

void print_value(int var) {
    printf("The value is %d\n", var);
}
```

# 5. Yes, a program can have a local and global variable with the same name. In such cases, active local variables take precedence.

```
/* Using a global */
#include <stdio.h>

int var = 99;
void print_func(void);

int main( void ) {
    int var = 77;
    printf("Printing in function with local and global:*");
    printf("\nThe value of var is %d", var);
    print_func();

    return 0;
}
void print_func(void) {
    printf("\nPrinting in function only global:*");
    printf("\nThe value of var is %d\n", var);
}
```

# 6. There is only one problem with a_sample_function(). Variables can be declared at the beginning of any block, the declarations of crtl and star are fine. The other variable, ctr2, is not declared at the beginning of a block; it needs to be. The following is the corrected function within a complete program.