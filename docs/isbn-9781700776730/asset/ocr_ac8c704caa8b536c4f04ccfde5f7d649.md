# Constructor Initializer List

One of the easiest ways to improve a C++ program's efficiency is to specify an appropriate base class constructor function in the colon list of a derived class constructor function. What happens without a constructor initialization list?

+   - To initialize an object of a particular class, your program calls the appropriate constructor for that class.

+   - To initialize a derived class's object, your program implicitly calls the appropriate base class constructor function.

Unfortunately, that implicit call to the base class constructor function makes it easy to initialize the base class's data members twice! See the example below:

```
// shape1.cpp
#include <iostream>

uses std;

class Shape {
private:
    int color;
    int sideCount;
public:
    Shape() {
        cout << "Shape default constructor" << endl;
        SetColor(0);
        SetSideCount(0);
    }
    Shape(int c, int sc) {
        cout << "Shape 2 arg constructor" << endl;
        SetColor(c);
        SetSideCount(sc);
    }
    void display() {
        cout << "color = " << color << endl;
        cout << "sides = " << sideCount << endl;
    }
    void SetColor(int c) {
        cout << "set color to " << c << endl;
    }
    void SetSideCount(int sc) {
        cout << "set side count to " << sc << endl;
        sideCount = sc;
    }
};
```