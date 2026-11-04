```
```c
                tot_grd[j] += firm_grd[i][j]; /* Each tot_grd[j]
holds the total score of the respective firm. */
            }
            getchar();
        }
        for(i = 0; i < MAX_FIRMS-1; i++)
        {
            for(j = i+1; j < MAX_FIRMS; j++)
            {
                if(tot_grd[i] < tot_grd[j])
                {
                    /* Swap grades and the corresponding names. */
                    k = tot_grd[i];
                    tot_grd[i] = tot_grd[j];
                    tot_grd[j] = k;

                    strcpy(tmp, firm_name[j]);
                    strcpy(firm_name[j], firm_name[i]);
                    strcpy(firm_name[i], tmp);
                }
            }
        }
        for(i = 0; i < MAX_FIRMS; i++)
            printf("%s: %d\n", firm_name[i], tot_grd[i]);
        return 0;
}
```
```

C.20.7 What is the output of the following program?

```
```c
#include <stdio.h>

void test(int **tmp);

int main(void)
{
    int *ptr, arr[] = {5, 10, 15};

    ptr = arr;
    test(&ptr);

    printf("%d ", *ptr);
    return 0;
}

void test(int **tmp)
{
    int i;

    i = *(*tmp)++;
    printf("%d ", i);

    i = ++(**tmp);
    printf("%d ", i);
}
```
```