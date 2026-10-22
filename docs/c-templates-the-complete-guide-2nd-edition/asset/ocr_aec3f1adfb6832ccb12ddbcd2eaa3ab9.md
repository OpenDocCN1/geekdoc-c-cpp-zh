function type that is qualified with const, volatile, &, and/or &&).

+   - To find out whether an rvalue of T would be swappable with another rvalue of T, use is_swappable_with<T&&, T&&>.
+   - Requires that the given type is a complete type (Section 10.3.1 on page 154), (cv-qualified) void, or an array of unknown bound.
+   - For example:

Click here to view code image

```
is_swappable_v<int> // yields true
is_swappable_v<int&> // yields true
is_swappable_v<int&&> // yields true
is_swappable_v<std::string&&> // yields true
is_swappable_v<void> // yields false
is_swappable_v<void*> // yields true
is_swappable_v<char[]> // yields false
is_swappable_v<std::unique_ptr<int>> // yields true
```

+   - Available since C++17.

# D.3.3 Relationships Between Types

Table D.5 lists the type traits that allow testing certain relationships between types. This includes checking which constructors and assignment operators are provided for class types.

| Trait | Effect |
|---|---|
| is_same<T1, T2> | T1 and T2 are the same types (including const/volatile qualifiers) |
| is_base_of<T, D> | Type T is base class of type D |
| is_convertible<T, T2> | Type T is convertible into type T2 |

Table D.5. Traits to Test Type Relationships

```
std:: is_same < T1, T2 > ::value
```

+   - Yields true if T1 and T2 name the same type including cv-qualifiers (const and volatile).
+   - Yields true if a type is a type alias of another.