```
};
int main() {
  cout << min3(3, 7, 2) << '\\n';
  cout << min3(8.11, 113.2, -3.1) << '\\n'; // Error: not an
integral type
}
```

Here we have restricted the arguments with integral so that min3(8.11...) no longer compiles. This works with functions like min2() as well as with lambdas like min3().

But you have even more options. First, you have already learned about the requires keyword. With it, you can not only specify a single concept but also combine multiple ones add further conditions.

```
// https://godbolt.org/z/fxoo4h9Gj
#include <concepts>
#include <iostream>
#include <string>
using namespace std; using std::literals;

string mk_string(integral auto val) { return to_string(val); };
template<typename T>
string mk_string(string val) { return '+'+val+'; };
requires copyable<T> // Type requirement
requires (T t) { mk_string(t) + mk_string(t); } // simple requirement
requires (T t) { // composite requirement
  mk_string(t) -> same_as<string>; // valid expression must meet condition
}
string dbl_quote(const T val) { // Create a copy (for demonstration)
  purposes only
  return '*' + mk_string(val) + '*';
}

int main() {
  cout << dbl_quote(10) << '\\n'; // Output: "1010"
  cout << dbl_quote("ab") << '\\n'; // Output: "[ab]"
  cout << dbl_quote(3.14) << '\\n'; // Error: no suitable mk_string
```