# Program

```
```c
#include<stdio.h>
#include<float.h>
#include<math.h>
void main()
{
    int i;
    float x,sum,fact,term;
    printf("\\n You have this series : 1+x/1!+x^2/2!+x^3/3!+x^4/4!+..... x^n/n!");
    printf("\\n\\n Enter the value for X:");
    scanf("%f",&x);
    i=1;
    sum=0;
    term=1;
    fact=1;
    while(term>=FLT_EPSILON)
    {
        fact*=i;
        sum+=term;
        term=pow(x,i)/fact;
        i++;
    }
    printf("\\n\\n The Calculated value of e^% .3f = %f",x,sum);
    printf("\\n\\n The Library Function Value of e^%.3f = %f",x,
    exp(x));
}
```
```

# Sample Output

```
```text
You have this series: 1+x/1!+x^2/2!+x^3/3!+x^4/4!+.....x^n/n!
Enter the value for X: 0.5
The Calculated value of e^0.500=1.648721
The Library Function Value of e^0.500=1.648721
```
```

# Outcomes

+   - Should be able to write C programs for any **statistical and mathematical functions**.
+   - Capable of refining the program till the required accuracy is attained.