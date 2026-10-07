# New Class Features

already present in other constructors. To make coding simpler and more reliable, C++11 allows to use a constructor as part of the definition of another constructor. This process is termed delegation because one constructor delegates responsibility to another to work on the object it is constructing. Delegation uses a variant of the member initialization list syntax:

```
class Notes {
    int k;
    double x;
    std::string st;
public:
    Notes();
    Notes(int);
    Notes(int, double);
    Notes(int, double, std::string);
};
Notes::Notes(int kk, double xx, std::string stt) : k(kk),
    x(xx), st(stt) {/*/ do other stuff*/}
Notes::Notes() : Notes(0, "0") {/*/ do other stuff*/}
Notes::Notes(int kk) : Notes(kk, 0.01, "Ah") {/*/ do other stuff*/ }
Notes::Notes(int kk, double xx) : Notes(kk, kk, "Uh") {/*/ ditto stuff*/}
```

The default constructor, for example, uses the first constructor in the list to initialize the data members and also to do whatever the body of that constructor requests. Then it finishes up doing whatever its own body requests.

# Inheriting Constructors

In another move to simplify coding, C++11 provides a mechanism for derived classes to inherit constructors from the base class. C++98 already had a syntax for making functions from a namespace available:

```
namespace Box {
    int fn(int) { ... }
    int fn(double) { ... }
    int fn(const char*) { ... }
}
using Box::fn;
```

This makes all the overloaded fn functions available. The same technique works for making nonlocal member functions of a base class available to a derived class. For example, consider the following code:

```
class Cl {
    ...
public:
    ...
```