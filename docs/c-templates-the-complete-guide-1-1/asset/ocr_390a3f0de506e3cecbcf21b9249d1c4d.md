```
~~~cpp
y[i] {
}
~~~
```

This formulation requires some more work for each class that will be mixed in, so classes such as label and color will need to become class templates. However, the mixed-in class can now tailor their behavior to the specific instance of the derived class they've been mixed into. For example, we can mix the previously discussed Object counter template into the root: the number of objects created by each class can be counted by that mixin with other application-specific mixins as well.

# 21.3.2 Parameterized Virtuality

Mixins also allow us to indirectly parameterize other attributes of the derived class, such as the virtuality of a member function. A simple example shows this rather surprising technique:

Click here to view code image

inherit/virtual.cpp

```
~~~cpp
#include <iostream>

class NotVirtual {
};

class Virtual {
public:
    virtual void foo() {
    }
};

template<typename... Mixins>
class Base :
    public Mixins... {
public:
    // the virtuality of foo() depends on its declaration
    // (if any) in the base classes Mixins.
    void foo() {
        std::cout << "Base::foo()\n";
    }
};

template<typename... Mixins>
class Derived : public Base<Mixins...> {
public:
    void foo() {
        std::cout << "Derived::foo()\n";
    }
};

int main()
{
    Base<NotVirtual> *p1 = new Derived<NotVirtual>();
    p1->foo(); // calls Base::foo()

    Base<Virtual> *p2 = new Derived<Virtual>();
    p2->foo(); // calls Derived::foo()
}
~~~
```

This technique can provide a tool to design a class template that is usable both to instantiate concrete classes and to extend using inheritance. However, it is rarely sufficient just to specialize virtuality on some member functions to obtain a class that makes a good base class for more specialized functionality. This sort of development method requires more fundamental design decisions. It is therefore usually more practical to design two different tools (a class or class template hierarchy) than try to fit everything into one template hierarchy.