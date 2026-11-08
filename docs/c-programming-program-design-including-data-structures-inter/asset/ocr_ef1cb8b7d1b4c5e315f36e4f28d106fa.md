28. What is the output of the following program?

```
```cpp
#include <iostream>
using namespace std;

int x;

void summer(int&, int);
void fall(int, int&);

int main()
{
    int intNum1 = 2;
    int intNum2 = 5;
    x = 6;

    summer(intNum1, intNum2);
    cout << intNum1 << " " << intNum2 << " " << x << endl;

    fall(intNum1, intNum2);
    cout << intNum1 << " " << intNum2 << " " << x << endl;
    return 0;
}

void summer(int& a, int b)
{
    int intNum1;
    intNum1 = b + 12;
    a = 2 * b + 5;
    b = intNum1 + 4;
}

void fall(int u, int& v)
{
    int intNum2;
    intNum2 = x;
    v == intNum2 * 4;
    x = u - v;
}
```
```

29. In the following program, number the marked statements to show the order in which they will execute (the logical order of execution). Also, what is the output if the input is 10?

```
```cpp
#include <iostream>

using namespace std;

int secret(int, int);

void func(int x, int& y);
```
```