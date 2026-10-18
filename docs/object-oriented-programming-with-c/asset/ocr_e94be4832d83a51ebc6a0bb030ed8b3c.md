The output of Program 12.3 would be:

+   Instantiating the class template as test1 with float and int data types..
+   test1: 1.23 and 123
+   Instantiating the class template as test2 with int and char data types..
+   test2: 100 and W

Just as we specify default values for function arguments, we may also specify default types for the template class data types. Program 12.4 modifies Program 12.3 to demonstrate default type specification:

# Program 12.4 Using Default Data Types in a Class Definition

```
#include <iostream.hgt>;
using namespace std;
template<class T1=int, class T2=intgt; //default dta types specified
as int
class Test
{
    T1 a;
    T2 b;
public:Test(T1 x, T2 y)
}
```