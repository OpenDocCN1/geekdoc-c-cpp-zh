# 20 • Inheritance 677

```
int main()
{
    Product prod(100);
    Book b("C++", 200);

    Product *p1 = &prod;
    Product *p2 = &b;
    f(p1, p2);
    return 0;
}
```

```
void f(const Product *p1, const Product *p2)
{
    p1->show();
    p2->show();
}
```

Answer: Since the exercise restricts us that the two pointers in f() must be of the same type and we see that the calls of show() in f display the members of both the Product and the Book objects we understand that the show() must be declared as virtual. Type should be a pointer to the base class, so that a pointer to the derived class can be passed (e.g., p2) and the mechanism of the virtual functions comes into effect. If show() was not declared as virtual, the program would call twice of the Product class and display 100 and 200.

# C.20.5 What is the output of the following program?

```
#include <iostream>
using std::cout;

class A
{
private:
    int k;
public:
    A() {k = 1};
    void f() const { cout << k; }
    virtual void v() const { cout << "A.v"; }
};
```

```
class B : public A
{
private:
    int k;
public:
    B() {k = 2};
    void f() const { cout << k; }
    virtual void v() const override { cout << "B.v"; }
};
```

```
void t1(A a)
{
    a.f();
    a.v();
}
```