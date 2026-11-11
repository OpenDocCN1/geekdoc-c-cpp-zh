```
```cpp
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
    // input elements of matrix y
for(i=0;i<row2;i++)
{
    for(j=0;j<col2;j++)
    {
        cout<<"Enter element of y["<<i<<"]["<<j<<"]:";
        cin>>y[i][j];
    }
}
    // addition to x and y matrix
for(i=0;i<row1;i++)
{
    for(j=0;j<col1;j++)
    {
        z[i][j] = x[i][j] + y[i][j];
    }
}
    //Printing elements of matrix x
cout<<"Elements of matrix x are :"<<endl;
for(i=0;i<row1;i++)
{
    for(j=0;j<col1;j++)
    {
        cout<<x[i][j]<<setw(5);
    }
    cout<<setw(0);
    cout<<endl;
}
    // Printing elements of matrix y
cout<<"Elements of matrix y are :"<<endl;
for(i=0;i<row2;i++)
{
    for(j=0;j<col2;j++)
    {
        cout<<y[i][j]<<setw(5);
    }
    cout<<setw(0);
    cout<<endl;
}
```
```