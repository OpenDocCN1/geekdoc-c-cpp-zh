# D.5 OTHER TRAITS

Table D.2 lists all remaining traits here. There exist special properties or provide more complicated type transformations.

| Trait | Effect |
|---|---|
| `enable_if<B, T>` | Yields type `T` only if bool `B` is true |
| `conditional<B, T, F>` | Yields type `T` if bool `B` is true and type `F` otherwise |
| `common_type<Types...>` | Common type of all passed types |
| `aligned_storage<Len>` | Type of `Len` bytes with default alignment |
| `aligned_storage<Len, Align>` | Type of `Len` bytes aligned according to a divisor of `sizeof(Align)` |
| `aligned_union<Len, Types...>` | Type of `Len` bytes aligned for a union of `Types...` |

Table D.7: Other Type Traits

```
std::enable_if<cond, T>::type
```

+   - Yields `void` or `T` in its member type if `cond` is true. Otherwise, it does not define a member type.
+   - Because the type member is not defined when the condition is false, this trait can and is usually used to disable or SFINAE out a function template based on the given condition.
+   - See Section 6.9.2 on page 48 for details about a first example. See Section D.6 on page 735 for another example using parameter packs.
+   - See Section 20.2 on page 409 for details about how `std::enable_if` is implemented.

```
std::conditional<cond, T, F>::type
```

+   - Yields `T` if `cond` is true, and `F` otherwise.
+   - This is the standard version of the trait `std::conditional<>` introduced in Section 19.7.1 on page 440.
+   - Note that, unlike a normal C++ if-then-else statement, the template arguments for both the “then” and “else” branches are evaluated before the decision is made, so neither branch may contain ill-formed code or the program is likely to be ill-formed. As a consequence, you might have to add a level of indirection to avoid this issue. Section 19.7.1 on page 440 demonstrates this for the trait `isThen`, which has the same behavior.
+   - See Section 11.5 on page 17 for an example.

```
std::common_type<T...>::type
```

+   - Yields the “common type” of the given types `T1, ..., TN`.
+   - The computation of a common type is a little more complex than we want to cover in this appendix. Roughly speaking, the common type of two types `T` and `U` is the type produced by the conditional operator `?:` when its second and third operands are the types `T` and `U`, respectively. If both types are `void`, the common type is `void`. Otherwise, if either type is an lvalue reference, the common type is determined by the conditional operator. If the result is not valid, there is no common type. `decay_t` is applied to this result. The default computation may be overridden by user specialization of `std::common_type<T>` (in the C++ standard library, partial specialization exists for durations and time points).
+   - If no type is given or no common type exists, there is no `type` member defined, so that is an error when using it as an error (which might SFINAE out a function template).
+   - If a single type is given, the result is the application of `decay_t` to that type.
+   - For more than two types, `common_type` recursively replaces the first two types by their common type. If at any point that process fails, there is no common type.
+   - While processing the common type, the passed types are decayed types, so that the trait always yields a decayed type.
+   - See Section 13.3.3 on page 12 for a discussion and example of the application of this trait.
+   - The core of the primary template of this trait is usually implemented by mentioning the following line, here using only two parameters:

![](bbox=[0.08, 0.987, 0.73, 0.999])