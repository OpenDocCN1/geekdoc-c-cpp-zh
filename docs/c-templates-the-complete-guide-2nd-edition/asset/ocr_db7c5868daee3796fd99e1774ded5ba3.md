```
is_copy_constructible_v<int>                  // yields true
is_copy_constructible_v<void>                 // yields false
is_copy_constructible_v<std::unique_ptr<int>> // yields false
is_copy_constructible_v<std::string>          // yields true
is_copy_constructible_v<std::string&>         // yields true
is_copy_constructible_v<std::string&&>        // yields false
// in contrast to:
is_constructible_v<std::string,std::string>   // yields true
is_constructible_v<std::string&,std::string&> // yields true
is_constructible_v<std::string&&,std::string&&> // yields true
```