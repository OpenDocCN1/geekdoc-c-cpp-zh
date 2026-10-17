C++

![](bbox=[0.331, 0.085, 0.662, 0.45])

Here, key point of the *while* loop is that the loop might not ever run. When the condition is tested and the result is false, the loop body will be skipped and the first statement after the while loop will be executed.

# Example

```
```cpp
#include <iostream>

using namespace std;

int main ()
{
    // Local variable declaration:
    int a = 10;

    // while loop execution
    while( a < 20 )
    {
        cout << "value of a: " << a << endl;
        a++;
    }
}
```
```