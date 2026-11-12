+   - (d) Using virtual functions will slow down the execution speed as the binding happens runtime.

Answer: (b) and (d)

# 71. What is the output of the following piece of code? Also point out the error in the code which could be logical. (L4)

```
```cpp
#include <iostream>
using namespace std;
class Base_class {
public:
    Base_class ()
    {
        cout << "This is a base class constructor" << "\n";
    }
    ~Base_class ()
    {
        cout << "This is a base class destructor" << "\n";
    }
};
class Derived_class : public Base_class {
public:
    Derived_class ()
    {
        cout << "This is a Derived class constructor" << "\n";
    }
    ~Derived_class ()
    {
        cout << "This is a Derived class destructor" << "\n";
    }
};
int main()
{
    Base_class *b;
    b = new Derived_class;
    delete b;
    return 0;
}
```
```

Answer: The expected output would not arrive and the following is the output one would get.

This is a base class constructor.
This is a Derived_class constructor.
This is a base class destructor.

Reasoning: If the destructor in the base class is not made virtual, then an object that might have been declared of type base class and instance of child class would simply call the base class destructor without having called the derived class destructor. This can be related and is synonymous to the previous learning about the virtual functions.

# 72. What is the output of the following piece of code? (L4)

```
```cpp
#include <iostream>
using namespace std;
class Base_class {
public:
    Base_class ()
    {
        cout << "This is a base class constructor" << "\n";
    }
    virtual ~Base_class ()
    {
        cout << "This is a base class destructor" << "\n";
    }
};
class Derived_class : public Base_class {
public:
    Derived_class ()
    {
        cout << "This is a Derived class constructor" << "\n";
    }
    ~Derived_class ()
    {
        cout << "This is a Derived class destructor" << "\n";
    }
};
int main()
{
```
```