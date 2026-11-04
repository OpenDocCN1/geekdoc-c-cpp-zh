Not only did you answer yes, but did you justify your answer? We tricked you once again... watch out for the traps coming next. Don't be angry, listen to Don't Look Back in Anger from Oasis and check the program again.

The first printf() outputs the address of the a variable. test() outputs the address of the arr variable. Are they the same? Of course not; they reside in different memory locations. However, the value of arr is equal to a; that is, if we remove &, the output values would be the same.

# Exercises

C.11.15 Write a function that takes as parameters an array containing the students' grades in a test and two grades (e.g. a and b) and returns the average of the grades within [a, b]. Write a program that reads the grades of 50 students and the two grades a and b and uses the function to display the average. The program should force the user to enter a value for a less than or equal to b.

```
#include <stdio.h>

#define SIZE 50

float avg_arr(float arr[], float min, float max);

int main(void)
{
    int i;
    float a, b, k, arr[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        printf("Enter grade: ");
        scanf("%f", &arr[i]);
    }
    do
    {
        printf("Enter min and max grades: ");
        scanf("%f%f", &a, &b);
    } while(a > b);

    k = avg_arr(arr, a, b);
    if(k == -1)
        printf("None grade in [%f, %f]\n", a, b);
    else
        printf("Avg = %.2f\n", k);
    return 0;
}

float avg_arr(float arr[], float min, float max)
{
    int i, cnt = 0;
```