```
is_lvalue_reference_v<int>    // yields false
is_lvalue_reference_v<int&>    // yields true
is_lvalue_reference_v<int&&>   // yields false
is_lvalue_reference_v<void>    // yields false
is_rvalue_reference_v<int>     // yields false
is_rvalue_reference_v<int&>    // yields false
is_rvalue_reference_v<int&&>   // yields true
is_rvalue_reference_v<void>    // yields false
```