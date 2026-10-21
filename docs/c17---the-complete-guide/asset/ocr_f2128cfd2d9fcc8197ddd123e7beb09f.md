This does not work automatically because the corresponding constructor is a template, which means that no implicit deduction guide applies:

```
namespace std {
    template<typename T> class shared_ptr {
        public:
            ...
            template<typename Y> explicit shared_ptr(Y* p);
            ...
    };
}
```

Y is a different template parameter to T, meaning that deducing Y from the constructor does not mean that we can deduce type T. This is a feature to be able to call something like:

```
std::shared_ptr<Base> sp{new Derived(...)};
```

The corresponding deduction guide would be simple to provide:

```
namespace std{
    template<typename Y> shared_ptr(Y*) -> shared_ptr<Y>;
}
```

However, this would also mean that this guide is taken when allocating arrays:

```
std::shared_ptr sp{new int[10]};      // OOPS: would deduce shared_ptr<int>
```

As so often in C++, we run into the nasty C problem that the type of a pointer to one object and an array of objects have or decay to the same type.

This problem seems dangerous and therefore, the C++ standards committee has decided not to support it.

For single objects, you still have to call:

```
std::shared_ptr<int> sp1{new int};      // OK
auto sp2 = std::make_shared<int>();      // OK
```

and for arrays:

```
std::shared_ptr<std::string> p(new std::string[10],
    [](std::string* p) {
        delete[] p;
    });
```

or, using the new feature to instantiate shared pointers for raw arrays, just:

```
std::shared_ptr<std::string[]> p{new std::string[10]};
```

# 9.3 Afternotes

Class template argument deduction was first proposed in 2007 by Michael Spertus in http://wg21.link/n2332. The proposal was revisited in 2013 by Michael Spertus and David Vandevoorde in http://wg21.link/n3602. The finally accepted wording was formulated by Michael Spertus, Faisal Vali, and Richard Smith in http://wg21.link/p0091r3, with modifications by Michael Spertus, Faisal Vali, and