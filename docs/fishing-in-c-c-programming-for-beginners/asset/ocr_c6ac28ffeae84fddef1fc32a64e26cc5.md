```
class square
{
    int side;
    public:
    void set_side (int s);
    friend class rectangle;
};
class rectangle
{
    int length, breadth;
    public:
    int area ();
    void set_square(square a);
};
```

```
int rectangle::area()
{
    return length * breadth;
}
void square::set_side(int s)
{
    side=s;
}
void rectangle::set_square (square a)
{
    length = breadth = a.side;
}
```

```
int main ()
{
    square sqr;
    rectangle rect;
    sqr.set_side(5);
    rect.set_square(sqr);
    cout<<rect.area();
    return 0;
}
```

Output
25

Now, let us see how to declare a simple class. A class can be declared like functions but without the braces (). A function should be defined before its use, if not then we have to declare a function before its use. Similarly a class should be defined before its use, if not then we have to declare the class before its use. For example consider the following program:

```
#include <iostream>
```

```
using namespace std;
```