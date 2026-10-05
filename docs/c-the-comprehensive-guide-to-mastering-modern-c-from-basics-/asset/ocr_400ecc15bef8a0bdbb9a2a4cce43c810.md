```
#include <iostream>
#include <vector>
#include <string>
using std::string; using std::string; using std::vector;
struct Squares {
    mutable int n = 1;
    int operator()() const { return n*n++; }
};

int main() {
    vector<int> sq(10);
    std::ranges::generate(sq, Squares());
    std::ranges::for_each(sq, [](auto n) {
        std::cout << n << " ";
    });
    std::cout << '\nNCC:'; // Output: 1 4 9 16 25 36 49 64 81 100
    std::string a = "NCC:";
    vector<int> b = {1, 7, 0, 1};
    vector<string> c(4);
    auto f = [](char c, int int) -> string { return string(c); };
    std::ranges::transform(
        a,
        b.begin(),
        c.begin(),
        f);
    std::ranges::for_each(c, [](auto s) {
        std::cout << s << " ";
    });
    std::cout << '\n'; // Output: N1 C7 C0
}
```

**Listing 25.12** “transform” can juggle with different types.

The example around generate demonstrates how functor Squares continuously generates square numbers. qs contains 10 elements, so the functor is called 10 times. Because it maintains an internal state with n, but the operator() must be const, the n is marked as mutable to be changeable.

The transform algorithm, holds elements of type char, b holds elements of type int, and the output goes into c with elements of type string. Therefore, for transform, the function f must have the function<string(char,int)> type, which is the case for the lambda f.