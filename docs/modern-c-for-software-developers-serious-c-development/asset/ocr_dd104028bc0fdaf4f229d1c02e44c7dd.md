derived class.

```
// Demonstrate typeid with a reference parameter
#include <iostream>
#include <typeinfo>
using namespace std;

// Mammal is a polymorphic class
class Mammal {
public:
    virtual bool lays_eggs() { return false; }
};
class Cat: public Mammal {
};
class Platypus: public Mammal {
public:
    bool lays_eggs() { return true; }
};

void MammalType(Mammal& obj) {
    cout << "obj is referencing an object of type ";
    cout << typeid(obj).name() << endl;
}

int main() {
    Mammal AnyMammal;
    Cat cat;
    Platypus platypus;

    MammalType(AnyMammal);
    MammalType(cat);
    MammalType(platypus);
}

// output
obj is referencing an object of type Mammal
obj is referencing an object of type Cat
obj is referencing an object of type Platypus
```