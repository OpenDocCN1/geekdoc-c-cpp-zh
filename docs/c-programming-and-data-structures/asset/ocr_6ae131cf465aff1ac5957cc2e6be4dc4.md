# 4. Reliability Graph

Problem: The reliability of an electronic component is given by reliability (r) = e^(-λ t) where λ is the component failure rate per hour and t is the time of operation in hours. A graph is required to determine the reliability at various operating times, from 0 to 3000 hours. The failure rate λ (lambda) is 0.001.

# Problem

```
```c
#include <math.h>
#define LAMBDA 0.001
main()
{
    double t;
    float r;
    int i, R;
    for (i=1; i<=27; ++i)
    {
        printf("—");
    }
    printf("\n");
    for (t=0; t<=3000; t+=150)
    {
        r = exp(-LAMBDA*t);
        R = (int)(50*r+0.5);
        printf(" |");
        for (i=1; i<=R; ++i)
        {
            printf("*");
        }
        printf("#\n");
    }
    for (i=1; i<=3; ++i)
    {
        printf(" |\n");
    }
}
```
```

# Output

```
```
_________________________
|******************************#
|*****************************#
|***************************#
|*************************#
|**********************#
|*******************#
|****************#
|*************#
|**********#
|********#
|******#
|****#
|***#
|**#
|*#
```
```