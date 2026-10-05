```
for(int j = 0; j < cols; j++)
cout << arr[i*cols+j] << ' ' ; /* Complex syntax and
prone to errors. As we already know, it is equivalent to the expression that
the compiler produces when we write arr[i][j]. */
```

As with one-dimensional arrays, to pass a two-dimensional array as an argument, we write only its name, without brackets. If we want to pass a row (e.g., i) we pass the pointer to that row (arr[i]), we do when passing a one-dimensional array. For example, the following program displays the elements of the first row:

```
#include <iostream> // Example 11.26
```

```
const int ROWS = 2;
const int COLS = 3;
```

```
void show_row(const int a[]);
```

```
int main()\{
    int arr[ROWS][COLS] = {{1, 2, 3}, {4, 5, 6}};

    show_row(arr[0]);
    return 0;
}
```

```
void show_row(const int a[])
{
    for(int i = 0; i < COLS; i++)
        std::cout << a[i] << ' ';
}
```

# # EXERCISES

C.11.23 Write a function that takes as parameter a 3x4 two-dimensional array and returns one array where each element is equal to the sum of the elements of the respective row of the two-dimensional array and another array where each element is equal to the sum of the elements of the respective column of the two-dimensional array. Write a program that reads 12 integers into a 3x4 two-dimensional array, and uses the function to display the elements in each row and the sum of the elements in each column as well.

```
#include <iostream>
using std::cout;
using std::cin;
```

```
const int ROWS = 3;
const int COLS = 4;
```

```
void find_sums(const int arr1[][COLS], int arr2[], int arr3[]);
```

```
int main()\{
    int i, j, arr1[ROWS][COLS], arr2[ROWS], arr3[COLS];
```