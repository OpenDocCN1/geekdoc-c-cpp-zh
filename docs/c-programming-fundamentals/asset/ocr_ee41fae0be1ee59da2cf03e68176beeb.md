# Code: Working with Interfaces

```
```cpp
#include <iostream>
using namespace std;
class myInterface
{
public:
virtual void Purely() = 0;
void method1()
{
cout<<"\nParent class method"<<endl;
}
};
class child1: public myInterface
{
public:
void Purely()
{
cout<<"\nParent method redefined"<<endl;
}
};

int main()
{
cout<<"\nInterfaces"<<endl;
child1 c1;
c1.Purely();
c1.method1();
return 0;
}
```
```

# Output:

```
```text
Interfaces
Parent method redefined
Parent class method
```
```

# Code Debriefing

+   - Here, the interface concept is being applied.
+   - Static binding is implemented using function overloading.
+   - The method is redefined in the child class as it can inherit and modify properties.