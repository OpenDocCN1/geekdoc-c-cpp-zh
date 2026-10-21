```
```cpp
void equal(T1 x, T2 y)
{
const char *p1 = typeid(x).name();
const char *p2 = typeid(y).name();
if(strcmp(p1,p2) == 0)
cout << "Data type " << p1 << " and " << p2 << " is same " << endl;
else
cout << "Data type " << p1 << " and " << p2 << " is not same" << endl;
}
```
```

typeid(x).name() returns the data type as constant string so p1 stores “int” and p2 stores “float”, both as string. Later we compare whether two strings are same or not by comparing them using strcmp( ). If strcmp return two data type are same otherwise not same. Same for other call to equal hold.

```
```cpp
/* PROG 13.7 CHECKING EQUALITY OF DATA TYPE OF TWO VARIABLES USING FUNCTION TEMPLATE VER 2 */
#include <iostream.h>
#include <typeinfo.h>
#include <string.h>
template <class T1, class T2>
void equal(T1 x, T2 y)
{
const char*p1 = typeid(x).name();
const char*p2 = typeid(y).name();
if(strcmp(p1,p2) == 0)
cout << "Data type " << p1 << " and " << p2 << " is same" << endl;
else
cout << "Data type " << p1 << " and " << p2 << " is not same" << endl;
}
void main()
{
equal(23.45, 23.45);
equal('A',65);
equal(2.0, 2.0f);
equal("str",(int*)"str");
}
```
```