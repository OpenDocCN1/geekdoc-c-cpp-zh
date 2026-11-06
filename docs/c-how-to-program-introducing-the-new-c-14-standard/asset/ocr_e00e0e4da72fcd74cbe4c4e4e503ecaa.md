```
```cpp
// Fig. 9.24: fig09_24.cpp
// Using the this pointer to refer to object members.
#include <iostream>
using namespace std;

class Test {
public:
    explicit Test(int);
    void print() const;
private:
    int x{0};
};

// constructor
Test::Test(int value) : x{value} {} // initialize x to value

// print x using implicit then explicit this pointers;
// the parentheses around *this are required
void Test::print() const {
    // implicitly use the this pointer to access the member x
    cout << "x = " << x;

    // explicitly use the this pointer and the arrow operator
    // to access the member x
    cout << "\n this->x = " << this->x;

    // explicitly use the dereferenced this pointer and
    // the dot operator to access the member x
    cout << "\n(*this).x = " << (*this).x << endl;
}

int main() {
    Test testObject{12}; // instantiate and initialize testObject
    testObject.print();
}
```
```

```
x = 12
this->x = 12
(*this).x = 12
```

**Fig. 9.24** Using the `this` pointer to refer to object members.

For illustration purposes, member function `print` (lines 19–30) first prints `x` by using the `this` pointer *implicitly* (line 21)—only the name of the data member is specified. Then `print` uses two different notations to access `x` through the `this` pointer—the arrow operator (`->`) off the