# ## Comparison of const, constexpr, and constinit

```
~~~cpp
 1  // constexprConstinit.cpp
 2
 3  #include <iostream>
 4
 5  constexpr int constexprVal = 1000;
 6  constinit int constinitVal = 1000;
 7
 8  int incrementMe(int val){ return ++val;}
 9
10  int main() {
11
12      auto val = 1000;
13      const auto res = incrementMe(val);
14      std::cout << "res: " << res << '\n';
15
16      // std::cout << "res: " << ++res << '\n';          ERROR
17      // std::cout << "++constexprVal: " << ++constexprVal << '\n'; ERROR
18      std::cout << "++constinitVal: " << ++constinitVal << '\n';
19
20      constexpr auto localConstexpr = 1000;
21      // constinit auto localConstinit = 1000; ERROR
22
23  }
~~~
```

Only the const variable (line 13) is initialized at run time. The constexpr and constinit variables are initialized at compile time.

The constinit (line 18) does not imply constness, as do const (line 16) or constexpr (line 17). A constexpr (line 20) or const (line 13) declared variable can be created as a local, but not a constinit declared variable (line 21).

![](bbox=[0.378, 0.766, 0.615, 0.845])

const, constexpr, and constinit declared variables