+   - std::tuple_size<type>::value has to return the number of elements.
+   - std::tuple_element<idx,type>::type has to return the type of the idxth element.
+   - A global or member get<idx>() has to yield the value of the idxth element.

The standard library types std::pair<>, std::tuple<>, and std::array<> are examples of types that provide this API.

If structures or classes provide the tuple-like API, the API is used.

In all cases, the number of elements or data members has to match the number of names in the declaration of the structured binding. You cannot skip a name and you cannot use a name twice. However, you could use a very short name such as '_' (as some programmers prefer but others hate and which is not allowed in the global namespace), but this works only once within the same scope:

```
auto [_,val1] = getStruct(); // OK
auto [_,val2] = getStruct(); // ERROR: name _ already used
```

Nested or non-flat decomposition is not supported.

The next subsections will discuss all of these uses of structured bindings in detail.

# 1.2.1 Structures and Classes

The introductory examples of structured bindings in the sections above have already described some simple uses for structures and classes with public members. A typical application is the direct use of multiple return values returned in one data structure (e.g., see insert() for node handles). However, there are a few edge cases to be aware of.

Note that only limited use of inheritance is possible. All non-static data members must be members of the same class definition (thus, they must be direct members of the type or of the same unambiguous public base class):

```
struct B {
    int a = 1;
    int b = 2;
};

struct D1 : B {
};
auto [x, y] = D1{};      // OK

struct D2 : B {
    int c = 3;
};
auto [i, j, k] = D2{};   // compile-time ERROR
```

Note that you should use structured bindings on public members only if their order is guaranteed to be stable. Otherwise, if the order of int a and int b inside B changes, x and y suddenly are initialized with different values. To support this stability, C++17 defines the order of members for some standard library structures (e.g., insert_return_type).

Structured bindings for unions are not allowed.