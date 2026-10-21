
Initializations and assignments always use the best match to find the new alternative. If the type does not fit exactly, there might be surprises.

Note that empty variants, variants with reference members, variants with C-style array members, and variants with incomplete types (such as void) are not allowed.³

There is no empty state. This means that for each constructed object, at least one constructor has to be called. The default constructor initializes the first type with the default constructor:

```
std::variant<std::string, int> var;        // => var.index() == 0, value == ""
```

If there is no default constructor defined for the first type, calling the default constructor for the variant is a compile-time error:

```
struct NoDefConstr {
    NoDefConstr(int i) {
        std::cout << "NoDefConstr::NoDefConstr(int) called\n";
    }
};
```

```
std::variant<NoDefConstr, int> v1;    // ERROR: can't default construct first type
```

The auxiliary type std::monostate provides the ability to deal with this situation and also provides the ability to simulate an empty state.

## std::monostate

To support variants where the first type has no default constructor, the C++ standard library provides a special helper type: std::monostate. Objects of type std::monostate always have the same state. Thus, they always compare to be equal. Their own purpose is to represent an alternative type so that the variant has no value of any other type.

That is, the struct std::monostate can serve as a first alternative type to make the variant type default constructible. For example:

```
std::variant<std::monostate, NoDefConstr, int> v2;    // OK
std::cout << "index: " << v2.index() << '\n';          // prints 0
```

To some extent, you can interpret the state to signal emptiness.⁴

There are various ways to check for the monostate, which also demonstrates some of the other operations you can call for variants:

```
if (v2.index() == 0) {
    std::cout << "has monostate\n";
}
if (!v2.index()) {
    std::cout << "has monostate\n";
}
if (std::holds_alternative<std::monostate>(v2)) {
```

³ These features might be added later, but for C++17, there was not enough experience to support it.

⁴ In principle, std::monostate can serve as any alternative, not just the first one. However, this alternative does not help to make the variant default constructible.

```
std::cout << "has monostate\n";
}
if (std::get_if<0>(&v2)) {
    std::cout << "has monostate\n";
}
if (std::get_if<std::monostate>(&v2)) {
    std::cout << "has monostate\n";
}
```

get_if<>() uses a pointer to a variant and returns a pointer to the current alternative if the current alternative is T. Otherwise it returns nullptr. This differs from get<T>(), which takes a reference to a variant and returns the current alternative by value if the provided type is correct, but throws in all other cases.

As usual, you can assign a value of another alternative and even assign the monostate, signaling emptiness again:

```
v2 = 42;
std::cout << "index: " << v2.index() << '\n';  // index: 1

v2 = std::monostate{};
std::cout << "index: " << v2.index() << '\n';  // index: 0
```

## Deriving From Variants

You can derive from a variant. For example, you can define an aggregate that derives from a std::variant<> as follows:

```
class Derived : public std::variant<int, std::string> {
};
```

```
Derived d = {{"hello"}};
std::cout << d.index() << '\n';      // prints: 1
std::cout << std::get<1>(d) << '\n'; // prints: hello
d.emplace<0>(77);                  // initializes int, destroys string
std::cout << std::get<0>(d) << '\n'; // prints: 77
```

## 16.3 std::variant<> Types and Operations

This section describes the types and operations of std::variant<> in detail.

### 16.3.1 std::variant<> Types

In the header file <variant>, the C++ standard library defines class std::variant<> as follows:

```
namespace std {
    template<typename Types...> class variant;
}
```

That is, std::variant<> is a variadic class template (a feature introduced with C++11 that allows you to deal with an arbitrary number of types).

In addition, the following types and objects are defined:

- Class template std::variant_size
- Class template std::variant_alternative
- Value std::variant_npos
- Type std::monostate
- Exception class std::bad_variant_access, derived from std::exception.

Variants also use the two variable templates std::in_place_type<> and std::in_place_index<>, which have their own types std::in_place_type_t and std::in_place_index_t and are defined in the header file <utility>.

### 16.3.2 std::variant<> Operations

Table std::variant Operations lists all operations that are provided for std::variant<>.

| Operation | Effect |
|---|---|
| constructors | Creates a variant object (might call constructor for underlying type) |
| destructor | Destroys a variant object |
| = | Assigns a new value |
| emplace<T>() | Destroys the old value and assigns a new value to the alternative with type T |
| emplace<Idx>() | Destroys the old value and assigns a new value to the alternative with index Idx |
| valueless_by_exception() | Returns whether the variant has no value due to an exception |
| index() | Returns the index of the current alternative |
| swap() | Swaps values between two objects |
| ==, !=, <, <=, >, >= | Compares variant objects |
| hash<> | Function object type for computing hash values |
| holds_alternative<T>() | Returns whether there is a value for type T |
| get<T>() | Returns the value for the alternative with type T |
| get<Idx>() | Returns the value for the alternative with index Idx |
| get_if<T>() | Returns a pointer to the value for the alternative with type T or nullptr |
| get_if<Idx>() | Returns a pointer to the value for the alternative with index Idx or nullptr |
| visit() | Performs an operation for the current alternative |

Table 16.1. std::variant<> Operations

## Construction

By default, the default constructor of a variant calls the default constructor of the first alternative:

```
std::variant<int, int, std::string> v1;  // sets first int to 0, index()=0
```

The alternative is value initialized, which means that it is 0, false, or nullptr for fundamental types.

If a value is passed for initialization, the best matching type is used:

```
std::variant<long, int> v2{42};
std::cout << v2.index() << '\n';  // prints 1
```

However, the call is ambiguous if two types match equally well:

```
std::variant<long, long> v3{42};          // ERROR: ambiguous
std::variant<int, float> v4{42.3};        // ERROR: ambiguous
std::variant<int, double> v5{42.3};       // OK
std::variant<int, long double> v6{42.3};  // ERROR: ambiguous
```

```
std::variant<std::string, std::string_view> v7{"hello"}; // ERROR: ambiguous
std::variant<std::string, std::string_view, const char*> v8{"hello"}; // OK
std::cout << v8.index() << '\n';  // prints 2
```

To pass more than one value for initialization, you have to use the in_place_type or in_place_index tags:

```
std::variant<std::complex<double>> v9{3.0, 4.0};      // ERROR
std::variant<std::complex<double>> v10{{3.0, 4.0}};  // ERROR
std::variant<std::complex<double>> v11{std::in_place_type<std::complex<double>>, 3.0, 4.0};
std::variant<std::complex<double>> v12{std::in_place_index<0>, 3.0, 4.0};
```

You can also use the in_place_index tags to resolve ambiguities or overrule priorities during the initialization:

```
std::variant<int, int> v13{std::in_place_index<1>, 77};  // init 2nd int
std::variant<int, long> v14{std::in_place_index<1>, 77};  // init long, not int
std::cout << v14.index() << '\n';  // prints 1
```

You can even pass an initializer list followed by additional arguments:

```
// initialize variant with a set with lambda as sorting criterion:
auto sc = [] (int x, int y) {
    return std::abs(x) < std::abs(y);
};
std::variant<std::vector<int>, std::set<int,decltype(sc)>> v15{std::in_place_index<1>, {4, 8, -7, -2, 0, 5}, sc};
```

However, this works only if all initial values match the element type of the container exactly. Otherwise you have to explicitly pass a std::initializer_list<>:

```
// initialize variant with a set with lambda as sorting criterion:
```
