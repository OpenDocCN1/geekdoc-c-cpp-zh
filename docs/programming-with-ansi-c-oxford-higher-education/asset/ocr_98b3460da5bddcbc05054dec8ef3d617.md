# # 418 Programming with ANSI C++

```
cout << "Draw size using derived class pointer: " << DrawSize << "\n";
it displays 200 correctly.
```

> When we use a base class pointer to point to a derived class object, the default value of the base class function will be taken. Here, the function that is executed is correct, but with the default value of the base class. On the other hand, when we use a derived class pointer, the default value of the derived class function is taken.

# ## Dummy Default Arguments to the Rescue

Program 10.3 showed that default parameters cannot be used like a normal function. The solution here is to provide a local variable initialized in both such classes and then use the default argument. If default arguments are needed, they can be assigned values of such local variables, as shown in Program 10.4.

One only needs to see whether the user has supplied a value, and if not, take information from the local variables rather than the default arguments. One can easily check whether the user has supplied a value by keeping a dummy default argument. If the argument equals the dummy value, the user has not supplied the argument, and one can take the value from the local variable.

# ## PROGRAM 10.4 Using dummy default argument as a solution

```
//SolutionDefArgs.cpp
#include <iostream>
using namespace std;
class Shape
{
    int LineStyle;
    int FillColour;
public:
    virtual int draw(int size = 1)
    /* The size parameter is dummy; it is there to check whether the default argument is provided */
    {
        cout << "Shape is drawn\n";
        int ShapeSize = 100;
        /* This is to check whether the default argument is provided with the given value 100 */
        if(size == 1)
            size = ShapeSize;
        return size;
    }
};
class Circle : public Shape
{
    int Radius;
    int CentrePointX;
    int CentrePointY;
public:
    int draw(int size = 1)
    {
        cout << "Circle is drawn\n";
        int CircleSize = 200;
        if(size == 1)
            size = CircleSize;
        return size;
    }
};
```