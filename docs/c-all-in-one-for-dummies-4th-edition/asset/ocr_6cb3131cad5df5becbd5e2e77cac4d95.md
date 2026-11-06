# Dealing with Pack Expansions

A data pack is a group of variables sent to a templated function in which the number of variables is unknown until runtime. Pack expansion is an essential part of dealing with a variable number of arguments. The following sections describe pack expansion using a number of examples so that you can see how the basic concept works.

# Considering the template

Starting with C++11, you can send a variable number of arguments using a variadic template. To provide you with a basic idea of how this works, consider the code found in the `VariadicTemplate` example, as shown in Listing 3-3.

# LISTING 3-3: Using a Variadic Template

```
```cpp
#include <iostream>

using namespace std;

template<typename... Types>
size_t nargs(Types... args) {
  return sizeof...(args);
}

int main()
{
  cout << nargs(1, "3.5", true) << endl;
  cout << nargs(2, 4, "Hello", 1.1) << endl;
  cout << nargs() << endl;
  return 0;
}
```
```

The `...` operator says that this code is variadic — meaning that the number of arguments and their types are unknown. The `nargs()` function receives a variable number of arguments in a single packed variable, `args`. All this function does is tell you the number of arguments passed, so you see the following output:

```
```text
3
4
0
```
```