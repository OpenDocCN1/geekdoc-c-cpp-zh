# Case 1.

int num1 = 80;

int num2 = 40;

condition: (num1 > num2) , if (80 > 40), will evaluate to “true”

if(condition) will be “true” and executes the if-block.

![](bbox=[0.2, 0.35, 0.9, 0.55])

# StatementIfElse.c

```
#include <stdio.h>

int main() {
    int num1 = 80;
    int num2 = 40;
    if( num1 > num2) {
        printf("%d is greater than %d",num1,num2);
    }else {
        printf("%d is less than or equals to %%d", num1, num2);
    }
    return 0;
}
```

# Output

80 is greater than 40