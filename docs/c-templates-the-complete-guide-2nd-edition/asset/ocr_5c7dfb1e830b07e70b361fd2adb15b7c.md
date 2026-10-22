```
template<char const* name>
class MyClass {
    ...
};

MyClass<"hello"> x;  // ERROR: string literal "hello" not allowed
```