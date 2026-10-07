# 2.4 Control flow

if constexpr

As we saw at the beginning of this chapter, we know that C++11 introduces the constexpr keyword, which compiles expressions or functions into constant results. A natural idea is that if we introduce this feature into the conditional judgment, let the code complete the branch judgment at compile time, can it make the program more efficient? C++17 introduces the constexpr keyword into the if statement, allowing you to declare the condition of an expression in your code. Consider the following code:

```
#include <iostream>
```

```
template<typename T>
auto print_type_info(const T& t) {
    if constexpr(std::is_integral<T>::value) {
        return t + 1;
    } else {
        return t + 0.001;
    }
}
int main() {
    std::cout << print_type_info(5) << std::endl;
    std::cout << print_type_info(3.14) << std::endl;
}
```

At compile time, the actual code will behave as:

```
int print_type_info(const int& t) {
    return t + 1;
}
double print_type_info(const double& t) {
    return t + 0.001;
}
int main() {
    std::cout << print_type_info(5) << std::endl;
    std::cout << print_type_info(3.14) << std::endl;
}
```

# Range-based for loop

Finally, C++11 introduces a range-based iterative method, and we have the ability to write loops that are as concise as Python, and we can further simplify the previous example: