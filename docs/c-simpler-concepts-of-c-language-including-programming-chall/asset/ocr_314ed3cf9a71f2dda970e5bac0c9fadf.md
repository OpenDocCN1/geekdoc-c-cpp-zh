```
#include<stdio.h>
void main()
{
    int i,j;
    float f;
    i=10;
    j=20;
    f=i/j;
    printf("%f",f);
    getch();
}
```

# Program 4.5 Casting need

As the above program shows, the operation (i/j) will produce the answer 0.5. But since both the operands are int, the result will be 0 (truncating the fractional part). When the program is executed, the following output is obtained.

(10/20) is 0.000000

# Output 4.5

In order to obtain the accurate result, the help of casting operator will be expected. How to perform casting? It's simple. Just append (float) before (i/j). Refer to the following Program 4.6.

```
#include<stdio.h>
void main()
{
    int i,j;
    float f;
    i=10;
    j=20;
    f=(float)i/j;
    printf("%d/%d is %f",i,j,f);
    getch();
}
```

# Program 4.6 Casting example

When the program is executed, the following result is obtained. Now, the result is accurate.

(10/20) is 0.500000_

The point to be noted in Program 4.6 is, when we cast one of the operands, the other operand is also converted to float. And hence the output! So, in general, the following rules are proved for type conversions.

+   - If either operand is long double, convert the other to long double.
- Otherwise, if either operand is double, convert the other to double.
- Otherwise, if either operand is float, convert the other to float.
- Otherwise, convert char and short to int.
- Then, if either operand is long, convert the other to long.

Also, beware of the fact that type conversions can't be performed on the left hand side of the assignment operator!