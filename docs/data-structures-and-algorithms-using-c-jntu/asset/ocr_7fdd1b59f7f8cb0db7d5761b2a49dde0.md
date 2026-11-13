In Program 2.5 a,b,c are the objects of vector class. Each object will have the copy of variables x,y.z. Addition of objects a and b means adding member variables of a and member variables of b and stored in object c. In Program 2.5, each variable is accessed individually, that is x of x and x of b are added and stored in x of c, similarly for other variables. We cannot directly perform as c=a+b; this can be overcome by using operator overloading.

The general form of operator overloading is as follows:

```
Return-type class-name::operator<symbol of the operator>(arguments)
{
    //Redefinition of the operator
}
```

# 2.3.1 OVERLOADING THE PLUS (+) OPERATOR

# Program 2.6

```
/*Program to overload+operator*/
#include<iostream.h>
#include<conio.h>
class vector
{
    int x,y,z;
    public:
    vector(){}
    vector(int a,int b,int c)
    {
    x=a;
    y=b;
    z=c;
    }
    void show()
    {
    cout<<x<<"i"<<y<<"j"<<z<<"k";
    }
    vector operator+(vector v)
    {
    vector temp;
    temp.x=x+v.x;
    temp.y=y+v.y;
    temp.z=z+v.z;
    return temp;
    }
};
void main()
{
    vector a(10,20,30),b(1,2,3),c;
    clrscr();
    cout<<"\nVector A:\n";
```