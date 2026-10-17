```
```cpp
Test *ptrvar = NULL;
try
{
    cout << typeid(*ptrvar).name() << endl;
}
catch (bad_typeid)
{
    cout << "The object is null" << endl;
}
return 0;
}
```
```

+   a. No exception arises
+   b. The object is null
+   c. Error
+   d. The object is

42. What is the correct output of the given code?

```
```cpp
#include <iostream>
using namespace std;
int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;

        if (B == 0)
            throw 2;

        C = A / B;
    }
    catch (int num) {
        cout << "Error code: " << num << endl;
    }
    return 0;
}
```
```

+   a. Error code: 2
+   b. Syntax error
+   c. No output
+   d. Garbage value