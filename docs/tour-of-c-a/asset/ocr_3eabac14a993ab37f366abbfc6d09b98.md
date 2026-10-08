```
auto twice(Arithmetic auto x) { return x+x; } // just for numbers
auto thrice(auto x) { return x+x+x; } // for anything with a +

auto x1 = twice(7); // OK: x1==14
string s "Hello";
auto x2 = twice(s); // error: a string is not Arithmetic
auto x3 = thrice(s); // OK x3="Hello Hello Hello"
```