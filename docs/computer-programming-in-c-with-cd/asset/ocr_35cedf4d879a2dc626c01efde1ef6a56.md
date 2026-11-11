Largest element in a[3] is :87
Smallest element in a[2] is :3

Q3. Write a program to generate multiplication of two matrices.

Ans.

```
```cpp
#include<iostream.h>
#include<iomanip.h>
void main()
{
    int i, j, k, x[10][10], y[10][10], z[10][10];
    int row1, col1, row2, col2;
    cout<<"Enter row of Matrix x"<<endl;
    cin>>row1;
    cout<<"Enter col of Matrix x"<<endl;
    cin>>col1;
    cout<<"Enter row of Matrix y"<<endl;
    cin>>row2;
    cout<<"Enter col of Matrix y"<<endl;
    cin>>col2;
    if(col1 != row2)
    {
        cout<<"Multiplication of two matrix is not possible"<<endl;
    }
    else
    {
        // input elements of matrix x
        cout<<"Enter element of matrix x"<<endl;
        for(i=0;i<row1;i++)
        {
            for(j=0;j<col1;j++)
            {
                cout<<"Enter element of x["<<i<<"]["<<j<<"]:";
                cin>>x[i][j];
            }
        }

        cout<<"Enter element of matrix y"<<endl;
        //input elements of matrix y
        for(i=0;i<row2;i++)
        {
            for(j=0;j<col2;j++)
            {
                cout<<"Enter element of y["<<i<<"]["<<j<<"]:";
                cin>>y[i][j];
            }
        }
        // multiplication to x and y matrix
        for(i=0;i<row1;i++)
```
```