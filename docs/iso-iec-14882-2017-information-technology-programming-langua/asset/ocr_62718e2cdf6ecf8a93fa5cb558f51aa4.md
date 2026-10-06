# ISO/IEC 14882:2017(E)

Remarks: This operator shall not participate in overload resolution sizeof...((Types) == 2 and is_assignable_v<T0, U1> is true for the first type T0 in Types and is_assignable_v<T1, U2&&> is true for the second type T1 in Types.

Returns: *this.

# 23.5.3.3 swap [tuple.swap]

```
void swap(tuple<rhs> noexcept(...)
```

+   1. Each element in *this shall be swappable with (20.5.3.2) the corresponding element in rhs.

+   2. Effects: Swap for each element in *this and its corresponding element in rhs.

+   3. Remarks: The expression inside noexcept is equivalent to the logical AND of the following expressions: is_not_swappable_v<T>,

where Ti is the i-th type in Types.

+   4. Throws: Unless one of the element-wise swap calls throws an exception.

# 23.5.3.4 Tuple function creations [tuple.creation]

+   1. In the function descriptions that, the members of a parameter XTypes are denoted by Xi, for i in [0, sizeof...(XTypes)], where indexing is zero-based.

```
template<class TTypes>
constexpr tuple<TTypes...> make_tuple(TTypes&&... t);
```

+   2. The pack VTypes is defined as follows. Let Ui, decay_t<Ti> for each Ti, in Types. If Ui is a specialization of reference_wrapper, then Vi in VTypes is Ui::type; otherwise Vi is Ui.

+   3. Returns tuple<TTypes...>(std::forward<T>(t)...).

+   4. [Example:

```
int; float;
make_tuple(1, ref(i), ref(j))
creates a tuple<int, float&, float>& -- end example
```

```
template<class TTypes>
constexpr tuple<TTypes...> forward_as_tuple(TTypes&&... t) noexcept;
```

+   5. Effects: Constructs a tuple of references to the arguments in t suitable variables, a program shall ensure that the return value of this function does not outline any of its arguments (e.g., the program should not return the tuple in a named function).

+   6. Returns tuple<TTypes...>(std::forward<TTypes>(t)).

```
template<class TTypes>
constexpr tuple(TTypes&&... t) noexcept;
```

+   7. Returns tuple<TTypes...>(t). (no...). When an argument t is ignore, assigning any value to the corresponding tuple element has effect

+   8. [Example: tie one to create tuples that unpack tuples into variables. ignore can be used for elements that are not needed:

```
int; std::string s;
tie(i, ignore, s) = make_tuple(4, 3.14, "C++");
// i == 42, s = "C++"
// end example
```

§ 23.5.3.4 ©ISO/IEC 2017 - All rights reserved 548