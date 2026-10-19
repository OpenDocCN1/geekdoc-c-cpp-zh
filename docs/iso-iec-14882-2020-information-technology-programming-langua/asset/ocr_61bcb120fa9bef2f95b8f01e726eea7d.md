# ISO/IEC 14882:2020(E)

```
template<class T1, class T2>
    tuple(pair<T1, T2>) -> tuple<T1, T2>;
template<class Alloc, class... UTypes>
    tuple(allocator_arg_t, Alloc, UTypes...) -> tuple<UTypes...>;
template<class Alloc, class T1, class T2>
    tuple(allocator_arg_t, Alloc, pair<T1, T2>) -> tuple<T1, T2>;
template<class Alloc, class... UTypes>
    tuple(allocator_arg_t, Alloc, tuple<UTypes...>) -> tuple<UTypes...>;
}
```

# 20.5.3.1 Construction [tuple.cnstr]

1 In the descriptions that follow, let i be in the range [0, sizeof...(Types)) in order, Tᵢ be the iᵗʰ type in Types, and Uᵢ be the iᵗʰ type in a template parameter pack named UTypes, where indexing is zero-based.

2 For each tuple constructor, an exception is thrown only if the construction of one of the types in Types throws an exception.

3 The defaulted move and copy constructor, respectively, of tuple is a constexpr function if and only if all required element-wise initializations for move and copy, respectively, would satisfy the requirements for a constexpr function. The defaulted move and copy constructor of tuple<> are constexpr functions.

4 If is_trivially_destructible_v<Tᵢ> is true for all Tᵢ, then the destructor of tuple is trivial.

```
constexpr explicit(see below) tuple();
```

5 Constraints: is_default_constructible_v<Tᵢ> is true for all i.

6 Effects: Value-initializes each element.

7 Remarks: The expression inside explicit evaluates to true if and only if Tᵢ is not copy-list-initializable from an empty list for at least one i.

> [Note 1: This behavior can be implemented with a trait that checks whether a const Tᵢ& can be initialized with {}. — end note]

```
constexpr explicit(see below) tuple(const Types&...);
```

8 Constraints: sizeof...(Types) ≥ 1 and is_copy_constructible_v<Tᵢ> is true for all i.

9 Effects: Initializes each element with the value of the corresponding parameter.

10 Remarks: The expression inside explicit is equivalent to:
!conjunction_v<is_convertible<const Types&, Types>...>

```
template<class... UTypes> constexpr explicit(see below) tuple(UTypes&&... u);
```