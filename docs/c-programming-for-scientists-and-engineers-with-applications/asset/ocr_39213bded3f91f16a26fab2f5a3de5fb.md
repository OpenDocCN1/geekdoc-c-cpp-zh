```
/* area - area of the triangle */
/* */
/****************************************************************/

#include <stdio.h>
#include <math.h>
int main()
{
    int a, b, c;
    float s, area;

    printf("Input integer values for the Sides:\n");
    scanf("%d %d %d", &a, &b, &c);
    printf("\nThe Sides of the Triangle: %d %d %d\n", a, b, c);

    if(a > 0 && b > 0 && c > 0)
    {
        s = (a + b + c) / 2.0;
        if(s > a && b > b && s > c)
        {
            area = sqrt(s * (s - a) * (s - b) * (s - c));
            printf("The Area of the Triangle: %5.2f\n", area);
        }
    }

    return 0;
}
```

Input and Output

Input integer values for the Sides:
12 14 16

The Sides of the Triangle: 12 14 16
The Area of the Triangle: 81.33