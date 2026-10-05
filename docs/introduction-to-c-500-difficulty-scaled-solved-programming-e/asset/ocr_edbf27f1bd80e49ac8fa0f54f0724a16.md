```
r.f();
r.g();
r.v();
return 0;
}
```

When a pointer or reference is used to call a function we check if the function is virtual or not. If the binding is static and we look at the type of the pointer or reference. If it is virtual, the binding is dynamic and we look at the type of the object pointer points to or reference refers to. Let's apply this rule to the program.

Since f is not virtual, the compiler uses static binding to select which version to call. Because the type of r is reference to class A, A.f() will be called. Since g() is virtual, dynamic binding is used. Because the type of b is the object referred by r is class B, B.g() will be called. The declaration of v() is virtual in the derived class and not in the base class has no effect. Thus, as a result, the program displays: A B A

Now, we've discussed virtual functions let's sum up. C++ supports:

+   a. Polymorphism at compile time (e.g., templates).
b. Polymorphism at runtime through virtual functions.

# Using the override and Final Specizers

C++11 introduced the word override as a safeguard against mistakes in the declaration of the virtual function in a derived class. For example:

```
class Book : public Product
{
    void show() override;
    void show(); // Wrong
};
```

The word override is added at the end of the declaration and explicitly states that the class will override the inherited virtual function. Also, as with the word virtual, it is wrong to be added in a def-ition for the class.

```
virtual void Book::show(); // Wrong.
void Book::show() override {}; // Wrong.
```

The use of override specifier protects us from potential oversights, which may lead to errors that are difficult to spot. For example, what does the following program display?

```
#include <iostream> // Example 20.10
using std::cout;

class A
{
public:
    void f() const { cout << "A \ }
    virtual void g() const { cout << "A \ };
};
```