# 11.22 C Programming and Data Structures

```
```c
/* ILLUSTRATION OF POINTERS TO FUNCTIONS */
#include <math.h>
/*define PI 3.1415926 */
main()
{
double y(); table();
printf("Table of y(x)=2*x-x-x+1\n");
table(y, 0.0, 2.0, 0.5);
printf("\nTable of cos(x)\n");
table(cos, 0.0, PI, 0.5);
}
double table(f, min, max, step)
double f();
double min, max, step;
{
double a, value;
for(a = min; a <= max; a += step)
{
value = (f)(a);
printf("%5.2f%10.4f\n", a, value);
}
}
double y(x)
double x;
{
return(2*x*x-x+1);
}
double cos(x)
double x;
{
return(cos(x));
}
```
```

| a   | value   |
|-----|---------|
| 0.00 | 1.0000 |
| 0.50 | 2.0000 |
| 1.00 | 4.0000 |
| 1.50 | 7.0000 |
| 2.00 | 10.0000 |

| a   | value   |
|-----|---------|
| 0.00 | 1.0000 |
| 0.50 | 0.8776 |
| 1.00 | 0.5403 |
| 1.50 | 0.0707 |
| 2.00 | -0.4161 |
| 2.50 | -0.8011 |
| 3.00 | -0.9900 |

> Fig. 11.14 Use of pointers to functions

we pass a pointer to the function y as the first parameter of table. Note that y is not followed by a parameter list,