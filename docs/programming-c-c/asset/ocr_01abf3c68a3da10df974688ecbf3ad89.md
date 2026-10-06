# Lab Programming

```
return0;
}
```

# Output

Enter a character: G
ASCII value of G = 71

# 5. Write a C Program to compute quotient and remainder.

```
#include<stdio.h>
int main(){
    int dividend, divisor, quotient, remainder;
    printf("Enter dividend: %d", &dividend);
    scanf("%d", &dividend);
    printf("Enter divisor: %d", &divisor);
    scanf("%d", &divisor);

    // Computes quotient
    quotient = dividend / divisor;

    // Computes remainder
    remainder = dividend % divisor;

    printf("Quotient = %d\n", quotient);
    printf("Remainder = %d\n", remainder);
    return0;
}
```

# Output

Enter dividend: 25
Enter divisor: 4
Quotient = 6
Remainder = 1

# 6. Write a C Program to find the size of int, float, double and char.

```
#include<stdio.h>
int main(){
    int intType;
    float floatType;
    double doubleType;
    char charType;

    // sizeof evaluates the size of a variable
```