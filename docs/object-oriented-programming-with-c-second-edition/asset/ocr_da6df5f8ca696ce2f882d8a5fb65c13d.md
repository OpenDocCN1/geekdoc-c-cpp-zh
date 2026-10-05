```
/*End of A.h*/
/*Beginning on A.cpp*/
void A::setX(const int pX)
{
    x = pX;
}
int A::getX() const
{
    return x;
}
```

```
/*Beginning of B.h*/
#include"A.h"
class B : public A //inheriting from A
{
    int y;
public:
    void setY(const int=0);
    int getY()const;
```

```
/*End of B.h*/
/*Beginning on B.cpp*/
#include"B.h"
void B::setY(const int pY)
{
    y = pY;
}
int B::getY() const
{
    return y;
}
```

```
/*Beginning of inherit.cpp*/
#include<iostream>
#include"B.h"
void main())
{
    cout<<sizeof(A)<<endl<<sizeof(B); //an object of the derived class
    B1;
    B1.setX(1); //OK: calling a base class member function
               //with respect to a derived class object
    B1.setY(3);
    cout<<B1.getX()<<endl; //OK: calling a base class
                          //member function with respect to
    cout<<B1.getY()<<endl; //a derived class object
}
/*End of inherit.cpp*/
```

# Output

4
8
1
3