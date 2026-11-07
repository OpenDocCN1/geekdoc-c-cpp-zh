# ### 15.3.2 Move Semantics for std::optional<>

std::optional<> is a value type available since C++17 that extends the possible values of a *contained type* by the value “*there is no value*.” That avoids the need to mark one specific value of the type to have this semantics (such as the value 0 for pointers).

Optional objects also support move semantics. If you move the object as a whole, the state is copied and the contained object (if there is one) is moved. As a result, a moved-from object still has the same state but any value becomes unspecified.

However, you can also move a value into or out of the contained object. For example:

```
~~~cpp
std::optional<std::string> os;
std::string s = "a very very long string";
os = std::move(s);          // OK, moves
std::string s2 = *os;       // OK, copies
std::string s3 = std::move(*os);  // OK, moves
~~~
```

Note that after the last call, os still has a string value but as usual for moved-from objects, the value is unspecified. Thus, you can use it as long as you do not make any assumption about its value. You can even assign a new string value there.

Note also that some overloads ensure that temporary optionals are moved. Consider a function that returns an optional string:

```
~~~cpp
std::optional<std::string> func();
~~~
```

In this case, the following is well-defined to move the value:

```
~~~cpp
std::string s4 = func().value();  // OK, moves
std::string s5 = *func();         // OK, moves
~~~
```

This behavior is possible by using reference qualifiers that provide rvalue overloads for the corresponding member functions:

```
~~~cpp
namespace std {
  template<typename T>
  class optional {
    ...
    constexpr T& operator*() &;
    constexpr const T& operator*() const&;
    constexpr T&& operator*() &&;
    constexpr const T&& operator*() const&&;

    constexpr T& value() &;
    constexpr const T& value() const&;
    constexpr T&& value() &&;
    constexpr const T&& value() const&&;
  };
}
~~~
```

By using reference qualifiers, the class can return the moved value when the operation is called for rvalues (temporary objects or objects marked with std::move()):