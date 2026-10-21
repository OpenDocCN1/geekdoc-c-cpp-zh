Consider the following program to understand how to invoke the base class object. It is needless to say that if the object members are not qualified this way, the compiler will get confused (whether to use a base class member from Derived1 or Derived2) and will not compile the program.

```
#include <iostream>
#include <string>
using namespace std;
// Base class
class Base
{
public:
    int BaseInt;
};
// First derived class
class Derived1 : public Base
{
public:
    int Derived1Int;
};
// Second derived class
class Derived2 : public Base
{
public:
    int Derived2Int;
};
// Multiple inheritance
class DDerived : public Derived1, public Derived2
{
public:
    int DDerivedInt2;
};
void main()
{
    DDerived DD;
    // DD.BaseInt = 0;
    // Error: ambiguous access of 'BaseInt' in 'DDerived'
    DD.Derived1::BaseInt = 0; // Now it is not ambiguous
    DD.Derived2::BaseInt = 10;
    /* Yes. This is different from previous BaseInt */
    cout << DD.Derived1::BaseInt << "\n";
    cout << DD.Derived2::BaseInt << "\n";
}
```

Output

0

10

In this example, it is not possible to access the base class member as it is. It needs to be qualified with the derived class name.