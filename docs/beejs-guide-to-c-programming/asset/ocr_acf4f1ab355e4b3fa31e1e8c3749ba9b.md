# Chapter 30. Variable-Length Arrays (VLAs)

There's a bit more to it than. You can also let C know that the array is a specific VLA size by passing that in first and giving dimension in the parameter list:

```
int sum(int count, int v[count])
{
    // ...
}
```

Incidentally, there are a couple ways of listing a prototype for the above function; one of them involves a if you don't want to specify name value in the VLA. It just indicates that the type is a VLA as opposed to a regular pointer.

VLA prototypes:

```
void do_something(int count, int v[count]); // With names
void do_something(int, int v[*]); // Without names
```

Again, that * only works with the prototype—in the function itself, you'll have to put the explicit size. Now—let's get multidimensional! This is where fun begins.

# 30.5 Passing Multi-Dimensional VLAs to Functions

Same as you did with the second form of one-dimensional VLAs, above, but this time we're passing in two dimensions and using those.

In the following example, we build a multiplication table matrix of a variable width and height, and pass it to a function to print out.

```
#include <stdio.h>

void print_matrix(int h, int w, int m[h][w]) {
    for (int row = 0; row < h; row++) {
        for (int col = 0; col < w; col++) {
            printf("%2d ", m[row][col]);
        }
        printf("\n");
    }
}

int main(void)
{
    int rows = 4;
    int cols = 7;

    int matrix[rows][cols];

    for (int row = 0; row < rows; row++) {
        for (int col = 0; col < cols; col++) {
            matrix[row][col] = row * col;
        }
    }

    print_matrix(rows, cols, matrix);
}

```