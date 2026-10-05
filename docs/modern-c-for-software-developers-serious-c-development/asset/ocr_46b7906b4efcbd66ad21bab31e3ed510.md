The following example, demonstrates this:

```
#include <iostream>
using namespace std;

class Base {
public:
    virtual void vfunction() {
    cout << "This is the base class vfunction()\n";
};

class Derived1 : public Base {
public:
    void vfunction() {
    cout << "This is the derived1 class vfunction()\n";
};

class Derived2 : public Base {
public:
    void vfunction() {
    cout << "This is the derived2 class vfunction()\n";
};

void print(base* bPtr) {
    bPtr->vfunction();
}

int main() {
    Base *p, b;
    Derived1 d1;
    Derived2 d2;

    // point to the Base class instance
    p = &b;
    print(p); // access the base instance vfunction()

    // point to Derived1
    p = &d1;
    print(p); // access the derived1 instance vfunction()
```