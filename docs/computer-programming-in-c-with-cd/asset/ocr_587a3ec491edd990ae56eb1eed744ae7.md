```
```cpp
s.display() ; //call to overridden display function of derived class
getch() ;

}
```
```

Q45: Develop a friend function to carryout multiplication between two conformable matrices stored in a single dimensional array variables as a private member of class ‘Onedim’. The result of multiplication needs to be stored in a two dimensional array variable as a private member of class ‘Twodim’. Incorporate suitable member functions both in class Onedim and class Twodim for reading this matrix and display of matrix.

One of the single dimensional array variables can hold matrix in column wise and other row wise. Also develop main program to reference the friend function.

Ans:

```
```cpp
#include<iostream.h>
#include<conio.h>

class Beta;
class Alpha
{
    int M,L,N;
    int A[100];
    int B[100];
public :

    void InputArray()
    {
        cin>>M>>L>>N;

        for(int i=1;i<=M*L;i++)
        cin>>A[i];
        cout<<endl;
        for( i=1;i<=L*N;i++)
        cin>>B[i];
    }
    friend void matmult(Alpha &obja,Beta &Objb);
};

class Beta
{
    int C[10][10];
    int M,N;
```
```