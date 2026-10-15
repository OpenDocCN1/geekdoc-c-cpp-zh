# 2.5 Input & Output on Console

You may want to show message on console using C. You can use printf() to write message on console. printf() also can be passed parameters inside using %d for integer numeric and %f for floating numeric. For char data type, we can use %c for passing parameter.

Here is a sample code

```
#include <stdio.h>

int main() {
    int n = 10;
    float m = 1.245;
    char c = 'A';

    printf("%d \n",n);
    printf("%f \n",m);
    printf("%.2f \n",m);
    printf("%.3f \n",m);
    printf("%c \n",c);

    return 0;
}
```

Save this code into a file, called inout.c.

Compile and run this code

![](bbox=[0.06, 0.59, 0.84, 0.77])

You can see on %f that wrote floating data with 6 decimal digits. You can specify the number of decimal digit by passing numeric after dot (.), for instance, %.2f and %.3f.