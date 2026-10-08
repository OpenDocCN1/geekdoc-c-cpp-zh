# 432 One-Dimensional Arrays

```
amin <- a[i]
end for
return
end
```

Program

```
#include <stdio.h>
# define N 10
void maxmin(int, float [ ], float *, float *);

int main()
{
    int i;
    float number[N], amax, amin;
    printf("Enter the Numbers:\n");
    for(i = 0; i < N; i++)
    scanf("%f", &number[i]);
```