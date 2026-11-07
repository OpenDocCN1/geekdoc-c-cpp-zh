```
```cpp
num1 = 10;

num2 = 20;

cout << "Line 3: In main: num1 = " << num1
     << ", num2 = " << num2 << endl;                 //Line 3
funOne(num1);                                           //Line 4
cout << "Line 5: In main after funOne: num1 = "
     << num1 << ", num2 = " << num2 << endl;          //Line 5

return 0;                                               //Line 6
}

void funOne(int& a)
{
    int x = 12;
    int z;

    z = a + x;                                           //Line 7

    cout << "Line 8: In funOne: a = " << a
         << ", x = " << x
         << ", and z = " << z << endl;                 //Line 8

    x = x + 5;                                           //Line 9

    cout << "Line 10: In funOne: a = " << a
         << ", x = " << x
         << ", and z = " << z << endl;                 //Line 10

    a = a + 8;                                           //Line 11

    cout << "Line 12: In funOne: a = " << a
         << ", x = " << x
         << ", and z = " << z << endl;                 //Line 12
}
```
```

35. What is the output of the following program? (11)

```
```cpp
#include <iostream>
using namespace std;

void tryMe(int& v);

int main()
{
    int x = 8;

    for (int count = 1; count < 5; count++)
        tryMe(x);

    return 0;
}
```
```