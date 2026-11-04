```
for(i = 0; i < 100; i++)
{
    printf("Enter price: ");
    scanf("%f", &arr[i]);
    if(arr[i] == -1)
        break;
}
if(i == 0)
    return 0;
/* The variable i indicates how many prices were stored into the array. For example, if the user does not enter the value -1, i would be equal to 100. */
stat_arr(arr, i, &min, &max, &avg);
printf("Max=%.2f Min=%.2f Avg=%.2f\n", max, min, avg);
return 0;
}

void stat_arr(float arr[], int size, float *min, float *max, float *avg)
{
    int i;
    float sum;
    sum = *min = *max = arr[0];
    for(i = 1; i < size; i++)
    {
        if(arr[i] > *max)
            *max = arr[i];
        if(arr[i] < *min)
            *min = arr[i];
        sum += arr[i];
    }
    *avg = sum/size;
}
```

# C.11.34 What is the output of the following program?

```
#include <stdio.h>

int *test(int *ptr1, int *ptr2);

int main(void)
{
    int arr[] = {1, 2, 3, 4};
    *test(arr, arr+3) = 30;
    printf("%d %d %d %d\n", arr[0], arr[1], arr[2], arr[3]);
    return 0;
}

int *test(int *ptr1, int *ptr2)
{
    *(ptr1+1) = 10;
    *(ptr2-1) = 20;
```