```
}
return 0;
}
```

# Output:

Enter the element to search:
55
55 found at index 6 %

# 3.3 Multi-Dimensional Array

We learned about 1D arrays and their operations earlier, so let us move on to working with 2D and 3D arrays. These kinds of arrays have rows and columns, and you can express them using the following statements:

2D array: datatype array_name[rows][column];

3D array: int three_d[array_no][rows][columns];

# Code: An Example Showing 2D and 3D Arrays

```
#include<iostream>
using namespace std;

int main()
{
    int array[3] = {{5,1,4}, {2,3,7}};
    cout<<"\n2D Array:\n";
    for (int i = 0; i < 2; ++i) {
        for (int j = 0; j < 3; ++j) {
            cout << array[i][j]<<" ";
        }
        cout<<"\n";
    }

    int x[3][3] = { { { 7, 1,5 }, { 26, 3,88 }, { 45, 5,78 } },
        { { 66, 77,33}, { 84, 9,32 }, { 10, 11,12 } } };
    cout<<"\n3D Array:\n";
    for (int m = 0; m < 2; ++m) {
        for (int n = 0; n < 3; ++n) {
            for (int q = 0; q < 3; ++q) {
                cout<< x[m][n][q]<<" ";
            }
        }
    }
```