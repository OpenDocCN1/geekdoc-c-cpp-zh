```
Output:

Enter row of Matrix x
2
Enter col of Matrix x
2
Enter row of Matrix y
2
Enter col of Matrix y
2
Enter element of matrix x
Enter element of x[0][0]:1
Enter element of x[0][1]:2
Enter element of x[1][0]:3
Enter element of x[1][1]:4
Enter element of matrix y
Enter element of y[0][0]:1
Enter element of y[0][1]:2
Enter element of y[1][0]:3
Enter element of y[1][1]:4
Elements of matrix x are :
1     2
3     4
Elements of matrix y are :
1     2
3     4
Multiplication of matrix x and matrix y are :
7     10
15    22
```

Q4. Write a program to find addition of two matrices.
Ans.

```
#include<iostream.h>
#include<omanip.h>
void main()
{
    int i, j, x[10][10], y[10][10], z[10][10];
    int row1, col1, row2, col2;
    cout<<"Enter row of Matrix x"<<endl;
    cin>>row1;
    cout<<"Enter col of Matrix x"<<endl;
    cin>>col1;
    cout<<"Enter row of Matrix y"<<endl;
    cin>>row2;
    cout<<"Enter col of Matrix y"<<endl;
    cin>>col2;
    if(row1 == row2 && col1 == col2)
    {
        // input elements of matrix x
```