# Functions-Modular Programming 5.49

```
printf("Enter upper limit:");
scanf("%f", &end point);
printf("Enter number of trapezoids:");
scanf("%d", &numtraps);
}
float find_area(float a, float b, int n)
{
float base, lower, h1, h2; /* LOCAL VARIABLES */
float function_x(float x); /* prototype */
float trap_area(float h1,float h2,float base);/*prototype*/
base = (b-1)/n;
lower = a;
for(lower =a; lower <= b-base; lower = lower + base)
{
h1 = function_x(lower);
h1 = function_x(lower + base);
total area += trap_area(h1, h2, base);
}
return(total_area);
float trap_area(float height_1,float height_2,float base)
{
float area; /* LOCAL VARIABLE */
area = 0.5 * (height_1 + height_2) * base;
return(area);
}
float function_x(float x)
{
/* F(x) = x * x + 1 */
return(x*x + 1);
}
```

Output

AREA UNDER A CURVE
Enter lower limit: 0
Enter upper limit: 3
Enter number of trapezoids: 30
TOTAL AREA = 12.005000

AREA UNDER A CURVE
Enter lower limit: 0
Enter upper limit: 3
Enter number of trapezoids: 100
TOTAL AREA = 12.004038

> Fig. 5.21 Computing area under a curve