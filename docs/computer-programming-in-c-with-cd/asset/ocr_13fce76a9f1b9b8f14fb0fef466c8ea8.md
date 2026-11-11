```
```cpp
object3 = object1 + object2;  /* addition of two objects, calls
operator+() */
object3.getxy(x, y);
cout << "(Object1+object2) x: " << x << ", y: " << y << endl;

object3 = object1 - object2;  /* difference of two objects, calls
operator-
() */
object3.getxy(x, y);
cout << "(Object1-object2) x: " << x << ", y: " << y << endl;
object3 = object1;  /* assign an object with another object,
calls
operator=() */
object3.getxy(x, y);
cout << "(Object3=object1) x: " << x << ", y: " << y << endl;
return 0;
}
```
```

```
```text
Output:

(Object1+object2) x: 25, Y: 33
(Object1-object2) x: 15, Y: 27
(Object3=object1) x: 20, Y: 30
```
```

Q12. Write a program to overload the parenthesis () operator.

Ans:

```
```cpp
#include <iostream.h>

class OverloadedParenthesis {
    int x, y, z;
public:
    OverloadedParenthesis(int i, int j, int k) {
        x = i;
        y = j;
        z = k;
    }
    OverloadedParenthesis()
    {
        x=y=z=0;
    }
    OverloadedParenthesis operator()(int a, int b, int c);
    void display() ;
};

OverloadedParenthesis OverloadedParenthesis::operator()(int a, int
    b, int c)
{
    OverloadedParenthesis temp;
```
```