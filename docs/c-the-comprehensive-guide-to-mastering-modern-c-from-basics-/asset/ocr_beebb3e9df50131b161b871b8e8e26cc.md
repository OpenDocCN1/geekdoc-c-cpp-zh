# 2.7 Speed Up the Sample Program

If the program runs too long for you, then tabulate the intermediate results. This means that you save them in a table-like data structure. The zeroth entry receives fib(0), the first result of fib(1), and so on. If you want to use fib(n) to calculate the nth entry in the table, do not call fib(n-1) and fib(n-2), but look in the table instead. Then you will get the results faster than you can. Create a new project or modify the program:

```
// https://godbolt.org/z/3W1qY7b9x
// modern102.cpp : Fibonacci console
#include <iostream>
#include <map>
int fib(int n) {
    static std::map<int, int> table;
    table[n] = n<=1 ? n : table[n-2] + table[n-1];
}
int main() {
    std::cout << "How many Fibonacci numbers?";
    int n = 0;
    std::cin >> n;
    for (int i = 1; i <= n; ++i)
        std::cout << "fib" << i << " =" << fib(i) << "\n";
}
```

**Listing 2.2** A quickly created table of Fibonacci numbers.

If you enter “50” here, for example, then you will see that the results are sometimes negative from 46—an overflow. The same applies here: On platforms other than 32/64-bit Windows, you may have different