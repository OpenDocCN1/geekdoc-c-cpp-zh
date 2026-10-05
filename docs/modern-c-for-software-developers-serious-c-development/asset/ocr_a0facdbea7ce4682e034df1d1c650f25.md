Notice that we can use a struct wherever we can use a class. Usually it is best to use a class when we want a class, and a struct when we want a C-like structure.

# Unions And Classes

In C++, unions can contain both member functions and data members. They can also include constructor and destructor functions. A union in C++ retains all of its C features. In a union, all of the data elements share the same location in memory. Like a struct, union members are public by default.

Here is an example:

```
#include <iostream>
using namespace std;

union swapByte
{
    void swap();
    void setColor(unsigned short i);
    void showWord();

private:
    unsigned short u;
    unsigned char c[2];
};

void swapByte::swap() {
    unsigned char t;
    t = c[0];
    c[0] = c[1];
    c[1] = t;
}

void swapByte::showWord() {
    cout << u;
}

void swapByte::setColor(unsigned short i) {
    u = i;
}

int main()
```