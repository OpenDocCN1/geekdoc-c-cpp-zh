```
```cpp
// add one or more arguments with a fold expression
template <typename FirstItem, typename... RemainingItems>
auto foldingSum(FirstItem first, RemainingItems... theRest) {
    return (first + ... + theRest); // expand the parameter
}

int main() {
    using namespace std::literals;

    std::cout << "Recursive variadic function template sum:"
        << std::format("\n{}\n{}\n{}\n{}\n",
            "sum(1): ", sum(1), "sum(1, 2): ", sum(1, 2),
            "sum(1, 2, 3): ", sum(1, 2, 3),
            "sum(\"s\", \"u\", \"m\"): ", sum("s"s, "u"s, "m"s));

    std::cout << "Variadic function template foldingSum:"
        << std::format("\n{}\n{}\n{}\n{}\n",
            "sum(1): ", foldingSum(1), "sum(1, 2): ", foldingSum(1, 2),
            "sum(1, 2, 3): ", foldingSum(1, 2, 3),
            "sum(\"s\", \"u\", \"m\"): ",
            foldingSum("s"s, "u"s, "m"s));
}
```
```

```
```text
Recursive variadic function template sum:
sum(1): 1
sum(1, 2): 3
sum(1, 2, 3): 6
sum("s", "u", "m"): sum

Variadic function template foldingSum:
sum(1): 1
sum(1, 2): 3
sum(1, 2, 3): 6
sum("s", "u", "m"): sum
```
```

**Fig. 15.14** | Variadic function templates. (Part 2 of 2.)

# Compile-Time Recursion

Lines 8–11 and 14–17 define overloaded function templates named `sum` that use compile-time recursion to process variadic parameter packs. The function template sum with one template parameter (lines 8–11) represents the recursion’s base case, in which sum receives only one argument and returns it. The recursive function template sum (lines 14–17) specifies two type parameters:

+   - The type parameter `FirstItem` represents the first function argument.
+   - The type parameter `RemainingItems` represents all the other arguments passed to the function.

The typename `...` introduces a variadic template’s parameter pack representing any number of arguments. In the function’s parameter list (line 15), the variable-length parameter must appear last and is denoted with `...` after its type (`RemainingItems`). Note