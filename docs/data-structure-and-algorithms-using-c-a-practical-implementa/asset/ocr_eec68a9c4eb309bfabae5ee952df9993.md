```
a=b;
b=c;
}
}
void main()
{
int n;
cout<<"Enter how many digits U want to print";
cin>>n;
fibio obj (n);
obj.generate(); }
```

# OUTPUT

Enter how many digits U want to print 8
THE FIBONACCI SERIES NUMBERS ARE
0 1 1 2 3 5 8 13

# 4.1.1.2 Destructor

A destructor is also a member function of the class which is used for the destruction of the objects which are created by constructor. That is this is used for the de-allocation purpose. The declaration of the destructor is as same as the constructor except that the destructor is declared with the tiled(~) symbol and it does not have any return type as well as it does not have any argument.

The destructors are also called automatically. The keyword “virtual” cam be used with destructor.

Ex :

```
#include<iostream.h>
#include<conio.h>
class demo
{
public:
demo()
{
cout<<"CONSTRUCTOR IS CALLED";
}
void input()
{
cout<<endl<<"HELLO";
}
~demo()
{
cout<<endl<<"DESTRUCTOR IS CALLED";
getch();
}
```