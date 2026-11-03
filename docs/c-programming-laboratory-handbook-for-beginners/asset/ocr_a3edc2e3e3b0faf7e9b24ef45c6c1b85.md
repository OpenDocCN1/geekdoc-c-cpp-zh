# Related Program

# Program 1

Program in C to find and output all the roots of a given quadratic equation, for non-zero coefficients, **using Switch statement.**

```
#include<stdio.h>
#include<math.h>
#include<process.h>
void main()
{
    int option;
    double a, b, c, d;
    double r,r1,r2;
    printf(" Quadratic Equation ax^2+bx+c=0 \n");
    printf("*******************************\n");

    /* Get a, b, and c from user */
    printf("\n a=");
    scanf("%lf", &a);
    printf("b=");
    scanf("%lf", &b);
    printf("c=");
    scanf("%lf", &c);

    if(a==0) /* check for valid input */
    {
        printf("\n Invalid Imput \n");
        exit(0);
    }

    /* Calculate determinant */
    d=(b*b)-(4*a*c);
    r=sqrt(abs(d));
    if(d==0)
       option=1;
    else if(d>0)
       option=2;
    else
       option=3;
    /* Use switch statement */
```