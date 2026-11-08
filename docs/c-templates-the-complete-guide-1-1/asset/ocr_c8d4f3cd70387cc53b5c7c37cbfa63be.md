Instead, we may prefer to use std::decay<>, which, however, also removes array and function types to corresponding pointer types (see Section 5.4 on page 115).

Click here to view code image

```
```
decay_t<const T>            // yields int
decay_t<const T&>           // yields int
```
```

+   - See Section 9.3.2 on page 696 for implementation details.

```
```
std::add_const_t<T> // T type
std::add_volatile_t<T> // T type
std::add_cv_t<T> // T type
```
```

+   - The type of the const/volatile qualifiers added at the top level.
+   - Applying one of these traits to a reference type or a function type has no effect. For example:

Click here to view code image

```
```
std::add_const_t<int>       // yields int const
volatile int
std::add_const_t<volatile int> // yields int const volatile
std::add_const_t<int const> // yields int const
std::add_const_t<int&>      // yields int&
std::add_const_t<int&&>     // yields int&&
std::add_const_t<int*>      // yields int* const
```
```

+   - Yields the corresponding signed/unsigned type of T.
+   - Requires that T is an enumeration type or a (cv-qualified) integral type other than bool. All other types lead to undefined behavior (see Section 9.3 on page 696) for a discussion about how to avoid such undefined behavior.
+   - Applying one of these traits to a reference type or a function type has no effect; otherwise, a pointer is passed as a reference to a T const and is not qualified for example:

Click here to view code image

```
```
std::make_signed<char>        // yields signed char
char
std::make_unsigned<char>      // yields unsigned char
std::make_unsigned<char const> // yields unsigned char
```
```

+   - Yields the type the reference type T refers to (or T itself if it is not a reference type).
+   - For example:

Click here to view code image

```
```
remove_reference<int>        // yields int
remove_reference<int&>       // yields int
remove_reference<int&&>      // yields int
remove_reference<int const&> // yields int const
remove_reference<int const&&> // yields int const
```
```

+   - Note that a reference type itself is not a type. For this reason, the member apply const int? traits traits.

Click here to view code image

```
```
remove_const_remove_reference<int const&> // yields int
remove_reference_remove_const<int const&> // yields int
```
```

Instead, we may prefer to use std::decay<>, which, however, also removes array and function types to corresponding pointer types (see Section 5.4 on page 115).

Click here to view code image

```
```
decay_t<const T>            // yields int
decay_t<const T&>           // yields int
```
```