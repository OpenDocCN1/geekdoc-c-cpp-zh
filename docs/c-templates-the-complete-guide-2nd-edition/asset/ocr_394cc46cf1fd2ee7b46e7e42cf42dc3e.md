```
```cpp
add_cv_t<int>                  // yields int const volatile
add_cv_t<int const>             // yields int const volatile
add_cv_t<int const volatile>    // yields int const volatile
add_const_t<int>                // yields int const
add_const_t<int const>           // yields int const
add_const_t<int&>                // yields int&
```
```