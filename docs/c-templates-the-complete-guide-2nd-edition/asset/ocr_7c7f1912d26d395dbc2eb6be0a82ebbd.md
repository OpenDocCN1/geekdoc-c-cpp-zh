```
is_assignable_v<std::string&&, std::string&&> // yields true
```

# std:: **is_copy_assignable** < T >::value
std:: **is_trivially_copy_assignable** < T >::value
std:: **is_nothrow_copy_assignable** < T >::value

+   • Yields true if a value of type T can be (copy-)assigned to an object of type T (without using a nontrivial operation or with the guarantee that no exception is thrown).
+   
+   • Yields `false` if T is not a *referenceable type* (either (cv-qualified) `void` or a function type that is qualified with `const`, `volatile`, `&`, and/or `&&`).
+   
+   • Provided T is a referenceable type, same as `is_assignable<T&, T const&>::value`, `is_trivially_assignable<T&, T const&>::value`, or `is_nothrow_assignable<T&, T const&>::value` respectively.
+   
+   • To find out whether an rvalue of type T can be copy assigned to another rvalue of type T, use `is_assignable<T&&, T&&>`, and so on.
+   
+   • Note that `void`, built-in array types, and classes with deleted copy-assignment operator cannot be copy-assigned.
+   
+   • Requires that the given type is either complete (see Section 10.3.1 on page 154), (cv-qualified) `void`, or an array of unknown bound.
+   
+   • For example:

[Click here to view code image](#)

```
is_copy_assignable_v<int> // yields true
is_copy_assignable_v<int&> // yields true
is_copy_assignable_v<int&&> // yields true
is_copy_assignable_v<void> // yields false
is_copy_assignable_v<void*> // yields true
is_copy_assignable_v<char[]> // yields false
is_copy_assignable_v<std::string> // yields true
is_copy_assignable_v<std::unique_ptr<int>> // yields false
```

# std:: **is_move_assignable** < T >::value
std:: **is_trivially_move_assignable** < T >::value
std:: **is_nothrow_move_assignable** < T >::value

+   • Yields true if an rvalue of type T can be move-assigned to an object of type T (without using a nontrivial operation or with the guarantee that no exception is thrown).
+   
+   • Yields `false` if T is not a *referenceable type* (either (cv-qualified) `void` or a