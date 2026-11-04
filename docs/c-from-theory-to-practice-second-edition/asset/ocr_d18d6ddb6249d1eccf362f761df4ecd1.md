The accessibility_type specifies the accessibility to the members of the base class. To give you an idea how inheritance works, we'll use the type public. It is one of several possibilities, too detailed to describe all options. When the public type is used, the functions and the objects of the derived class can access the public members of the base class and cannot access the private members. The functions of the derived class can access the protected members of the base class; the objects of the derived class cannot do the same though.

Inheritance usually provides increasing specialization from a general class (e.g., Product) to a more specific derived class (e.g., Book). For example:

```
```cpp
#include <iostream>
#include <string>
using namespace std;

class Product
{
public:
    string code;
    float prc;

    void init(string c, float p);
    void show();
};

class Book : public Product
{
public:
    string title;
    string auth;
    int pages;

    void display();
};

void Product::init(string c, float p)
{
    code = c;
    prc = p;
}

void Product::show()
{
    cout << "\nP:" << prc << " C:" << code << endl;
}

void Book::display()
{
    cout << "T:" << title << " A:" << auth << " P:" << pages << endl;
}
```
```