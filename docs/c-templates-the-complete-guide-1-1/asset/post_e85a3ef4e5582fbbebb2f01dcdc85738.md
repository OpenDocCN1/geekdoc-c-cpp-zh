
```cpp
#include <utility>
#include <iostream>

class X {
    ...
};

void g (X) {
    std::cout << "g() for val\n";
}

void g (X const&) {
    std::cout << "g() for const\n";
}

void g (X&&) {
    std::cout << "g() for movable object\n";
}

// let f() perfect forward argument val to g()

template<typename T>
void f (T&& val)
{
    g(std::forward<T>(val));  // call the right g()
}

int main()
{
    X v;              // create variable

    X const c;        // create constant

    f(v);             // f() for variable calls f(X&)
    f(c);             // f() for constant calls f(X const&)
    f(X());           // f() for temporary calls f(X&&)
    f(std::move(v));  // f() for non-const movable variable
}
```

Of course, perfect forwarding can also be used with variadic templates (see Section 4.3 on page 6 for some examples). See Section 15.6.3 on page 336 for details of perfect forwarding.

## 6.2 SPECIAL MEMBER FUNCTION TEMPLATES

Member function templates can also be used as special member functions, including as a constructor, which, however, might lead to surprising behavior.

Consider the following example:

Click here to view code image

```cpp
#include <utility>
#include <string>
#include <iostream>

class Person
{
private:
    std::string name;

public:
    // constructor for passed initial name
    explicit Person(std::string const& n) : name(n) {
        std::cout << "COPYING string-CONSTR for " << ...
    }

    explicit Person(std::string&& n) : name(std::move(n)) {
        std::cout << "MOVING string-CONSTR for " << ...
    }

    // copy and move constructors:
    Person(Person const& p) : name(p.name) {
        std::cout << "COPY-CONSTR Person " << name << ...
    }

    Person(Person&& p) : name(std::move(p.name)) {
        std::cout << "MOVE-CONSTR Person " << name << ...
    }
};
```

Here, we have a class Person with a string member name for which we provide initializing constructors. To support move semantics, we overload the constructor taking a std::string:

- We provide a version for string object, for which name is initialized by a copy of the passed argument:

Click here to view code image

```cpp
Person(std::string const& n) : name(n) {
    std::cout << "COPY-CONSTR for " << name << ...
}
```

- We provide a version for movable string object, for which we call std::move() to "steal" the value from:

Click here to view code image

```cpp
Person(std::string&& n) : name(std::move(n)) {
    std::cout << "MOVE-CONSTR for " << name << ...
}
```

As expected, the first is called for passed string objects that are in use (lvalues), while the latter is called for movable objects (rvalues):

Click here to view code image

```cpp
std::string s = "name";      // init with string object => call copying string-constr
Person p2("tmp");             // init with string literal => call moving string-CONSTR
```

Besides these constructors, the example has specific implementations for copy and move constructor to see when a Person as a whole is copied/moved:

Click here to view code image

```cpp
Person p3(p1);                // copy Person => calls COPY-CONSTR
Person p4(std::move(p1));     // move Person => calls MOVE-CONSTR
```

Now let's replace the two string constructors with one generic constructor perfect-forwarding the passed argument to the member name:

Click here to view code image

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
    template<typename T>
    explicit Person(T&& n) : name(std::forward<T>(n))
    {
        std::cout << "TMPL-CONSTR for '" << name << "'\n";
    }

    // copy and move constructor:
    Person (Person const& p) : name(p.name) {
        std::cout << "COPY-CONSTR Person '" << name << "'\n";
    }
    Person (Person&& p) : name(std::move(p.name)) {
        std::cout << "MOVE-CONSTR Person '" << name << "'\n";
    }
};
```

Construction with passed string works fine, as expected:

Click here to view code image

```cpp
std::string s = "Nancy";
Person p1(s);              // init with string object => calls TMPL-CONSTR
Person p2("tmp");          // init with string literal => calls TMPL-CONSTR
```

Note how the construction of p2 does not create a temporary string in this case. The parameter T&& is a forwarding reference (see Section 6.1). Applying std::forward<T>() to the passed parameter in the constructor has no effect of any kind, and the name member is thus constructed from an lvalue and moved from.

But when we attempt to call the copy constructor, we get an error:

Click here to view code image

```cpp
Person p3(p1);              // ERROR
```

While initializing a new Person by a nonconstant object still works fine:

Click here to view code image

```cpp
Person p4(std::move(p1));   // OK: move Person => calls MOVE-CONSTR
```

Note that also copying a constant Person works fine:

Click here to view code image

```cpp
Person const cp("tmp");     // init constant object with string literal
Person p5(cp);              // OK: copy constant Person => calls COPY-CONSTR
```

The problem is that, according to the overload resolution rules of C++ (see Section 16.2.5 on page 333), for a nonconstant lvalue Person p, the template constructor

Click here to view code image

```cpp
template<typename T>
Person(T&& n)
```

is a better match than the (usually predefined) copy constructor:

Click here to view code image

```cpp
Person (Person const& p)
```

For an rvalue, the template constructor is a better match than the (usually predefined) move constructor:

Click here to view code image

```cpp
Person (Person&& p)
```

You might think about avoiding this by also providing a nonconstant copy constructor:

Click here to view code image

```cpp
Person (Person& p)
```

However, this is only a partial solution because for objects of a derived class, the template constructor is a better match. What you really want is to disable the template member for the case that the passed argument is a Person or an expression that can be converted to a Person. This can be done only using std::enable_if<>, which is introduced in the next section.

## 6.3 DISABLE TEMPLATES WITH ENABLE_IF<>

type convertible to std::string;

For this, we use a more standard type trait, `std::is_convertible`. In C++20, with C++17, the corresponding definition looks as follows:

Click here to view code image

```cpp
template<typename T>
using EnableIfString =
    std::enable_if_t<
        std::is_convertible_v<T,
            std::string>>;

template<typename T>
Person(T&& n);
```

If T is convertible to std::string, the whole declaration expands to

Click here to view code image

```cpp
template<typename T>
Person(T&& n)
    : name(std::forward<T>(n))
{
    static_assert(
        std::is_convertible_v<T,
            std::string>);
}
```

If T is not convertible to std::string, the whole function template is ignored.

Again, we can define our own name for the constraint by using an alias template:

Click here to view code image

```cpp
template<typename T>
using EnableIfString =
    std::enable_if_t<
        std::is_convertible_v<T,
            std::string>>;

template<typename T,
    typename = EnableIfString<T>>
Person(T&& n);
```

Thus, the whole class Person should look as follows:

Click here to view code image

```cpp
#include <utility>

#include <string>

#include <iostream>

#include <type_traits>

template<typename T>
using EnableIfString = std::enable_if_t<
    std::is_convertible_v<T, std::string>>;

class Person
{
private:
    std::string name;

public:
    // generic constructor for passed initial name:
    template<typename STR, typename = EnableIfString<STR>>
    explicit Person(STR&& n)
        : name(std::forward<STR>(n)) {
        std::cout << "TMPL-CONSTR for '" << n << "'\n";
    }

    // copy and move constructor:
    Person (Person const& p) : name(p.name) {
        std::cout << "COPY-CONSTR Person '" << p.name << "'\n";
    }
    Person (Person&& p) : name(std::move(p.name)) {
        std::cout << "MOVE-CONSTR Person '" << p.name << "'\n";
    }
};
```

Now, all calls behave as expected:
