
`basics/specialmemtmpl1.cpp`

```cpp
#include <utility>
#include <string>
#include <iostream>

class Person
{
private:
    std::string name;
public:
    // constructor for passed initial name:
    explicit Person(std::string const& n) : name(n) {
        std::cout << "copying string-CONSTR for '" << name << "'\n";
    }
    explicit Person(std::string&& n) : name(std::move(n)) {
        std::cout << "moving string-CONSTR for '" << name << "'\n";
    }
    // copy and move constructor:
    Person(Person const& p) : name(p.name) {
        std::cout << "COPY-CONSTR Person '" << name << "'\n";
    }
    Person(Person&& p) : name(std::move(p.name)) {
        std::cout << "MOVE-CONSTR Person '" << name << "'\n";
    }
};

int main()
{
    std::string s = "sname";
    Person p1(s); // init with string object => calls copying string-CONSTR
    Person p2("tmp"); // init with string literal => calls moving string-CONSTR
    Person p3(p1); // copy Person => calls COPY-CONSTR
    Person p4(std::move(p1)); // move Person => calls MOVE-CONSTR
}
```

Here, we have a class `Person` with a string member `name` for which we provide initializing constructors. To support move semantics, we overload the constructor taking a `std::string`:

- We provide a version for string object the caller still needs, for which `name` is initialized by a copy of the passed argument:

```cpp
explicit Person(std::string const& n) : name(n) {
    std::cout << "copying string-CONSTR for '" << name << "'\n";
}
```

- We provide a version for movable string object, for which we call `std::move()` to “steal” the value from:

```cpp
explicit Person(std::string&& n) : name(std::move(n)) {
    std::cout << "moving string-CONSTR for '" << name << "'\n";
}
```

As expected, the first is called for passed string objects that are in use (lvalues), while the latter is called for movable objects (rvalues):

```cpp
std::string s = "sname";
Person p1(s); // init with string object => calls copying string-CONSTR
Person p2("tmp"); // init with string literal => calls moving string-CONSTR
```

Besides these constructors, the example has specific implementations for the copy and move constructor to see when a `Person` as a whole is copied/moved:

```cpp
Person p3(p1); // copy Person => calls COPY-CONSTR
Person p4(std::move(p1)); // move Person => calls MOVE-CONSTR
```

Now let’s replace the two string constructors with one generic constructor perfect forwarding the passed argument to the member `name`:

`basics/specialmemtmpl2.hpp`

```cpp
#include <utility>
#include <string>
#include <iostream>

class Person
{
private:
    std::string name;
public:
    // generic constructor for passed initial name:
    template<typename STR>
    explicit Person(STR&& n) : name(std::forward<STR>(n)) {
        std::cout << "TMPL-CONSTR for '" << name << "'\n";
    }

    // copy and move constructor:
    Person(Person const& p) : name(p.name) {
        std::cout << "COPY-CONSTR Person '" << name << "'\n";
    }
    Person(Person&& p) : name(std::move(p.name)) {
        std::cout << "MOVE-CONSTR Person '" << name << "'\n";
    }
};
```

Construction with passed string works fine, as expected:

```cpp
std::string s = "sname";
Person p1(s); // init with string object => calls TMPL-CONSTR
Person p2("tmp"); // init with string literal => calls TMPL-CONSTR
```

Note how the construction of `p2` does not create a temporary `string` in this case: The parameter `STR` is deduced to be of type `char const[4]`. Applying `std::forward<STR>` to the pointer parameter of the constructor has not much of an effect, and the `name` member is thus constructed from a null-terminated string.

But when we attempt to call the copy constructor, we get an error:

```cpp
Person p3(p1); // ERROR
```

while initializing a new `Person` by a movable object still works fine:

```cpp
Person p4(std::move(p1)); // OK: move Person => calls MOVE-CONSTR
```

Note that also copying a constant `Person` works fine:

```cpp
Person const p2c("ctmp"); // init constant object with string literal
Person p3c(p2c); // OK: copy constant Person => calls COPY-CONSTR
```

The problem is that, according to the overload resolution rules of C++ (see Section 16.2.4 on page 333), for a nonconstant lvalue `Person p` the member template

```cpp
template<typename STR>
Person(STR&& n)
```

is a better match than the (usually predefined) copy constructor:

```cpp
Person(Person const& p)
```

`STR` is just substituted with `Person&`, while for the copy constructor a conversion to `const` is necessary.

You might think about solving this by also providing a nonconstant copy constructor: `Person(Person& p)`. However, that is only a partial solution because for objects of a derived class, the member template is still a better match. What you really want is to disable the member template for the case that the passed argument is a `Person` or an expression that can be converted to a `Person`. This can be done by using `std::enable_if<>`, which is introduced in the next section.

## 6.3 Disable Templates with enable_if<>

Since C++11, the C++ standard library provides a helper template `std::enable_if<>` to ignore function templates under certain compile-time conditions.

For example, if a function template `foo<>` is defined as follows:

```cpp
template<typename T>
typename std::enable_if<(sizeof(T) > 4)>::type
foo() {
}
```

this definition of `foo<>` is ignored if `sizeof(T) > 4` yields false.[^4] If `sizeof(T) > 4` yields true, the function template instance expands to `void foo() { }`.

That is, `std::enable_if<>` is a type trait that evaluates a given compile-time expression passed as its (first) template argument and behaves as follows:

- If the expression yields `true`, its type member `type` yields a type:
  - The type is `void` if no second template argument is passed.
  - Otherwise, the type is the second template argument type.
- If the expression yields `false`, the member type is not defined. Due to a template feature called SFINAE (substitution failure is not an error), which is introduced later (see Section 8.4 on page 129), this has the effect that the function template with the `enable_if` expression is ignored.

As for all type traits yielding a type since C++14, there is a corresponding alias template `std::enable_if_t<>`, which allows you to skip `typename` and `::type` (see Section 2.8 on page 40 for details). Thus, since C++14 you can write

```cpp
template<typename T>
std::enable_if_t<(sizeof(T) > 4)>
foo() {
}
```

If a second argument is passed to `enable_if<>` or `enable_if_t<>`:

```cpp
template<typename T>
std::enable_if_t<(sizeof(T) > 4), T>
foo() {
    return T();
}
```

the `enable_if` construct expands to this second argument if the expression yields true. So, if `MyType` is the concrete type passed or deduced as `T`, whose size is larger than 4, the effect is `MyType foo();`.

Note that having the `enable_if` expression in the middle of a declaration is pretty clumsy. For this reason, the common way to use `std::enable_if<>` is to use an additional function template argument with a default value:

```cpp
template<typename T,
typename = std::enable_if_t<(sizeof(T) > 4)>>
void foo() {
}
```

which expands to

```cpp
template<typename T,
typename = void>
void foo() {
}
```

if `sizeof(T) > 4`.

If that is still too clumsy, and you want to make the requirement/constraint more explicit, you can define your own name for it using an alias template:[^5]

```cpp
template<typename T>
using EnableIfSizeGreater4 = std::enable_if_t<(sizeof(T) > 4)>;
```

```cpp
template<typename T,
typename = EnableIfSizeGreater4<T>>
void foo() {
}
```

See Section 20.3 on page 469 for a discussion of how `std::enable_if` is implemented.

## 6.4 Using enable_if<>

We can use `enable_if<>` to solve our problem with the constructor template introduced in Section 6.2 on page 95.

The problem we have to solve is to disable the declaration of the template constructor
