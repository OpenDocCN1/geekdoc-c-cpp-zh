# 20 • Inheritance 653

To clarify once more, the fact that there is no A copy constructor that accepts a B reference parameter does not produce a compilation error, because the A copy constructor takes a A reference parameter, and as we've learned, a base class reference can refer to a derived type. Thus, the A copy constructor uses the A part of the argument to construct the A sub-object. So, b2.a becomes 11 and b2.t becomes 31. The program displays these.

Note that if you employ the call to the copy constructor of A, that is, you write:

```
B(const B& b) : t(b.t + 1) {
```

the compilation fails. The reason is that the compiler knows it has to create a A sub-object, but it is not specified how to do it. If you not call by the copy constructor of A, you have to tell the compiler to do so.
Note that this example has practical besides exercises; it serves to see how to call a base class copy constructor from a derived class in case you want to use your own copy constructors. If you do not have a reason to do so, and most probably you won't, let the default copy constructors copy the members and do not define your own. It is dangerous, for example, you can very easily copying a member or if you add a new member in the future you might forget to copy it.

# Define a Copy Assignment Function in a Derived Class

Like the copy constructor of the derived class, the copy assignment function must copy the members of the base sub-object. Consider the following program:

```
#include <iostream> // Example 20.7

class A
{
public:
    int v;
    A(int i) : v(i) {}
};

class B
{
public:
    int r;
    B(int i) : A(i+5), r(i) {}
    B& operator=(const B& b);
};

B& B::operator=(const B& b)
{
    A::operator=(b); // Copy the members of the base sub-object.
    r = b.r;
    return *this;
}

int main()
{
    B b1(10), b2(20);

    b2 = b1; // Equivalently, b2.operator=(b1);
    std::cout << b2.v << ' ' << b2.r << ' '\n';
    return 0;
}
```