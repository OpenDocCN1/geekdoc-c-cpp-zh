```
```cpp
void ConstFunction::setVal()
{

x=10;
y=x*x;
}
void ConstFunction::display() const
{
cout<<"x = "<<x<<endl;
cout<<"y = "<<y<<endl;
}

void main()
{
ConstFunction cf;
cf.setVal();
cf.display();
}
```
```

# Output:

```
```text
x = 10
y = 100
```
```

In Listing 3, x and y are variables of int type that are assigned with values in the setVal() function. The display() is a const function, which is used to display the values of x and y variables. If you try to assign values to the variables in the display() function, you get compilation error as a const function cannot modify the values of data members of a class.

# Nesting of Member Functions

In C++, it is not necessary that a function can be invoked only by an object of a class. The functions that can be invoked by other functions are called nested functions.

Listing 4 shows how to call a function through another function call (you can find this example in the NumberAddition.cpp file on the CD in the code\chapter6 folder):

# Listing 4: Calling a Function through another Function

```
```cpp
#include<iostream.h>

class NumberAddition
{
    int a, b;
    int add();
    public:
    void numAccept();
    void display();
```
```