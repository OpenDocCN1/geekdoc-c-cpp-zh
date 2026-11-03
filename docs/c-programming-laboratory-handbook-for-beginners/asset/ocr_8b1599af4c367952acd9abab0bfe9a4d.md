```
switch(option)
{
    case 1: printf("\\nThe roots are real and equal\\n");
        r1=r2=-b/(2.0*a);
        printf("\\nThe roots are \\nr1 =\\t%f\\n\\tr2 =\\t%f\\n", r1, r2);
        break;
    case 2: printf("\\nThe roots are real and distinct\\n");
        r1=(-b+r)/(2.0*a);
        r2=(-b-r)/(2.0*a);
        printf("\\nThe roots are \\ntr1 =\\t%f\\ntr2 =\\t%f\\n",
        r1, r2);
        break;
    case 3: printf("\\nThe roots are complex\\n");
        r1=-b/(2.0*a);
        r2=r/(2.0*a);
        printf("\\nThe roots are:\\ntr1=%f +i %f\\ntr2=%f -i
%f\\n", r1, r2, r1, r2);
        break;
}/* End Switch */
}/* End program */
```

# Output

```
1.
Quadratic Equation ax^2+bx+c=0
**************************************
a=0
b=1
c=2
Invalid Input

2.
Quadratic Equation ax^2+bx+c=0
**************************************
a=1
b=2
c=1
The roots are real and equal
The roots are
    r1=-1.000000
    r2=-1.000000
```