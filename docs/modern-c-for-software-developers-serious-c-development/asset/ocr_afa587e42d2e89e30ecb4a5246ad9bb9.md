We can inherit a base class in protected access mode. When this is done, all of the public and protected members of the base class become protected members of the derived class.

```
#include <iostream>

class Base {
protected:
    // private to base, but inheritable by Derived
    int i, j;
public:
    void setij(int a, int b) { i = a; j = b; }
    void showij() { std::cout << i << " " << j << "\n"; }

// Inherit Base as protected.
class Derived : protected Base
{
    int k;
public:
    void setk() { setij(10, 12); k = i*j; }
    void showall() { std::cout << k << " " << showij(); }
}

int main() {
    Derived obj;

    obj.setk();      // OK, setij is a protected member of derived
    obj.showall();   // OK, public member of derived
    // obj.showij(); // Error, showij is protected of derived

    return 0;
}

// output
120 10 12
```

# Pointers To Derived Classes

In general, a pointer to one type of object cannot point to an object of a different type. However, there is an important exception to this rule that only applies to derived