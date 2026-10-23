```
for(int i=1; i<=n; i++)
    result *= i;
    return result;
} /* compute n! using a loop */
```

The instruction that follows the loop heading can by itself be a loop. This structure is known as nested loops (Figure 1.3). Here is a program that uses nested loops to print a checkerboard:

```
#include<stdio.h>
int main(){
    for(int i=0;i<8;i++){
    for(int j=0;j<8;j++)
        printf("%c ",((i+j)%2)?'*':'o');
    printf("\n");
    }
    return 0;
} /* print a checkerboard */
```

![](bbox=[0.25, 0.59, 0.85, 0.82])

Figure 1.3. Nested loops: the outer loop goes over i = 0, 1, 2; for each particular i, the inner loop goes over j = 0, 1, 2.

# 1.12 Example: Reversed Integer

Here we show how a loop can be used in a function that reverses the order of the digits in an arbitrarily long integer number. For example, for the concrete argument 123, it returns the output 321: