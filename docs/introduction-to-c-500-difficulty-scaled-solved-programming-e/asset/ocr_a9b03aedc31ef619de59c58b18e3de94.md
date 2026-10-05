# 820 Introduction to C++

```
class B : public A
{
public:
    virtual void show() const override {std::cout << "B\n";
};
```

```
class C : public B
{
public:
    virtual void show() const override {std::cout << "C\n";
};
```

```
int main() {
    B *b = new B;
    A *a = dynamic_cast<A*>(b); // Safe cast.
    if(a) {
        a->show();
        std::cout << ' ' << b << '\n';
    }
    C *c = dynamic_cast<C*>(b); // Not safe cast.
    if(c) {
        c->show();
    } else {
        std::cout << "Error\n";
    }
    delete b;
    return 0;
}
```

The first cast is safe and the dynamic_cast operator returns a non-null pointer. show() is virtual and the pointer points to an object of the B class, the program displays B. Then, since the a and b pointers point to the same address, the program displays the same value. Because the second cast is not safe, the operator returns a null pointer and the program displays Error.

As we said, we can apply dynamic_cast to a reference. In case of failure the notion of null reference does not exist to be returned, the operator throws an exception of type bad_cast. This exception is derived from the exception class and it is declared in the typeinfo file. For example:

```
#include <iostream> // Example 25.4
#include <typeinfo>
int main() {
    B b;
    B &br = b;
    try {
        C &c = dynamic_cast<C&>(br); // Not safe cast.
    } catch (std::bad_cast&) {
        std::cout << "bad_cast exception is caught\n";
    }
    return 0;
}
```