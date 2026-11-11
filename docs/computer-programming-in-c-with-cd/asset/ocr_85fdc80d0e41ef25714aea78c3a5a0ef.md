array by using the nested for loop,(you can find the Array3.cpp file on the CD in the code/chapter3 folder):

# ▶ Listing 4: Creating Two-dimensional Array

```
```cpp
#include <iostream.h>
#include <string.h>

int main()
{
    int matrix[3][4];
    int i,j;
    for(i=0; i<3; i++)
    {
        for(j=0; j<4; j++)
        {
            cout<<"Enter the element of matrix["<<i<<"]["<<j<<"] :";
            cin>>matrix[i][j];
        }
    }

    cout<<endl;
    cout<<"The element of matrix are: "<<endl;
    for(i=0; i<3; i++)
    {
        for(j=0; j<4; j++)
        {
            cout<<matrix[i][j]<<"  ";
        }
        cout<<endl;
    }

    return 0;
}
```
```

# Output:

```
```text
Enter the element of matrix[0][0] :3
Enter the element of matrix[0][1] :6
Enter the element of matrix[0][2] :1
Enter the element of matrix[0][3] :5
Enter the element of matrix[1][0] :2
Enter the element of matrix[1][1] :7
Enter the element of matrix[1][2] :4
Enter the element of matrix[1][3] :2
Enter the element of matrix[2][0] :4
Enter the element of matrix[2][1] :3
Enter the element of matrix[2][2] :8
Enter the element of matrix[2][3] :5
The element of matrix are:
3 6 1 5
```
```