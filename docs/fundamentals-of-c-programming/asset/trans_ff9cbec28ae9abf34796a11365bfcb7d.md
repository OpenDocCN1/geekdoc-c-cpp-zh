

```cpp
#include <iostream>

/*
 * increment(x)
 * Illustrates pass by value protocol.
 */
void increment(int x) {
    std::cout << "Beginning execution of increment, x = "
              << x << " \n";
    x++; // Increment x
    std::cout << "Ending execution of increment, x = "
              << x << " \n";
}

int main() {
    int x = 5;
    std::cout << "Before increment, x = " << x << " \n";
    increment(x);
    std::cout << "After increment, x = " << x << " \n";
}
```

为了增加戏剧性，我们选择将实际参数与形式参数命名相同。由于实际参数和形式参数在不同的上下文中声明和使用，并代表完全不同的内存位置，因此它们的名称可以相同而不会出现任何问题。

清单 9.9 (passbyvalue.cpp) 的输出为

```
Before increment, x = 5
Beginning execution of increment, x = 5
Ending execution of increment, x = 6
After increment, x = 5
```

main 中变量 x 的内存不受影响，因为 increment 对实际参数的副本进行操作。

C++ 支持另一种称为按引用传递的参数传递方式。按引用传递将在第 10.9 节中介绍。

函数以调用者按值传递参数的相同方式向调用者传递其返回值。在我们之前看到的 prompt 函数中：

```cpp
int prompt(int n) {
    int result;
    std::cout << "Please enter integer # " << n << ": ";
    std::cin >> result;
    return result;
}
```

return 语句是

```
return result;
```

变量 result 是 prompt 的局部变量。我们非正式地说我们正在返回 result 变量，但实际上，我们真正返回的只是 result 变量的值。调用者无法访问其调用的任何函数中声明的局部变量。事实上，函数的局部变量仅在函数处于活动状态（即正在执行）时才存在。当函数返回到其调用者时，其所有局部变量都会从内存中消失。在后续调用中，当函数再次变为活动状态时，其局部变量会重新出现，并在函数结束时再次消失。

## 9.4 函数示例

本节包含一些示例，说明如何使用函数来组织程序的代码。

### 9.4.1 更好组织的素数生成器

清单 9.10 (primefunc.cpp) 是清单 8.5 (moreefficientprimes.cpp) 的一个简单改进。它使用了平方根优化，并添加了一个单独的 is_prime 函数。

```cpp
Listing 9.10: primefunc.cpp

#include <iostream>
#include <cmath>

/*
 * is_prime(n)
 *  Determines the primality of a given value
 *  n an integer to test for primality
 *  Returns true if n is prime; otherwise, returns false
 */
bool is_prime(int n) {
    bool result = true;   // Provisionally, n is prime
    double root_n = sqrt(n);
    // Try all possible factors from 2 to the square
    // root of
    for (int trial_factor = 2;
         result && trial_factor <= root_n; trial_factor++)
        result = (n % trial_factor != 0);
    return result;
}

/*
 * main
 *  Tests for primality each integer from 2
 *  up to a value provided by the user.
 *  If an integer is prime, it prints it;
 *  otherwise, the number is not printed.
 */
int main() {
    int max_value;
    std::cout << "Display primes up to what value? ";
    std::cin >> max_value;
    for (int value = 2; value <= max_value; value++)
        if (is_prime(value)) // See if value is prime
            std::cout << value << " "; // Display the prime number
    std::cout << "\n"; // Move cursor down to next line
}
```

清单 9.10 (primefunc.cpp) 说明了关于组织良好的程序的几个重要点：

- 程序的完整工作不再局限于 main 函数。测试素性的工作被委托给一个单独的函数。main 专注于一个更简单的任务：生成所有要考虑的数字，并使用另一个函数 (is_prime) 来完成确定给定数字是否为素数的艰苦工作。main 现在更简单，也更具逻辑连贯性。当函数专注于单一任务时，它就是连贯的。连贯性是函数的理想属性。如果函数试图做太多不同的事情而变得过于复杂，那么编写正确代码并在发现问题时进行调试可能会更加困难。复杂的函数应该分解为几个更小、更连贯的函数。然后，原始函数将调用这些新的更简单的函数来完成其任务。在这里，main 不关心如何确定给定数字是否为素数；main 只是将工作委托给 is_prime，并利用 is_prime 函数的发现。

- 每个函数之前都有一个详尽的注释，描述了函数的性质。它解释了每个参数的含义，并指示函数应该返回什么。main 的注释可能不如其他函数详尽；这是因为 main 通常没有参数，并且在程序终止时始终向操作系统返回一个代码。

- 尽管外部注释指示函数要做什么，但每个函数内部的注释会更详细地解释函数如何完成其任务。

对 is_prime 的调用根据传递给它的值返回 true 或 false。这意味着我们可以像这样表达一个条件：

```
if (is_prime(value) == true) . . .
```

更紧凑地表达为

```
if (is_prime(value)) . . .
```

因为如果 is_prime(value) 为 true，则 true == true 为 true；如果 is_prime(value) 为 false，则 false == true 为 false。表达式 is_prime(value) 就足够了。

正如循环最好只有一个入口点和一个出口点一样，理想情况下函数也应该只有一个 return 语句。然而，返回语句数量较少的简单函数通常也是可以接受的。请考虑 is_prime 的以下版本：

```cpp
bool is_prime(int n) {
    for (int trialFactor = 2;
         trialFactor <= sqrt(static_cast<double>(n));
         trialFactor++)
        if (n % trialFactor == 0) // Is trialFactor a factor?
            return false; // Yes, return right away
    return true; // Tried them all, must be prime
}
```

此版本使用两个 return 语句，但消除了对局部变量 (result) 的需求。因为 return 语句会立即退出函数，所以不需要 break 语句。源代码中的两个 return 语句在文本上足够接近，因此逻辑相当清晰。

### 9.4.2 命令解释器

有些函数即使不从调用者接收任何信息且不返回任何结果也是有用的。清单 9.11 (calculator.cpp) 使用了这样的函数。

```cpp
Listing 9.11: calculator.cpp
#include <iostream>
#include <cmath>

/*
 * help_screen
 * Displays information about how the program works
 * Accepts no parameters
 * Returns nothing
 */
void help_screen() {
    std::cout << "Add: Adds two numbers\n";
    std::cout << "Example: a 2.5 8.0\n";
    std::cout << "Subtract: Subtracts two numbers\n";
    std::cout << "Example: s 10.5 8.0\n";
    std::cout << "Print: Displays the result of the latest operation\n";
    std::cout << "Example: p\n";
    std::cout << "Help: Displays this help screen\n";
    std::cout << "Example: h\n";
    std::cout << "Quit: Exits the program\n";
    std::cout << "Example: q\n";
}

/*
 * menu
 * Display a menu
 * Accepts no parameters
 * Returns the character entered by the user.
 */
char menu() {
    // Display a menu
    std::cout << "=== A)dd S)ubtract P)rint H)elp Q)uit ===\n";
    // Return the char entered by user
    char ch;
    std::cin >> ch;
    return ch;
}

/*
 * main
 * Runs a command loop that allows users to
 * perform simple arithmetic.
 */
int main() {
    double result = 0.0, arg1, arg2;
    bool done = false; // Initially not done
    do {
        switch (menu()) {
        case 'A': // Addition
case 'a':
    std::cin >> arg1 >> arg2;
    result = arg1 + arg2;
    std::cout << result << '\n';
    break;
case 'S': // Subtraction
case 's':
    std::cin >> arg1 >> arg2;
    result = arg1 - arg2;
    // Fall through, so it prints the result
case 'P': // Print result
case 'p':
    std::cout << result << '\n';
    break;
case 'H': // Display help screen
case 'h':
    help_screen();
    break;
case 'Q': // Quit the program
case 'q':
    done = true;
    break;
}
} while (!done);
}
```

help_screen 函数不需要来自 main 的任何信息，也不返回任何结果。每次调用时，它的行为都完全相同。menu 函数返回用户输入的字符。

### 9.4.3 受限输入

清单 7.3 (betterinputonly.cpp) 强制用户输入指定范围内的值。现在我们可以轻松地将该概念调整为一个函数。清单 9.12 (betterinputfunc.cpp) 使用一个名为 get_int_range 的函数，该函数在用户提供适当值之前不会返回。

```cpp
Listing 9.12: betterinputfunc.cpp

#include <iostream>

/*
 * get_int_range(first, last)
 *
 * Forces the user to enter an integer within a
 * specified range
 *
 * first is either a minimum or maximum acceptable value
 * last is the corresponding other end of the range,
 * either a maximum or minimum value
 * Returns an acceptable value from the user
 */
int get_int_range(int first, int last) {
    // If the larger number provided first,
    // switch the parameters
    if (first > last) {
        int temp = first;
```

