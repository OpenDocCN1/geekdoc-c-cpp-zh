```
```cpp
//https://godbolt.org/z/dzjaf6nbb
#include <string>
#include <string_view>
using std::string; using sview = std::string_view;

struct Person {
    string name_;
    int age_;
    string city_;
    Person(sview n, int a, sview c)
    {                   // // initialization list missing
        init(n, a, c); // // questionable initialization call
    }
    void init(sview n, int a, sview c) {
        name_ = n; age_ = a; city_ = c;
    }
};
```
```

# **Listing 12.18** Do not call an initializing method in the constructor body.

So feel free to use such an init method, but only when the object is already completely finished and the constructor code has already been exited. Sometimes you need this approach to initialize your objects in two phases: if the objects need each other, first construct all of them and then call the necessary `init()` methods.

# 12.8.5 Exceptions in the Constructor

Exceptions have a special significance within constructors. They prevent the object from being created. You can see the exact effects in Chapter 16.

# 12.9 Struct or Class?

A type that contains a constructor is no longer an aggregate; it is a *structure*. This term comes from the fact that you introduce the type declaration with `struct`.

You will sometimes hear the term *class* instead—and that is also correct, because instead of `struct` ... you can just as well write `class` ... There is only a tiny difference in meaning between `struct` and `class` in C++:

+   - **struct**
+     A struct initially has public access rights.
+   - **class**
+     A class starts with private access rights.