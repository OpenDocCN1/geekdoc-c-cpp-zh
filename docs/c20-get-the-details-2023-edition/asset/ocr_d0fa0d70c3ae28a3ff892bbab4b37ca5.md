```
```cpp
45    printContainer(set5);
46
47    std::cout << "\n\n";
48
49 }
```
```

set1 (line 19) and set4 (line 38) sort their keys in ascending order. Each of set2 (line 26), set3 (line 33), and set5 (line 44) sorts its keys in an uniquely manner, using a lambda in an unevaluated context. The using keyword (line 22) declares a type alias, which is used in the following line (line 26) to define the sets. Creating the std::set causes the call of the default constructor of the stateless lambda.

Here is the output of the program.

```
```
Bjarne Dave Herb michael scott
scott michael Herb Dave Bjarne
Herb scott Bjarne michael

-25  -10  0  3  5  100
0  3  5  -10  -25  100
```
```

Use of a lambda in an unevaluated context

When you study the output of the program, you may be surprised. The special set3, which uses the lambda [](const auto& l, const auto& r){ return l.size() < r.size(); } as a predicate, ignores the name Dave. The reason is simple. Dave has the same size as Herb, which was added first. std::set supports unique keys, and the keys in this case are identical using the special predicate. If I had used std::multiset, this wouldn't have happened.

# 4.7.4 consteval Lambdas

C++20 support consteval in C++20. consteval lambdas means that the lambda is an immediate function executed at compile time.

A consteval lambda

```
```cpp
1    // constevalLambda.cpp
2
3    #include <algorithm>
4    #include <iostream>
5    #include <vector>
6
7    int main() {
8
9        std::cout << '\n';
10
```
```