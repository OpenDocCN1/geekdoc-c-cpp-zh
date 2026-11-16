The internal data structures that get created are shown below:

Base class object                   Base vtable
+---+                               +---+
| i | -------------------> 0        | &foo() -------> Base::foo()
+---+                               +---+
| vptr ----------------> 1          | &faa() -------> Base::faa()
+---+                               +---+
                                    2   | &laa() -------> Base::laa()
                                        +---+

A derived class is declared as follows:

```
class Derived : public Base {
  public:
    virtual void faa();
    virtual void taa();
};
```

Its internal data structures are shown below:

Derived class object                Derived vtable
+---+                               +---+
| i | -------------------> 0        | &foo() -------> Base::foo()
+---+                               +---+
| vptr ----------------> 1          | &faa() -------> Derived::faa()
+---+                               +---+
                                    2   | &laa() -------> Base::laa()
                                        +---+
                                    3   | &taa() -------> Derived::taa()
                                        +---+