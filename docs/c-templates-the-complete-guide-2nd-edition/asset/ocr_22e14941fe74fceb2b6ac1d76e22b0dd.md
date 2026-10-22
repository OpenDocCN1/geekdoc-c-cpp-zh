```
IsConvertibleT<int, int>::value          // yields true
IsConvertibleT<int, std::string>::value      // yields false
IsConvertibleT<char const*, std::string>::value // yields true
IsConvertibleT<std::string, char const*>::value // yields false
```