Use object as function parameter in addition of matrices. Write suitable main program to test the member functions.

Ans:

```
#include<iostream.h>
#include<conio.h>

class matrix
{
int n,m;
int mat[10][10];
public:
void input();
void display();
void add(matrix obj,matrix obj1);
void mul(matrix obj,matrix obj1);
void Elimination();
void Transpose();

};
void matrix::input()
{
cout<<"\n Enter The Number of Rows: ";
cin>>m;
cout<<"\n Enter The Number of Columns: ";
cin>>n;
for(int i=0;i<m;i++)
for(int j=0;j<n;j++)
cin>>mat[i][j];
}
void matrix::display()
{
for(int i=0;i<m;i++)
{
cout<<endl;
for(int j=0;j<n;j++)
cout<<"\t"<<mat[i][j];
}
}

void matrix::Transpose()
{
```