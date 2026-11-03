The cost is 40 when p = 0, and 33 when p = 1 and 60 when p = 10. The cost, therefore, decreases first and then increases. The program in Fig. 4.27 evaluates the cost at successive intervals of p (in steps of 0.1) and stops when the cost begins to increase. The program employs break and continue statements to exit the loop.

```
Program
main()
{
    float p, cost, p1, cost1;
    for (p = 0; p <= 10; p = p + 0.1)
    {
        cost = 40 - 8 * p + p * p;
        if(p == 0)
        {
            cost1 = cost;
            continue;
        }
        if (cost >= cost1)
            break;
        cost1 = cost;
        p1 = p;
    }
    p = (p + p1)/2.0;
    cost = 40 - 8 * p + p * p;
    printf("\nMINIMUM COST = %.2f AT p = %.1f\n",
        cost, p);
}

Output
    MINIMUM COST = 24.00 AT p = 4.0
```

Fig. 4.27 Program of minimum cost problem

# 4. Plotting of Two Functions

Problem: We have two functions of the type

y1 = exp (-ax)
y2 = exp (-ax^2/2)

Plot the graphs of these functions for x varying from 0 to 5.0.

```
Program
#include <math.h>
main()
{
    int i;
    float a, x, y1, y2;
    a = 0.4;
    printf(" y ---- \n");
```