> **Remember!** If you want to display a string on the screen, the string must be enclosed in double quotes.

The following C++ program:

```
```cpp
#include <iostream>
using namespace std;
int main() {
    int a;

    a = 5 + 6;
    cout << "The sum of 5 and 6 is " << a;
    return 0;
}
```
```

displays the message shown in **Figure 6–1.**

![](bbox=[0.38, 0.355, 0.748, 0.55])

**Figure 6–1** A string displayed on the screen

> **Notice:** Please note the space inserted at the end of the first string in C++, just after the word “is.” If you remove it, the number 11 will get too close to the last word and the output on the screen will be
> 
> *The sum of 5 and 6 is11*

You can also calculate the result of a mathematical expression directly in a `cout` statement. The following statement:

```
```cpp
#include <iostream>
using namespace std;
int main() {
    cout << "The sum of 5 and 6 is " << 5 + 6;
    return 0;
}
```
```

displays exactly the same message as the statements in **Figure 6–1.**

> **Notice:** Please note that C++ requires that all statements be terminated with a semicolon.