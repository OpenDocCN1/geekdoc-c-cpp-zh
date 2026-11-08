
## Enumerators as Constants for Classes

The *enum class errc* is defined as in the following listing.

```cpp
enum class errc {
    address_family_not_supported,
    address_in_use,
    // ...
    value_too_large,
    wrong_protocol_type,
};
```

**Listing 28.37** Definition of “enum class errc”.

It seems that an *implicit conversion* of the errc element to an *error_condition* instance occurs when we then apply the comparison ec == errc::file_exists. Almost, but not quite: for the entire system to be extensible, the *error_category* of ec must somehow be taken into account. Because there are overlaps in error values, ec can mean one thing in file operation but something entirely different in memory operations. This is resolved through the *error_category* mechanism. In addition, errc here represents a set of constants for *error_condition*. But the library also supports the reverse way—that is, comparing an enum element representing an *error_code* with an *error_condition* instance.

Therefore, two steps are necessary for the equivalence check:

- 1. Decide whether errc represents an enum for specific error codes or generic error conditions.
- 2. Associate the value with an error_category.

For step 1, the is_error_code_enum and is_error_condition_enum *type traits* are used. By default, is_error_code_enum<E>::value and is_error_condition_enum<E>::value yield the value false. The standard library now specializes is_error_condition_enum and thus defines is_error_condition_enum<errc>::value == true.

```cpp
template <>
struct is_error_condition_enum<errc> : true_type {};
```

**Listing 28.38** Specialization of “is_error_condition_enum” for “errc”.

The implicit conversion can then take place through the templatization of the constructor of error_condition—that is, through template <class E> error_condition(E e).⁸ When we then write ec == errc::file_exists, the compiler chooses the bool operator==(const error_code& a, const error_condition& b) overload, because the constructor

⁸ E stands for the enum class, and the overload can only be found if is_error_condition_enum<errc>::value is true. The exact implementation is left to the library, but it is possible with standard template metaprogramming methods.

```cpp
}
}
int main() {
    std::error_code ec = mylib::run(667);
    if(!ec) {
        std::cout << "Great, it works!\n";
    } else if (ec == mylib::error_category(mylib::errc::OTHER_ERR)) {
        std::cout << "Another error\n";
    } else {
        std::cout << "Nothing happening here\n" << ec;
    }
}
```

Similarly, proceed to support the portable `error_category` as well.

## 28.5.6 “system_error” Exception

Library functions that prefer to propagate their errors as exceptions use the large aggregate exception class `system_error` from the header of the same name. This class again transports

- an `error_code`, consisting of an int detail and an `error_category`; and
- an error message.

This single exception can then be caught and examined in more detail. This is the alternative to many exception classes in a more or less arbitrary hierarchy—which may also differ on different systems and implementations.

For example, library code might look like this, attempting to join a thread:

```cpp
int osSpecificCode = pthread_detach(thread, 0);
if (osSpecificCode != 0)
    throw system_error(
        error_code(osSpecificCode, system_category()),
        "thread::detach failed");
```

You would handle this in user code like this:

```cpp
// https://godbolt.org/z/a8zP84j1x
#include <thread>
#include <iostream>
#include <system_error>
int main() {
    try {
        std::thread().detach(); // this will fail
    } catch(std::system_error& e) {
        std::cout
            << "system_error with code: " << e.code()
            << " message: " << e.what()
            << '\n';
    }
}
```

For me, this outputs the following:

`system_error with code:generic:22 message:Invalid argument`

Here, code contains the osSpecificCode.

In the standard library, there are already many places where a `system_error` can be thrown. You can handle them like this:

```cpp
// https://godbolt.org/z/cjh93oPcr
#include <iostream>
#include <system_error> // std::make_error_condition, std::io_errc
int main () {
    // switch to exceptions:
    std::cin.exceptions (std::ios::failbit|std::ios::badbit);
    try {
        std::cin.rdbuf(nullptr);        // triggers an exception
    } catch (std::ios::failure& e) {   // derived from system_error
        std::cerr << "Error: ";
        if (e.code() == std::make_error_condition(std::io_errc::stream)) {
            std::cerr << "stream\n";
        } else {
            std::cerr << "other\n";
        }
    }
}
```

So you catch the exception in a catch block. By comparing it with an `error_condition`, you can then check portable error conditions more precisely.

## 28.6 Runtime Type Information: “<typeinfo>” and “<typeindex>”

The `<typeinfo>` header actually contains only a few things:

- **Operator typeid()**  
  A function-like operator for determining a unique identification
- **Class type_info**  
  The return type of `typeid()`
- **Exceptions bad_cast and bad_typeid**  
  The exceptions that occur in the context of dynamic types

This is a little bit of a lie: `typeid()` is similar to `sizeof()` in that it is not a function but an operator, and `typeid` is even a keyword. However, you **must** include the `<typeinfo>` header before using `typeid()`; otherwise it is an error. Therefore, you can think of `typeid()` as a function defined in the header.

With this “function,” you can get information about a type that you specify as a parameter, which you can use for comparison purposes or, to a limited extent, for debugging.

The type can either be directly the name of a type or an expression. In the latter case, `typeid()` returns information about the type of the expression. However, the expression cannot include calculations like `a+b*c` or even method or function calls.

But what information does typeid return? Well, mainly a const& to a type_info instance; let's call it ti. The following things can be done with ti:

- **size_t ti.hash_code()**  
  Returns a hash value, for example, to quickly test for inequality.
- **const char* ti.name()**  
  Returns a textual representation of the type. However, this does not have a standardized format, nor must it be different for all types in a program, nor is it guaranteed that this text will always be the same for a given type. So, it is not very reliable, although informative, and is therefore mainly used for diagnostics.
- **type_index(ti)**  
  This important function from the `<typeindex>` header is the way to check the equality of two types based on their `type_info` references.

More important than what works is perhaps what **does not** work: You cannot create or copy a `type_info`, and you should not compare them with `==`. It is not guaranteed that two calls `ti1` and `ti2` of `typeid(A)` will return the same `type_info`—in fact, even `ti1 == ti2` is not guaranteed, although `operator==` is overloaded for `type_info`.

If you want to find out whether ti1 and ti2 represent the same type, do it like this:

`type_index(ti1) == type_index(ti2)`.

`type_index` can also be used as a key for map and similar, which is not possible with `type_info`. This allows you to build a mechanism with reliable type names, for example.

```cpp
// https://godbolt.org/z/dlG9ez4KW
#include <iostream>
#include <typeinfo>
#include <typeindex>
#include <map>
#include <string>

struct Base {
    virtual ~Base() {}
};
struct Derived_One : public Base {};
struct Derived_Two : public Base {};
int main() {
    using std::string; using std::cout; using std::type_index;
    std::map<std::type_index, string> names {
        { type_index(typeid(int)), "int" },
        { type_index(typeid(double)), "double" },
        { type_index(typeid(Base)), "Base" },
        { type_index(typeid(Derived_One)), "Derived_One" },
        { type_index(typeid(Derived_Two)), "Derived_Two" },
        { type_index(typeid(string)), "string" },
        { type_index(typeid(string::const_iterator)), "string" },
    };
    names[type_index(typeid(names))] = "names-map";
    int integer;
    double floating;
    Base base{};
    Base *one = new Derived_One{};
    Base *two = new Derived_Two{};
    // typeid.name() is implementation- and runtime-dependent:
    cout << typeid(integer).name() << '\n';   // On my system: i
    cout << typeid(floating).name() << '\n';  // On my system: d
    cout << typeid(base).name() << '\n';      // On my system: 4Base
    cout << typeid(*one).name() << '\n';      // On my system: 11Derived_One
    cout << typeid(*two).name() << '\n';      // On my system: 11Derived_Two
    cout << typeid(string).name() << '\n';    // For me: Ss
    cout << typeid(string("World").begin()).name() << '\n';
        // For me: N9__gnu_cxx17__normal_iteratorIPcSsEE
    cout << typeid(names).name() << '\n';
        // For me: St3mapISt10type_indexSsSt4lessIS0_ESaISt4pairIKS0_SsEEE
    cout << typeid(6/0).name() << '\n'; // Expression not executed! For me: i
    // type_index makes type_infos comparable:
    cout << names[type_index(typeid(integer))] << '\n';  // Output: int
    cout << names[type_index(typeid(floating))] << '\n'; // Output: double
    cout << names[type_index(typeid(base))] << '\n';     // Output: Base
    cout << names[type_index(typeid(*one))] << '\n';     // Output: Derived_One
    cout << names[type_index(typeid(*two))] << '\n';     // Output: Derived_Two
    cout << names[type_index(typeid(string))] << '\n';   // Output: string
    cout << names[type_index(typeid(names))] << '\n';    // Output: names-map
}
```

**Listing 28.41** Use “typeindex” for reliable type information.
