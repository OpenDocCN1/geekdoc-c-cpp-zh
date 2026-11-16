instantiates a derived-class object and stores the address as a pointer to its base class:

```
#include <iostream>
using namespace std;
class Base {
public:
Base();
~Base();
};
class Derived : public Base {
protected:
char *pBuf;
public:
Derived();
~Derived();
};
Base::Base() {
cout << "Base::Base()" << endl;
}
Base::~Base() {
cout << "Base::~Base()" << endl;
}
Derived::Derived() : Base() {
pBuf = new char[100];
cout << "Derived::Derived()" << endl;
}
Derived::~Derived() {
delete[] pBuf;
cout << "Derived::~Derived()" << endl;
}
int main() {
Base *pObject = new Derived();
delete pObject;
return 0;
}
Output:
Base::Base()
Derived::Derived()
Base::~Base()
```