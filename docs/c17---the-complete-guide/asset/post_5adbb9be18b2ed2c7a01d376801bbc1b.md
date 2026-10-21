
```
template<> decltype(auto) get<0>(Customer&& c) {
    return std::move(c.firstname()); }
template<> decltype(auto) get<1>(const Customer& c) { return c.lastname(); }
template<> decltype(auto) get<1>(Customer& c) { return c.lastname(); }
...
```

Again, note that the primary function template declaration and the full specializations must have the same signature (including the same return type). The following will not compile:

```
template<std::size_t> decltype(auto) get(Customer& c);
template<> std::string& get<0>(Customer& c) { return c.firstname(); }
template<> std::string& get<1>(Customer& c) { return c.lastname(); }
template<> long& get<2>(Customer& c) { return c.value(); }
```

You can now use structured bindings for read access and to modify the members of a Customer:

lang/structbind2.cpp

```
#include "structbind2.hpp"
#include <iostream>

int main()
{
    Customer c{"Tim", "Starr", 42};
    auto [f, l, v] = c;
    std::cout << "f/l/v:    " << f << ' ' << l << ' ' << v << '\n';

    // modify structured bindings via references:
    auto&& [f2, l2, v2] = c;
    std::string s{std::move(f2)};
    f2 = "Ringo";
    v2 += 10;
    std::cout << "f2/l2/v2: " << f2 << ' ' << l2 << ' ' << v2 << '\n';
    std::cout << "c:        " << c.firstname() << ' '
              << c.lastname() << ' ' << c.value() << '\n';
    std::cout << "s:        " << s << '\n';
}
```

The program has the following output:

```
f/l/v:      Tim Starr 42
f2/l2/v2: Ringo Starr 52
c:          Ringo Starr 52
s:          Tim
```

### 1.4 Afternotes

Structured bindings were first proposed by Herb Sutter, Bjarne Stroustrup, and Gabriel Dos Reis in http://wg21.link/p0144r0 by using curly braces instead of square brackets. The finally accepted wording for this feature was formulated by Jens Maurer in http://wg21.link/p0217r3.

## Chapter 2: if and switch with Initialization

The if and switch control structures now allow us to specify an initialization clause before the usual condition or selection clause.

For example, you can write:

```
if (status s = check(); s != status::success) {
    return s;
}
```

where the initialization

```
status s = check();
```

initializes s, which is then valid for the whole if statement (including the optional else part).

### 2.1 if with Initialization

Any value initialized inside an if statement is valid until the end of the then and the else part (if this part exists). For example:

```
if (std::ofstream strm = getLogStrm(); coll.empty()) {
    strm << "<no data>\n";
}
else {
    for (const auto& elem : coll) {
        strm << elem << '\n';
    }
}
// strm no longer declared
```

The destructor for strm is called at the end of the whole if statement (at the end of the else part, if any, or at the end of the then part, otherwise).

Another example would be the use of a lock while performing some tasks depending on a condition:

```
if (std::lock_guard<std::mutex> lg{collMutex}; !coll.empty()) {
    std::cout << coll.front() << '\n';
}
```

which, due to class template argument deduction, can now also be written as:

```
if (std::lock_guard lg{collMutex}; !coll.empty()) {
    std::cout << coll.front() << '\n';
}
```

In any case, this code is equivalent to:

```
{
    std::lock_guard<std::mutex> lg{collMutex};
    if (!coll.empty()) {
        std::cout << coll.front() << '\n';
    }
}
```

with the minor difference that lg is defined in the scope of the if statement so that the condition is in the same scope (declarative region).

Note that this feature works in the same way as the initialization statement of a traditional for loop. For the guard to be effective, the initializer needs to declare a variable with a name. Otherwise, the initialization itself is an expression that creates and immediately destroys a temporary object. As a consequence, initializing a lock guard without a name is a logical error, because the guard would no longer lock when the condition is checked:

```
if (std::lock_guard<std::mutex>{collMutex}; // runtime ERROR:
    !coll.empty()) {                 // - no longer locked
    std::cout << coll.front() << '\n'; // - no longer locked
}
```

In principle, a single _ as a name would be enough (as some programmers prefer but others hate and which is not allowed in the global namespace):

```
if (std::lock_guard<std::mutex> _{collMutex}; // OK, but...
    !coll.empty()) {
    std::cout << coll.front() << '\n';
}
```

You can have multiple declarations with optional initializations:

```
if (auto x = qqq1(), y = qqq2(); x != y) {
    std::cout << "return values " << x << " and " << y << " differ\n";
}
```

or:

```
if (auto x{qqq1()}, y{qqq2()}; x != y) {
    std::cout << "return values " << x << " and " << y << " differ\n";
}
```

As another example, consider inserting a new element into a map or unordered map. You can check whether this was successful as follows:

```
std::map<std::string, int> coll;
...
if (auto [pos,ok] = coll.insert({"new",42}); !ok) {
    // if insert failed, handle error using iterator pos:
    const auto& [key,val] = *pos;
    std::cout << "already there: " << key << '\n';
}
```

Here, we also use structured bindings to give both the return value and the element at the return position pos useful names instead of just first and second. Before C++17, the corresponding check had to be formulated as follows:

```
auto ret = coll.insert({"new",42});
if (!ret.second){
    // if insert failed, handle error using iterator ret.first
    const auto& elem = *(ret.first);
    std::cout << "already there: " << elem.first << '\n';
}
```

Note that the extension also applies to the new compile-time if feature.

### 2.2 switch with Initialization

Using the switch statement with an initialization allows us to initialize an object/entity for the scope of the switch before formulating the condition to decide where to continue the control flow.

For example, we can initialize a filesystem path before we deal with its category:

```
namespace fs = std::filesystem;
...
switch (fs::path p{name}; status(p).type()) {
    case fs::file_type::not_found:
        std::cout << p << " not found\n";
        break;
    case fs::file_type::directory:
        std::cout << p << ":\n";
        for (const auto& e : std::filesystem::directory_iterator{p}) {
            std::cout << "- " << e.path() << '\n';
        }
        break;
    default:
        std::cout << p << " exists\n";
        break;
}
```

Here, the initialized path p can be used throughout the whole switch statement.

### 2.3 Afternotes

if and switch with initialization was first proposed by Thomas Köppe in http://wg21.link/p0305r0, initially extending only the if statement. The finally accepted wording was formulated by Thomas Köppe in http://wg21.link/p0305r1.

## Chapter 3: Inline Variables

For portability and ease of integration, it often makes sense to provide classes and libraries that are entirely contained in header files. However, up to C++17, this was only possible if no global variables/objects were needed or provided by such a library.

Since C++17, you can define a variable/object in a header file as inline:

```
class MyClass {
    inline static std::string msg{"OK"};  // OK since C++17
    ...
};
```

```
inline MyClass myGlobalObj;  // OK even if included/defined by multiple CPP files
```

No further definition in one translation unit is necessary, and if this definition is used by multiple translation units, they all refer to the same unique object.

### 3.1 Motivation for Inline Variables

In C++, initializing a non-const static member inside the class structure is not allowed:

```
class MyClass {
    static std::string msg{"OK"};  // compile-time ERROR
    ...
};
```

Defining the variable outside the class structure is also an error if this definition is part of a header file included by multiple CPP files:

```
class MyClass {
    static std::string msg;
    ...
};
std::string MyClass::msg{"OK"};  // Link ERROR if included by multiple CPP files
```
