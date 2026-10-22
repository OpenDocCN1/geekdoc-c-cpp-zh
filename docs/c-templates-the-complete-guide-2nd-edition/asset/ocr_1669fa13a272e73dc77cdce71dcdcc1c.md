```
is_base_of_v<int, int> // yields false (no class type)
```

# std:: is_convertible < FROM, TO >::value

+   - Yields true if expression of type FROM is convertible to type TO. Thus, the following must be valid:¹¹
+   
+   Click here to view code image
+   
+   ```
+   TO test() {
+   return std::declval<FROM>();
+   }
+   ```

+   - A reference on top of type FROM is only used to determine the value category of the expression being converted; the underlying type is then the type of the source expression.

+   - Note that is_constructible does not always imply is_convertible. For example: Click here to view code image
+   
+   ```
+   class C {
+   public:
+   explicit C(C const&); // no implicit copy constructor
+   ...};
+   is_constructible_v<C,C> // yields true
+   is_convertible_v<C,C> // yields false
+   ```

+   - Requires that the given types are either complete (see Section 10.3.1 on page 154), (cv-qualified) void, or arrays of unknown bound.

+   - Note that is_constructible (see Section D.3.2 on page 719) and is_assignable (see Section D.3.2 on page 721) have a different order for the source and destination types.

+   - See Section 19.5 on page 428 for implementation details.

# D.4 Type Construction

The traits listed in Table D.6 allow us to construct types from other types.

| Trait | Effect |
|---|---|
| remove_const<T> | Corresponding type without const |
| remove_volatile<T> | Corresponding type without volatile |
| remove_cv<T> | Corresponding type without const and |