return 0;
}

+   a. ###Exception Received
+   b. @@@Exception Received
+   c. Syntax error
+   d. No output

# 51. What is the correct output of the given code?

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
        if (B == 0) {
            bad_exception E;
            throw E;
        }
        C = A / B;
    }
    catch (bad_exception E) {
        cout << "@@@Exception Received" << endl;
    }
    catch (exception E) {
        cout << "###Exception Received" << endl;
    }
    return 0;
}
```
```

+   a. ###Exception Received
+   b. @@@Exception Received
+   c. Syntax error
+   d. No output