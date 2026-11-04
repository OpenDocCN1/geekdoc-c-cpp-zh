U.8.11 Use p1, p2, and temp and complete the following program to reverse the elements of arr. Then, use p1 to display the array elements. For example, the new content of arr should be: 2.5  9.4  -3.8  -4.1  1.3

```
```c
#include <stdio.h>
int main(void)
{
    double arr[] = {1.3, -4.1, -3.8, 9.4, 2.5}, temp, *p1 = arr, *p2 = arr+4;

    ...

}
```
```

U.8.12 Write a program that reads 100 integers and stores them in an array. Then, the program should replace the duplicated values with -99. Use pointer arithmetic to process the array. For example, if the array were {5, 5, 5, 5, 5} the program should make it {5, -99, -99, -99, -99} and if it were {-2, 3, -2, 50, 3} it should make it {-2, 3, -99, 50, -99}.

U.8.13 Use the ptr pointer and complete the following program to read and store integers into arr, with the restriction to store an input number only if it is less than the last stored number. The value -1 should not be stored in the array. If the user enters 0 or if there is no other free place, the insertion of numbers should terminate and the program should display how many numbers were stored in the array. The program should prompt the user to input the numbers, as follows:

```
```
Enter number_1:
Enter number_2:
...
```
```

```
```c
int main(void)
{
    int *ptr, arr[100];
    ...
}
```
```

U.8.14 Use an iterative loop to complete the following program and display the elements of the array in reverse order. It is not allowed to use digits (e.g., to write arr[0], p[1] or p+2).

```
```c
int main(void)
{
    int *p, arr[] = {10, 20, 30, 40};
    ...
}
```
```

U.8.15 Use arr and complete the following program to read three integers and display the sum of the even numbers.

```
```c
int main(void)
{
    int *arr[3], i, j, k, m, sum;
    ...
}
```
```