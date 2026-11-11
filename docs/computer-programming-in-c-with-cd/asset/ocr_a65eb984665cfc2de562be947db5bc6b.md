```
```cpp
{ cout << "Derived constructor called\n"; };
~Derived()
{
    { cout << "Derived destructor called\n"; };
}
};

void main()
{
    Derived my_class;
}
```
```

Ans. The output of the preceding program is as follows:

```
```
Constructor for One
Constructor for Two
Constructor for Three
Derived constructor called
Derived destructor called
Destructor for Three
Destructor for Two
Destructor for One
```
```

# Q8. What is the output of the following program?

```
```cpp
#include <iostream.h>

class BClass {
    int i;
public:
    BClass(int n) {
        cout << "Constructor of base class"<< endl;
        i = n;
    }
    ~BClass() {
        cout << "Destructor of base class"<< endl;
    }
    void show() {
        cout << i << endl;
    }
};

class DClass : public BClass {
    int j;
public:
    DClass(int x, int y) : BClass(x) {
        cout << "Constructor of derived class\n";
        j = y;
    }
    ~DClass() {
        cout << "Destructor of derived class\n";
    }
```
```