# **A generic constructor**

```
```cpp
1  // implicitExplicitGenericConstructor.cpp
2  
3  #include <iostream>
4  #include <string>
5  
6  struct Implicit {
7      template <typename T>
8      Implicit(T t) {
9          std::cout << t << '\n';
10     }
11 };
12 
13 struct Explicit {
14     template <typename T>
15     explicit Explicit(T t) {
16         std::cout << t << '\n';
17     }
18 };
19 
20 int main() {
21 
22     std::cout << '\n';
23 
24     Implicit imp1 = "implicit";
25     Implicit imp2("explicit");
26     Implicit imp3 = 1998;
27     Implicit imp4(1998);
28 
29     std::cout << '\n';
30 
31     // Explicit exp1 = "implicit";
32     Explicit exp2("explicit");
33     // Explicit exp3 = 2011;
34     Explicit exp4(2011);
35 
36     std::cout << '\n';
37 
38 }
```
```

Now, you have an issue. A generic constructor (line 7) is a catch-all constructor because you can invoke it with any type. The constructor is way too greedy. By putting an `explicit` in front of the constructor (line 14), implicit conversions (lines 31 and 33) are not valid anymore. Only the explicit calls (lines 32 and 34) are valid.