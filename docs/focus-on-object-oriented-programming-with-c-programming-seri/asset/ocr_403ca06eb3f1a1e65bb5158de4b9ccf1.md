# Base and Derived Class Destructors

A derived class typically provides a constructor if its base class has one, and a base class constructor must be called in order to initialize any data members in the base class. Destructors, on the other hand, do not require such strict handling. A derived class needs to supply a destructor only if the derived class has any members that require deleting when an object of the derived class goes out of scope.

```
// dtor.cpp

#include <iostream>
#include <string.h>

using namespace std;

class Base {
private:
    char *buf;
public:
    Base(char *s) {
        buf = new char[strlen(s) + 1];
        strcpy(buf, s);
    }
    ~Base() {
        delete [] buf;
    }
    char *getStr() {
        return buf;
    }
};
```

Note that the constructor copies a string argument to the heap, assigning the address of the allocated memory to buf. The destructor deletes this memory block when an object of type Base goes out of scope. Consider what happens in a new class derived from Base: