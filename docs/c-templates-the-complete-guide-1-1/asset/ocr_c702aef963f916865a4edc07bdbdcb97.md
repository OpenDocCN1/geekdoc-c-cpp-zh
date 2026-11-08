page 154, (cv-qualified) void, or arrays of unknown bound.

+   - For example:

Click here to view code image

```
is_constructible_v<int>                         //
true                                             //
is_constructible_v<const int>                   //
true                                             //
is_constructible_v<long,int>                    //
true                                             //
is_constructible_v<long[],int>                 //
false                                            //
is_constructible_v<void*>                       //
false                                            //
is_constructible_v<const char*,std::string>     //
false                                            //
is_constructible_v<char*,std::string>           //
true
```

+   - Note that `is_constructible` has a different order for the source and destination types.

```
std::is_default_constructible<T>::value
std::is_trivially_default_constructible<T>::value
std::is_nothrow_default_constructible<T>::value
```

+   - Yields `true` if an object of type `T` can be initialized without any argument for initialization (without using a nontrivial operation or with the guarantee that no exception is thrown).

+   - Same as `is_constructible<T>`, `is_trivially_constructible<T>`, or `is_nothrow_constructible<T>`, respectively.

+   - A true value implies that the object can be destroyed accordingly (i.e., `is_trivially_destructible<T>` or `is_nothrow_destructible<T>::value`).

+   - Requires that the given type is either complete (see Section 30.3.1 on page 354), (cv-qualified) void, or an array of unknown bound.

+   - For example:

Click here to view code image

```
is_default_constructible<int>                  // yields
true                                            // yields
is_copy_constructible<U>                        // yields
true
is_copy_constructible<std::unique_ptr<int>>     // yields
false
is_copy_constructible<std::string>              // yields
true
is_copy_constructible<const std::string>        // yields
false
is_constructible_v<std::string,const std::string&> // yields
true
is_constructible_v<std::string,std::string&&>    // yields
true
is_constructible_v<std::string,std::string&>     // yields
true
```

```
std::is_move_constructible<T>::value
std::is_trivially_move_constructible<T>::value
std::is_nothrow_move_constructible<T>::value
```

+   - Yields `true` if an object of type `T` can be created from an rvalue of type `T` (without using a nontrivial operation or with the guarantee that no exception is thrown).