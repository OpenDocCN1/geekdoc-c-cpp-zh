# Program 6.21  Shadowing in global scope

```
```cpp
/************************************************************/
/* A program to test shadowing of global scope              *
 ************************************************************/
#include <iostream>
using namespace std;

int num = 5;   // Global variable

int main()
{
    cout << num << endl;   // global num
    int num = 25;          // local variable
    cout << num;           // local num shadows global num
    return 0;
} // End of main

Run
5
25
```
```

![](bbox=[0.373, 0.477, 0.844, 0.58])

**Figure 6.25**  Two versions of scope resolution operator

**Scope Resolution Operator** Sometimes we may need to override the shadowing and access a global entity inside a local block. C++ provides an operator (`::`) that can explicitly or implicitly define the scope of the entity. Figure 6.25 shows the two versions of this operator. The first version takes one right operand; the second version takes two operands.

In the first version, the name of the scope is implicit (it means the global scope of the program). In the second version, we must give the name of the scope. Program 6.22 shows the use of the first version of the scope operator.

# Program 6.22  Using the scope resolution operator

```
```cpp
/************************************************************/
/* A program to test the use of scope operator              *
 ************************************************************/
#include <iostream>
using namespace std;
```
```