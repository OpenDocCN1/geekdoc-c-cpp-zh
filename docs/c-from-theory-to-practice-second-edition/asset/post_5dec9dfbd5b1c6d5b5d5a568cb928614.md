
```c
int main(void)
{
    int i, times, pos;
    double num, arr[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        printf("Enter number: ");
        scanf("%lf", &num);
        if(num == -1)
            break;
        arr[i] = num;
    }
    printf("Enter number to search: ");
    scanf("%lf", &num);

    pos = linear_search(arr, i, num, &times); /* The variable i
indicates the number of the array's elements. */
    if(pos == -1)
        printf("%f isn't found\n", num);
    else
        printf("%f appears %d times (first pos = %d)\n", num, times,
pos);
    return 0;
}

int linear_search(double arr[], int size, double num, int *t)
{
    int i, pos;

    pos = -1;
    *t = 0;
    for(i = 0; i < size; i++)
    {
        if(arr[i] == num)
        {
            (*t)++;
            if(pos == -1) /* Store the position of the first
occurrence. */
                pos = i;
        }
    }
    return pos;
}
```

### C.12.2 Write a function that takes as parameter an integer array and returns the maximum number of the same occurrences. For example, if the array is {1, 10, -3, 5, -3, 8}, the function should return 2 because -3 appears the most times, that is, 2. Write a program that reads 10 integers, stores them in an array, and uses the function to display the maximum number of the same occurrences.

```c
#include <stdio.h>

#define SIZE 10

int num_occurs(int arr[]);

int main(void)
{
    int i, arr[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        printf("Enter number: ");
        scanf("%d", &arr[i]);
    }
    printf("\nMax occurrences is %d\n", num_occurs(arr));
    return 0;
}

int num_occurs(int arr[])
{
    int i, j, k, max_times;

    max_times = 1;
    for(i = 0; i < SIZE; i++)
    {
        k = 1; /* Each number appears once at least. */
        for(j = i+1; j < SIZE; j++) /* Compare arr[i] with the rest elements. */
        {
            if(arr[i] == arr[j])
                k++;
        }
        if(k > max_times)
            max_times = k;
    }
    return max_times;
}
```

## Binary Search Algorithm

The binary search algorithm is used to search for a value in a sorted array (either in ascending or descending order). To understand how the algorithm works, suppose that we are searching for a value in an array sorted in ascending order:

Step I: We use the variables start and end to indicate the start and the end of the part of the array, in which we are searching for the value. We use the variable middle to calculate the middle position of that part: middle = (start+end)/2. For example, if we have a sorted array of 100 integers, start should be initialized to 0, end to 99, so middle becomes 49.

Step 2: We compare the value we are searching for with the middle element:
- a. If they are equal, the searched value is found and the algorithm terminates.
- b. If it is greater, the search continues in the part starting from the middle position and up to the end. The algorithm goes back to Step 1, and start becomes start = middle+1.
- c. If it is less, the search continues in the part starting from the start position and up to the middle. The algorithm goes back to Step 1, and end becomes end = middle-1.

In short, the binary search algorithm divides the array into two parts. Then, the searched value is compared with the middle element and the search continues in the proper part. The algorithm terminates if either the searched value is found or start becomes greater than end. In the following program, the binary_search() function implements the binary search algorithm.

## Exercises

### C.12.3 Write a function that searches for a number in an array of integers. If the number is found, the function should return its position, otherwise -1. Write a program that initializes an array of integers with values sorted in ascending order. The program should read an integer and use the function to display its position in the array.

```c
#include <stdio.h>

int binary_search(int arr[], int size, int num);

int main(void)
{
    int num, pos, arr[] = {10, 20, 30, 40, 50, 60, 70};

    printf("Enter number to search: ");
    scanf("%d", &num);

    pos = binary_search(arr, 7, num);
    if(pos == -1)
        printf("%d isn't found\n", num);
    else
        printf("%d is found in position %d\n", num, pos);
    return 0;
}

int binary_search(int arr[], int size, int num)
{
    int start, end, middle;

    start = 0;
    end = size-1;
    while(start <= end)
    {
        middle = (start+end)/2;
        if(num < arr[middle])
            end = middle-1;
        else if(num > arr[middle])
            start = middle+1;
        else
            return middle;
    }
    return -1; /* If the execution reaches this point it means that the number was not found. */
}
```

Comments: To see how the algorithm works, suppose that the user enters the number 45.

First iteration. The initial value of start is 0 and end is 6. middle becomes (start+end)/2 = 6/2 = 3. Since arr[middle] is 40, less than 45, the next statement to be executed is start = middle+1 = 3+1 = 4.

Second iteration. middle becomes (start+end)/2 = (4+6)/2 = 5. Since arr[middle] is 60, greater than 45, the next statement is end = middle-1 = 4.

Third iteration. middle becomes (start+end)/2 = (4+4)/2 = 4. Since arr[middle] is 50, greater than 45, the next statement is end = middle-1 = 3. Since start is greater than end, the loop terminates and the function returns -1.

### C.12.4 Write a program that reads an integer within [0, 1000] and uses the binary search algorithm to "guess" that number. The program should make questions to determine if the number we are searching for is less or greater than the middle of the examined interval. The answers must be given in the form of 0 (no) or 1 (yes). The program should display in how many tries the number was found.

```c
#include <stdio.h>
int main(void)
{
    int x, ans, low, high, middle, times;

    do
    {
        printf("Enter number in [0, 1000]: ");
        scanf("%d", &x);
    } while(x < 0 || x > 1000);

    times = 1;
    low = 0;
    high = 1000;
    middle = (high+low)/2;
    while(high >= low)
    {
        printf("Is %d the hidden number (0 = No, 1 = Yes) ? ",
        middle);
        scanf("%d", &ans);

        if(ans == 1)
        {
            printf("Num = %d is found in %d tries\n", x, times);
            return 0;
        }
        times++;
        printf("Is the hidden number < %d (0 = No, 1 = Yes) ? ",
        middle);
        scanf("%d", &ans);
        if(ans == 1)
        {
            high = middle-1;
            middle = (high+low)/2;
        }
        else
        {
            low = middle+1;
            middle = (high+low)/2;
        }
    }
    printf("Num = %d isn't found. You probably gave a wrong answer\n", x);
    return 0;
}
```

## Sorting Arrays

There are several algorithms to sort an array. We are going to describe some of the most popular, the selection sort, the insertion sort, the bubble sort, and the quick sort algorithms.

## Selection Sort Algorithm

To describe the algorithm, we'll show you how to sort an array in ascending order. At first, we find the element with the smallest value and we swap it with the first element of the array. Therefore, the smallest value is stored in the first position.

Then, we find the smallest value among the remaining elements, except the first one. Like before, we swap that element with the second element of the array. Therefore, the second smallest value is stored in the second position. This procedure is repeated with the rest of the elements and the algorithm terminates once the last two elements are compared.

To sort the array in descending order, we find the largest value instead of the smallest. In the following program, the sel_sort() function implements the selection sort algorithm to sort an array in ascending order.

## Exercises

### C.12.5 Write a function that takes as parameters an array of doubles and uses the selection sort algorithm to sort it in ascending order. Write a program that reads the grades of 10 students, stores them in an array, and uses the function to sort it.

```c
#include <stdio.h>

#define SIZE 10

void sel_sort(double arr[]);

int main(void)
{
    int i;
    double grd[SIZE];
    for(i = 0; i < SIZE; i++)
    {
        printf("Enter grade of stud_%d: ", i+1);
        scanf("%lf", &grd[i]);
    }
    sel_sort(grd);
    printf("\n**** Sorted array ****\n");
    for(i = 0; i < SIZE; i++)
        printf("%.2f\n", grd[i]);
    return 0;
}

void sel_sort(double arr[])
{
    int i, j;
    double tmp;
    for(i = 0; i < SIZE-1; i++)
    {
        for(j = i+1; j < SIZE; j++)
        {
            if(arr[i] > arr[j])
            {
                /* Swap values. */
                tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;
            }
        }
    }
}
```

Comments: In each iteration of the inner loop, arr[i] is compared with the elements from i+1 up to SIZE-1. If an element is less than arr[i], their values are swapped. Therefore,
