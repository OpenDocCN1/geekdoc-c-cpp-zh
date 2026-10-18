return;
}

Let us now call the function swap() by passing values by reference as in the following example:

```
#include <stdio.h>

/* function declaration */
void swap(int *x, int *y);

int main ()
{
    /* local variable definition */
    int a = 100;
    int b = 200;

    printf("Before swap, value of a : %d\n", a );
    printf("Before swap, value of b : %d\n", b );

    /* calling a function to swap the values.
    * &a indicates pointer to a i.e. address of variable a and
    * &b indicates pointer to b i.e. address of variable b.
    */
    swap(&a, &b);

    printf("After swap, value of a : %d\n", a );
    printf("After swap, value of b : %d\n", b );

    return 0;
}
```

Let us put the above code in a single C file, compile and execute it, to produce the following result:

```
Before swap, value of a :100
Before swap, value of b :200
```