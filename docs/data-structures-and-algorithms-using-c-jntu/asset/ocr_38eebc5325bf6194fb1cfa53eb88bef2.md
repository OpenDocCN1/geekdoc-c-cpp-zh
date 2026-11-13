```
/*Base Class Access Control in inheritance when Access Specifier is
PUBLIC*/
class Base
{
int a; //Private Member Data Variable, Not Accessible by
//the derived Class
void setA(int x) //Private Member Function, Not Accessible by
//the derived Class
{
a=x;
}
void showA() //Private Member Function,Not Accessible by
//the derived Class
{
cout<<"\nA="<<a;
}
public:
int b;
void setB(int y)
{
b=y;
}
void showB()
{
cout<<"\nB="<<b;
}
};
class Derived:public Base{
int c;
public:
void setC(int z)
{
c=z;
}
void showC()
{
cout<<"\nC="<<c;
}
};
void main()
{
Base obj1;
Derived obj2;
clrscr();
//Calling Base Class methods
cout<<" \nCalling Base Class methods";
//obj1.a=1; /*Not Accessible Because of private member of
* Base Class*/
```