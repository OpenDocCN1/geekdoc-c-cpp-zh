# Chapter 7 391

Declaring and Processing Two-Dimensional Arrays

```
Display of val array using a nested for
8 16 9 52
3 15 27 6
14 25 2 10
```

The first display of the val array produced by Program 7.4 is constructed by designating each array element. The second display of array elements values, which is identical to the first, is produced by using nested for loops. Nested are especially useful when dealing with two-dimensional arrays because they allow the program to designate and cycle through element easily. In Program 7.4, the variable i controls the outer loop, and the variable j controls the inner loop. Each pass through the outer loop corresponds to a single row, with the inner loop supplying the column elements. After a complete row is printed, a new line is started for the next row. The result is a display of the array in row-by-row fashion.

After two-dimensional elements are assigned, array processing can begin. Typically, loops are used to process two-dimensional arrays because, as noted previously, they allow the program to designate and cycle through each array element easily. For example, the nested for loop in Program 7.5 is used to multiply each element in the val by the scalar number 10 and display the resulting value.

# Program 7.5

```
#include <iostream>
#include <iomanip>
using namespace std;
int main()
{
    const int NUMROWS = 3;
    const int NUMCOLS = 4;
    int i, j;
    int val[NUMROWS][NUMCOLS] = {8,16,9,52,3,15,27,6,14,25,2,10};

    // multiply each element by 10 and display it
    cout << "\nDisplay of multiplied elements:\n";

    for (i = 0; i < NUMROWS; i++)
    {
        cout << endl;
        for (j = 0; j < NUMCOLS; j++)
        {
            val[i][j] = val[i][j] * 10;
            cout << setw(5) << val[i][j];
        } // end of inner loop
    } // end of outer loop
    return 0;
}
```

![](bbox=[0.113, 0.433, 0.185, 0.473])