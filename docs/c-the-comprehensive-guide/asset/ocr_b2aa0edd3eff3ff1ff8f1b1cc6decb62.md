# Enumerators as Constants for Classes

The *enum class errc* is defined as in the following listing.

```
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

+   1. Decide whether errc represents an enum for specific error codes or generic error conditions.
+   2. Associate the value with an error_category.

For step 1, the is_error_code_enum and is_error_condition_enum *type traits* are used. By default, is_error_code_enum<E>::value and is_error_condition_enum<E>::value yield the value false. The standard library now specializes is_error_condition_enum and thus defines is_error_condition_enum<errc>::value == true.

```
template <>
struct is_error_condition_enum<errc> : true_type {};
```

**Listing 28.38** Specialization of “is_error_condition_enum” for “errc”.

The implicit conversion can then take place through the templatization of the constructor of error_condition—that is, through template <class E> error_condition(E e).⁸ When we then write ec == errc::file_exists, the compiler chooses the bool operator==(const error_code& a, const error_condition& b) overload, because the constructor

⁸ E stands for the enum class, and the overload can only be found if is_error_condition_enum<errc>::value is true. The exact implementation is left to the library, but it is possible with standard template metaprogramming methods.