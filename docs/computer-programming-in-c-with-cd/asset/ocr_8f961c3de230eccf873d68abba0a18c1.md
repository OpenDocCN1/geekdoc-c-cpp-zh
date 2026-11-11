```
```cpp
for( int k=0; k< m-1;k++)
for(int i=k+1;i<m;i++)
{
float fact= mat[i][k]/ mat[k][k];
for(int j=0;j<n;j++)
mat[i][j]=mat[i][j]- mat[k][j]* fact;
}
}

void main()
{
matrix obj1,obj2,obj3;
obj1.input();
obj2.input();
obj1.display();
obj2.display();
obj3.add(obj1,obj2);
cout<<"\n Matrix After Addition Is: ";
obj3.display();
obj3.mul(obj1,obj2);
cout<<"\n Matrix After Multiplication Is: ";
obj3.display();
getch();
}
```
```

Q26: Expand the class member functions to satisfy the functionality described along side the function declaration (Mumbai University, December 2007)

Ans:

```
```cpp
#include<iostream.h>
class Dmanip
{
private:
int N,A[100];
public:
Dmanip(); // Default constructor
void Display();
void InputArray ( );// input function to read array A
void InputArray(int x[],int x[100]);// over loaded input function
void Sort( ); // sorting data stored in Array A
void Search(int data);
void Insert(int data);
void Delete(int data);
```
```