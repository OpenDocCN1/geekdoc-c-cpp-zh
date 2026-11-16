```
class area
{
int *x, *y;
public:
area (int,int);
~area();
int calculate_area (void);
};
int main()
{
    class area parallelogram(4,2);
    cout<<"Area of parallelogram is "<<parallelogram.calculate_area();
    return 0;
}
area::area(int a,int b)
{
x=new int;
y=new int;
*x=a;
*y=b;
}
area::~area()
{
delete x;
delete y;
cout<<"\nPointers deleted";
}
int area::calculate_area()
{
return *x**y;
}
Output
Area of parallelogram is 8
Pointers deleted
```

# Defining the methods inside the class

A method can be defined inside the class too. It is very useful when the method is too small. The code snippet used to define the methods inside the class is as follows:

```
class class_name
{
    //statements
    return_type func_name(arg1,arg2,...)
```