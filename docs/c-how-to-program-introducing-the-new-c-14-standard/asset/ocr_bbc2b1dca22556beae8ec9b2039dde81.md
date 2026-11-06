```
```cpp
// Fig. 9.23: Fig09_23.cpp
// Friends can access private members of a class.
#include <iostream>
using namespace std;

// Count class definition
class Count {
    friend void setX(Count&, int); // friend declaration
public:
    int getX() const {return x;}
private:
    int x{0};
};

// function setX can modify private data of Count
// because setX is declared as a friend of Count (line 8)
void setX(Count& c, int val) {
    c.x = val; // allowed because setX is a friend of Count
}

int main() {
    Count counter; // create Count object

    cout << "counter.x after instantiation: " << counter.getX() << endl;
    setX(counter, 8); // set x using a friend function
    cout << "counter.x after call to setX friend function: "
        << counter.getX() << endl;
}
```
```

```
```text
counter.x after instantiation: 0
counter.x after call to setX friend function: 8
```
```

# Fig. 9.23 **Friends** can access **private** members of a class.

Function `setX` (lines 17–19) is a standalone (global) function—it isn’t a member function of class `Count`. For this reason, when `setX` is called for object `counter`, line 25 passes `counter` as an argument to `setX` rather than using a handle (such as the name of the object) to call the function, as in