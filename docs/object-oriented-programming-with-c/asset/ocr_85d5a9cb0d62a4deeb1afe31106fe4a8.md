In some situations, we may not be able to anticipate all possible types of exceptions and therefore may not be able to design independent **catch** handlers to catch them. In such circumstances, we can force a **catch** statement to catch all exceptions instead of a certain type alone. This could be achieved by defining the **catch** statement using ellipses as follows:

```
```
catch(...)
{
    // Statements for
    processing
    // all exceptions
}
```
```

```
```
#include <iostream>
using namespace std;
void test(int x)
{
    try
    {
    if(x == 0) throw x;    // int
    if(x == -1) throw 'x';   // char
    if(x == 1) throw 1.0;    // float
    }
    catch(...)    // catch all
    {
    cout << "Caught an exception \n";
    }
}
int main()
{
    cout << "Testing Generic Catch \n";
    test(-1);
    test(0);
    test(1);
}
```
```