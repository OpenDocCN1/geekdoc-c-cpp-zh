```
if (b == 0)
    throw "Division by zero not allowed";
    res = a / b;
    cout << res;
}
```

+   a. 0
+   b. Bad operator
+   c. 10
+   d. 15

# 36. What is the output of the following C++ code?

```
#include <stdexcept>
#include <limits>
#include <iostream>
using namespace std;
void MyFunc(char c)
{
    if (c < numeric_limits<char>::max())
        return invalid_argument;
}
int main()
{
    try
    {
        MyFunc(256);
    }
    catch(invalid_argument& e)
    {
        cerr << e.what() << endl;
        return -1;
    }
    return 0;
}
```

+   a. 256
+   b. Invalid argument
+   c. Error
+   d. 246