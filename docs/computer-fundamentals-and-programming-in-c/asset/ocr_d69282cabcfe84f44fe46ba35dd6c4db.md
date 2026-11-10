```
result = b * c;        /* multiplication */
printf("b * c = %d \n", result);
result = a / c;        /* division */
printf("a / c = %d \n", result);
result = a + b * c;
printf("a + b * c = %d \n", result);
printf("a + b * c + d = %d\n", a+b*c+d);
return 0;
}
```

**Output**

```
a - b = 98
b * c = 50
a / c = 4
a + b * c = 150
a * b + c * d = 300
```

```
2.  #include <stdio.h>
    int main()
    {
        int a = 25;
        int b = '2';
        int result;
        float c = 25.0;
        float d = 2.0;
        printf("6 + a / 5 * b = %d \n", 6 + a / 5 * b);
        printf("a / b * b = %d\n", a / b * b);
        printf("c / d * d = %f\n", c / d * d);
        printf("-a = %d\n",-a);
        return 0;
    }
```

**Output**

```
6 + a / 5 * b = 16
a / b * b = 24
c / d * d = 25.000000
-a = -25
```

Note the difference between this and the previous program. When we evaluate 6 + a / 5 * b, we have not stored its value in any variable, but it is evaluated in the printf statement itself and printed straight away.

# Note

```
op1/op2
op1%op2
```

For / and %, op2 must be non-zero: op2 = 0 results in an error (We cannot divide by zero.). When op1 and op2 are integers and the quotient is not an integer, then the following points have to be noted:

+   - If op1 and op2 have the same sign, op1/op2 is the largest integer less than the true quotient, then op1%op2 has the sign of op1.
+   - If op1 and op2 have opposite signs, op1/op2 is the smallest integer greater than the true quotient, then op1%op2 has the sign of op1.

It is to be noted that rounding off is always towards zero.

+   - % operator returns the remainder of an integer division. i.e., x%y = x - (x/y)*y, where x and y both are of integer types. This operator can be applied only to integer operands and cannot be applied to operands of type float or double. The following example shows the occurrence of compiler error when the % operator is applied on a floating-point number:

```
#include <stdio.h>
int main()
{
    float c = 3.14;
    printf("%f", c%2);
    return 0;
}
```

# Check Your Progress

1. What will be the output of the following programs?

```
(a)  #include <stdio.h>
     int main()
     {
         int x = 5, y = 7, z;
         z = x + y;
         printf("The value of x is: %d\n", x);
         printf("The value of y is: %d\n", y);
         printf("Their sum, z, is: %d\n", z);
         return 0;
     }
```

**Output**

```
The value of x is: 5
The value of y is: 7
Their sum, z, is: 12
```

```
(b)  #include <stdio.h>
     int main()
     {
         int a, b, c; /* a, b and c are undefined. */
         c = a + b;
         printf("The value of a is: %d\n", a);
         printf("The value of b is: %d\n", b);
         printf("Their sum, c, is: %d\n", c);
         return 0;
     }
```

**Output**

```
The value of a is: 2146744409
The value of b is: 2146744417
Their sum, c, is: -1478470
```