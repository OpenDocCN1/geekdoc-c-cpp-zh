# Passing Two-Dimensional Array to a Function

We can pass a two-dimensional array to a function in multiple ways. However, in this chapter, let’s discuss the following three ways of passing a two-dimensional array to a function:

```
my_function(int my_array[4][6]) { ---- }

my_function(int my_array[][6]) { ---- }

my_function(int (*my_array)[6]) { ---- }
```

The three preceding ways might look different but eventually all of them pass the base address of a two-dimensional array to a function. Note that while passing a two-dimensional array to a function, we should always include the column number. In addition, pointer to an array of rows is passed to a function where each row again is an array. Listing 4.9 shows how a two-dimensional array is passed to a function:

Listing 4.9: Passing Two-Dimensional Array to a Function

```
#include <stdio.h>
void display_method_a(int *arr,int row, int col);
void display_method_b(int (*arr)[3],int row, int col);
void display_method_c(int arr[3][3],int row, int col);

int main()
{
    int i,j;
    int arr[3][3] = {
        {1,100,1000},
        {2,200,2000},
        {3,300,3000}
    };

    display_method_a(arr,3,3);
    display_method_b(arr,3,3);
    display_method_c(arr,3,3);
    getch();
}

void display_method_a(int *arr,int row, int col)
{
    int i,j;

    for(i=0;i < row; i++)
    {
        for(j=0; j < col; j++)
        {
            printf("%d ", *(arr + ((i*col) + j)));
        }
        printf("\n");
    }
}

void display_method_b(int (*arr)[3],int row, int col)
{
    int i,j;
    int *ptr;
    for(i=0;i < row; i++)
```