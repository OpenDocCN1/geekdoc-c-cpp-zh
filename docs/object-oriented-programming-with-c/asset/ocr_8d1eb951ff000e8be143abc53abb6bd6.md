```
```cpp
switch(i)
{
default:
case 4:
case 5:

break;
case 1:
continue;

case 2:
case 3:
break;

}
i--;
}
}
```
```

# **3.4** Identify the error in the following program.

```
```cpp
#include <iostream.h>
#define pi 3.14

int squareArea(int &);
int circleArea(int &);

void main()
{
        int a=10;
        cout << squareArea(a) << " ";
        cout << circleArea(a) << " ";
        cout << a << endl;
}
int squareArea(int &a)
{
        return a *= a;
}
```
```