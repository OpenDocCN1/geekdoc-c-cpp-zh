# 13.8  Function Object: Overloading Function Call Operator ()

An object that acts as a function is called as function object or a functor. We can use this object as if it is an ordinary function. To create such objects, we must overload the function call operator ( ), by including operator ( ) as a member function in the class.

Figure 13.17 shows the syntax to overload the operator ( ). The function can be defined to accept any number of arguments depending on the requirement of the programmer.

![](bbox=[0.185, 0.251, 0.808, 0.419])

**Figure 13.17:** Syntax to overload function call operator

As an example, let us consider class Rectangle, which has a single member function that overloads operator ( ). The function calculates and returns the area of the rectangle based on values of length and breadth passed to it.

```
```cpp
#include<iostream.h>
class Rectangle
{
public:
    float operator()(float length,float breadth)
    {
        return length*breadth;
    }
};
void main()
{
Rectangle area;
float x = area(10.0 , 3.0);
float y = area(15.5 , 5.0);
float z = area(3.5 , 6.45);
cout<<"Area of rectangle with length=10.0 and breadth=3.0
     is:"<<x<<endl;
cout<<"Area of rectangle with length=15.5 and breadth=5.0
     is:"<<y<<endl;
cout<<"Area of rectangle with length=3.5 and breadth=6.45
     is:"<<z<<endl;
}
```
```