is the case with normal methods—for example, with func(), which you can also call for Derived instances.

The reason for this is that constructors are really different from methods. A constructor must initialize a class instance. This is a task that is closely tied to the internal structure of the class. Calling a parent class constructor instead of its own constructor is very likely not achieving a correct initialization of the derived class. There may be administrative information related to the class that needs to be initialized in the respective constructor. What administrative information is needed is not specified in detail by the standard; it is left to the implementation. To allow this freedom, constructors have this special role.

If you still want to inherit the parent class constructors, you must explicitly specify this in the derived class. To achieve this, include using Base::Base; in the class definition, thereby explicitly referencing the constructors. Yes, constructors, plural—because this approach elevates all inherited constructors simultaneously, rather than just one. You can only employ this mechanism by following the all or nothing principle.

```
//://godbolt.org/z/h15eagjhh
class Base {
public:
    Base() {}
    explicit Base(int i) {}
    Base(int i, int j) {}
    void func() {}; // method
};

class Derived : public Base {
public:
```