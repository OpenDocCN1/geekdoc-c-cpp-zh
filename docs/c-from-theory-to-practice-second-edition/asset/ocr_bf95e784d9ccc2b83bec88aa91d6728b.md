```
b.show();
b.display();
return 0;
}
```

Since the members a and show() are declared as private, the objects and the functions of class B cannot access them. Since x is declared as protected, access from an object of a derived class is not allowed. As a result, the following statements are illegal:

```
cout << a << ' ' << k << endl; // in display
cin >> b.a;
cin >> b.x;
b.show();
```

Since x is declared in the derived class B, not in the base class A, the following statement is wrong:

```
cout << k << endl; // in check_B()
```

Besides single inheritance, C++ supports multiple inheritance. In multiple inheritance, a new class may be derived from two or more base classes. For example:

```
#include <iostream>
using namespace std;

class A
{
public:
    int a;
    void show_A();
};
void A::show_A()
{
    cout << a << endl;
}

class B
{
public:
    int b;
    void show_B();
};
void B::show_B()
{
    cout << b << endl;
}

class C : public A, public B
{
public:
    void show_C();
};
```