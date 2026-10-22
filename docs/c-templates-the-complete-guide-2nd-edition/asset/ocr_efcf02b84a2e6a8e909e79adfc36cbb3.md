```
std::string s = "hi";
passR(s);                  // OK: T deduced as std::string& (also the type of arg)
passR(std::string("hi")); // OK: T deduced as std::string, arg is std::string&&
passR(returnString());     // OK: T deduced as std::string, arg is std::string&&
passR(std::move(s));       // OK: T deduced as std::string, arg is std::string&&
passR(arr);                // OK: T deduced as int(&) [4] (also the type of arg)
```