# 9.2.3.1.2 Virtuality

When you override a virtual interface function, the overriding function should have a lock even if the function is private.

The Thread Safe Interface with a virtual member function

```
```cpp
// ThreadSafeInterfaceVirtual.cpp

#include <iostream>
#include <mutex>
#include <thread>

class Base{

public:
    virtual void interface() {
        std::lock_guard<std::mutex> lockGuard(mut);
        std::cout << "Base with lock" << '\n';
    }
private:
    std::mutex mut;
};

class Derived: public Base{

    void interface() override {
        std::cout << "Derived without lock" << '\n';
    }

};

int main(){

    std::cout << '\n';

    Base* base1 = new Derived;
    base1->interface();

    Derived der;
    Base& base2 = der;
    base2.interface();

    std::cout << '\n';

}
```
```