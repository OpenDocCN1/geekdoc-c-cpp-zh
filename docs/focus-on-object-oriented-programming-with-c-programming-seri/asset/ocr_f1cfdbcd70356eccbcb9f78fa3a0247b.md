Note that the destructor for the `Derived` class did not get called. The memory leaker can thus leak the buffer `pBuf` because it was allocated in the `Derived` constructor. To fix this, simply declare the destructor of the `Base` class as a virtual function, as in:

```
class Base {
public:
    Base();
    virtual ~Base();
};
```

As modified, the program output will be:

```
Base::Base()
Derived::Derived()
Derived::~Derived()
Base::~Base()
```

Now the `Derived` class destructor is called, and `Derived::pBuf` is deleted.

# Conclusion

Now you have seen a number of handy tricks of the trade that varsity-level C++ programmers use to implement memory leakage. If you use the tactics described above, you will not have to invent your own. Code reuse is, after all, what C++ is all about. A cautionary note: these memory leak scenarios are made possible by improper use of C++. They are not intrinsic to the language. As such, when your application runs out of memory at a customer site on the other side of the planet, you may not be successful in casting the blame on C++.