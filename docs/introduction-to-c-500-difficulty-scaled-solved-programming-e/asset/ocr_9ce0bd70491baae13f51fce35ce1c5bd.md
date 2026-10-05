Although we would expect this count to display No, it displays 0. Let's see why. The first, the count << (a > 20) is executed, displays 0. The << operator returns the count (we'll see how in Chapter 18), so the initial expression becomes equivalent to count ? "Yes\n" : "No\n"; This expression does not print anything. It checks the value of count, and because the expression yields Yes. To display the correct result we must use parentheses:

```
cout << ((a > 20) ? "Yes\n" : "No\n");
```

# EXERISES

C.5.11 What is the output of the following program?

```
#include <iostream>
int main()
{
    int a = 1, b = !a;
    if(b ? a : -a) <= 10)
        std::cout << "One " << -a << '\n';
    else
        std::cout << "Two " << -a << '\n';
    return 0;
}
```

Answer: Since b is 0, the result of the conditional expression is -a, that is, -1. The value of a does not change, it remains 1. Therefore, if the condition is true, the program outputs: One -1

C.5.12 Write a program that reads the price of three products and uses the ?: operator to display the highest price.

```
#include <iostream>
int main()
{
    float i, j, k;
    std::cout << "Enter prices: ";
    std::cin >> i >> j >> k;
    std::cout << "Max: " << ((i >= j && i >= k) ? i : (j > i && j > k) ? j : k) << '\n';
    return 0;
}
```

Comments: To display the lowest price we change the ? to <.

C.5.13 Write a program that reads a student's grade and uses the ?: operator to display a corresponding message to the next scale:

+   a. If grade is within [7.5–7.5], the program outputs: A
b. If grade is within [5–7.5], the program outputs: B
c. If grade is within [0–5], the program outputs: Next time
d. If grade is out of [0, 10], the program outputs: Wrong input