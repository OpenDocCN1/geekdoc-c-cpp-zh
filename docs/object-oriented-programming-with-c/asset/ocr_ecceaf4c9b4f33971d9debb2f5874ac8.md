of the order in the initialization list. This enables us to have statements such as

```
XYZ(int i, int j) : a(i), b(a * j) { }
```

Here a is initialized to 2 and b to 6. Remember, a which has been declared first is initialized first and then its value is used to initialize b. However, the following will not work:

```
XYZ(int i, int j) : b(i), a(b * j) { }
```

because the value of b is not available to a which is to be initialized first.

The following statements are also valid:

```
XYZ(int i, int j) : a(i) { b = j; }
XYZ(int i, int j) { a = i; b = j; }
```

We can omit either section, if it is not needed. Program 8.8 illustrates the use of initialization lists in the base and derived constructors.

# Program 8.8  Initialization List in Constructors

```
#include <iostream>
using namespace std;
class alpha
{
int x;
public:
alpha(int i)
{
x = i;
cout << "\n alpha constructed";
```