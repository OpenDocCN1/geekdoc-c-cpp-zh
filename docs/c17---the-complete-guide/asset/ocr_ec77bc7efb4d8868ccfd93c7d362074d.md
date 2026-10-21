```
a.reset();  // makes it empty
```

or:

```
a = std::any{};
```

or just:

```
a = {};
```

You can also check directly whether the object is empty:

```
if (a.has_value()) {
    ...
}
```

Note also that values are stored using their decayed type (arrays convert to pointers, and top-level references and const are ignored). For string literals, this means that the value type is const char*. To check against type() and use std::any_cast<>, you have to use exactly this type:

```
std::any a = "hello";  // type() is const char*
if (a.type() == typeid(const char*)) {          // true
    ...
}
if (a.type() == typeid(std::string)) {          // false
    ...
}
std::cout << std::any_cast<const char*>(a) << '\n';  // OK
std::cout << std::any_cast<std::string>(a) << '\n';  // EXCEPTION
```

These are more or less all the operations. No comparison operators are defined (which means that you cannot compare or sort objects), no hash function is defined, and no value() member functions are defined. Furthermore, because the type is only known at run time, no generic lambdas can be used to deal with the current value independently of its type. You always need the runtime function std::any_cast<> to be able to deal with the current value, which means that you need some type-specific code to reenter the C++ type system when dealing with values.

However, you can put std::any objects in a container. For example:

```
std::vector<std::any> v;

v.push_back(42);
std::string s = "hello";
v.push_back(s);

for (const auto& a : v) {
    if (auto pa = std::any_cast<const std::string>(&a); pa != nullptr) {
        std::cout << "string: " << *pa << '\n';
    }
    else if (auto pa = std::any_cast<const int>(&a); pa != nullptr) {
        std::cout << "int: " << *pa << '\n';
    }
}
```