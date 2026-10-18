+   - It is initialized to zero when the first object of its class is created. No other initialization is permitted.
+   - Only one copy of that member is created for the entire class and is shared by all the objects of that class, no matter how many objects are created.
+   - It is visible only within the class, but its lifetime is the entire program.

Static variables are normally used to maintain values common to the entire class. For example, a static data member can be used as a counter that records the occurrences of all the objects. Program 5.4 illustrates the use of a static data member.

# Program 5.4  Static Class Members

```
```cpp
#include <iostream.h>
using namespace std;
class item
{
static int count;
int number;
public:
void getdata(int a)
{
    number = a;
    count++;
}
void getcount(void)
{
    cout << "count:";
    cout << count << '\n';
}
}
```
```