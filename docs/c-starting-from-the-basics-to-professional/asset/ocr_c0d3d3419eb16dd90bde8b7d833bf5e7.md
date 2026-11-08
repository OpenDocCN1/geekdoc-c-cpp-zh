**Caution** Comparing floating-point numbers can be tricky. You should always be cautious when comparing the result of floating-point computations directly using operators such as `==`, `<=`, or `>=`. Rounding errors almost always prevent the floating-point value from ever becoming exactly equal to the mathematically precise value.

For the for loop in Ex_05_03, one option is to introduce an integral counter, specifically for controlling the loop. Another option is to replace the loop's condition with one that anticipates rounding errors. In this particular case, it suffices to use something like `radius < 3.0 + 0.001`. Instead of 0.001, you can use any number sufficiently greater than the expected rounding errors yet sufficiently less than the loop's .2 increment. A corrected version of the program can be found in Ex_05_03A.cpp. Most math libraries and so-called unit test frameworks will offer utility functions to aid you with comparing floating-point numbers in a reliable manner.

# More Complex for Loop Control Expressions

You can define and initialize more than one variable of a given type in the first for loop control expression. You just separate each variable from the next with a comma. Here's a working example that uses that:

```
```cpp
// Ex_04.cpp
// Multiple initializations in a loop expression
import <iostream>;
import <format>;

int main()
{
  unsigned int limit {};
  std::cout << "This program calculates n! and the sum of the integers "
            << "up to n for values 1 to limit.\n";

  std::cout << "What upper limit for n would you like? ";
  std::cin >> limit;

  // The format string for all rows of the table
  const auto table_format = "{:8} {:8} {:20}\n";

  // Output column headings
  std::cout << std::format(table_format, "integer", "sum", "factorial");

  for (unsigned long long n {1}, sum {}, factorial {1}; n <= limit; ++n)
  {
    sum += n;          // Accumulate sum to current n
    factorial *= n;    // Calculate n! for current n
    std::cout << std::format(table_format, n, sum, factorial);
  }
}
```
```

The program calculates the sum of the integers from 1 to n for each integer n from 1 to limit, where limit is an upper limit that you enter. It also calculates the factorial of each n. (The factorial of an integer n, written n!, is the product of all the integers from 1 to n; for example, 5! = 1 × 2 × 3 × 4 × 5 = 120.)