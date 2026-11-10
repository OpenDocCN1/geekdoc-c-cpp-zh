# 11.8.1 input2array.c: Passing an Array as an Argument

Program 11.5 uses a function to populate an array with keyboard input. This function uses the name of the array and its size as the two arguments. After the function completes execution, the program prints the values of all array elements. The output shows that the initialization of the “array”, f_arr, inside the function has actually changed arr in main, thus confirming our assertion that the array itself is never copied inside a function.

Since arr is the same as &arr[0], both &arr[0] and &f_arr[0] represent the address of the same array element. But f_arr is not an array even if the declaration and definition suggest that it is one (f_arr[]). The input2array function, however, treats f_arr as an array and uses the other argument (SIZE or num) to populate it correctly. Thus, changing f_arr inside the function actually changes arr outside the function.

Let’s now face the truth once and for all: Both arr and f_arr are pointers. The declaration could have specified short * f_arr instead of short f_arr[], and it would have made no difference to the existing implementation of the function. (See it for yourself by making this change.) But hold

```
```c
/* input2array.c: Uses a function to fill up array with keyboard input. */
#include <stdio.h>
#define SIZE 6
void input2array(short f_arr[], short num);   /* Note the [] */

int main(void)
{
    short arr[SIZE], i;
    input2array(arr, SIZE);                   /* Array name as argument */
    for (i = 0; i < SIZE; i++)
        printf("arr[%hd] = %hd ", i, arr[i]);
    printf("\n");
    return 0;
}

void input2array(short f_arr[], short num)
{
    short i;
    printf("Key in %hd integers: ", num);
    for (i = 0; i < num; i++)
        scanf("%hd", &f_arr[i]);              /* No array named f_arr actually */
    return;
}

PROGRAM 11.5: input2array.c
Key in 6 integers: 1 5 20 100 1024 4096
arr[0] = 1 arr[1] = 5 arr[2] = 20 arr[3] = 100 arr[4] = 1024 arr[5] = 4096

PROGRAM OUTPUT: input2array.c
```
```