

打印 14，并且

```
assign_m();
inc_m();
inc_m();
std::cout << process(12) << '\n';
```

打印 19。相同的打印语句会打印出不同的值，这取决于程序执行到该点为止的累积效应。

如果该函数失败，可能很难定位错误，因为这可能是*另一个*函数的过错，该函数向全局变量赋了一个错误的值。情况可能比上面的简单示例更复杂；请考虑：

```
assign_m();
.
.    /* 30 statements in between, some of which may change a,
.       b, and m */
.
if (a < 2 && b <= 10)
    m = a & b - 100;
.
.    /* 20 statements in between, some of which may change m */
.
std::cout << process(12) << '\n';
```

- 使用非局部变量的非平凡程序，对于人类读者来说，比不使用非局部变量的程序更难理解。在检查函数内容时，非局部变量要求读者到其他地方（函数外部）去查找其含义：

```
// Linear function
double f(double x) {
    return m*x + b;
}
```

m 和 b 是什么？它们在何处、何时以及如何被赋值或重新赋值？

- 仅使用局部变量的函数可以与其他函数隔离进行正确性测试，因为其他函数不会影响该函数的行为。该函数的行为仅受其参数（如果有的话）的影响。

从函数中排除全局变量会带来*函数独立性*。依赖于其作用域外部的信息才能正确执行任务的函数是依赖函数。当函数操作全局变量时，它依赖于该全局变量处于正确状态，以便函数能正确完成其任务。包含许多依赖函数的非平凡程序更难调试和扩展。一个真正独立的函数不使用任何全局变量，也不使用任何程序员定义的函数来帮助它，可以隔离地进行正确性测试。此外，独立函数可以从一个程序复制，粘贴到另一个程序中，无需修改即可工作。函数独立性是一种可取的品质。

与全局变量不同，全局常量通常可以安全使用。使用全局常量的函数中的代码依赖于这些常量，但由于常量不能更改，开发人员无需担心有权访问全局常量的其他函数可能会干扰它们的值。

在函数中使用全局常量在程序维护方面有缺点。随着程序的发展，代码会被添加和删除。如果在程序开发过程中删除了全局常量或其含义发生了变化，该更改将影响任何使用该全局常量的函数。

清单 10.2 (digitaltimer.cpp) 使用全局常量来辅助数字计时器的显示。

```
Listing 10.2: digitaltimer.cpp
#include <iostream>
#include <iomanip>
#include <ctime>

// Some conversions from seconds
const clock_t SEC_PER_MIN = 60,    // 60 sec = 1 min
              SEC_PER_HOUR = 60 * SEC_PER_MIN,  // 60 min = 1 hr
              SEC_PER_DAY = 24 * SEC_PER_HOUR;  // 24 hr = 24 hr

/*
 * print_time
 *
 * Displays the time in hr:min:sec format
 * seconds is the number of seconds to display
 */
void print_time(clock_t seconds) {
    clock_t hours = 0, minutes = 0;

    // Prepare to print time ========================
    std::cout << '\n';
    std::cout << " ";

    // Compute and display hours ====================
    hours = seconds/SEC_PER_HOUR;
    std::cout << std::setw(2) << std::setfill('0') << hours << ":";

    // Remove the hours from seconds
    seconds %= SEC_PER_HOUR;

    // Compute and display minutes ==================
    minutes = seconds/SEC_PER_MIN;
    std::cout << std::setw(2) << std::setfill('0') << minutes << ":";
    seconds %= SEC_PER_MIN;

    // Compute and display seconds ==================
    std::cout << std::setw(2) << std::setfill('0') << seconds << '\n';
}

int main() {
    clock_t start = clock();    // Record starting time
    clock_t elapsed = (clock() - start)/CLOCKS_PER_SEC, // Elapsed time in sec.
            previousElapsed = elapsed;
    // Counts up to 24 hours (1 day), then stops
    while (elapsed < SEC_PER_DAY) {
        // Update the display only every second
        if (elapsed - previousElapsed >= 1) {
            // Remember when we last updated the display
            previousElapsed = elapsed;
            print_time(elapsed);
        }
        // Update elapsed time
        elapsed = (clock() - start)/CLOCKS_PER_SEC;
    }
}
```

在清单 10.2 (digitaltimer.cpp) 中：

- main 函数控制时间初始化和更新，并且严格以秒为单位。main 中的逻辑保持相对简单。

- 从给定秒数中提取小时、分钟和秒的代码被隔离在 print_time 中。现在，每当需要将秒数表示为 小时:分钟:秒 格式时，都可以使用 print_time 函数。

- 秒转换常量（SEC_PER_HOUR、SEC_PER_MIN 和 SEC_PER_DAY）是全局常量，以便两个函数在必要时都可以访问它们。在这种情况下，函数使用不同的常量，但将所有转换因子放在一个地方是合理的。

由于两个函数以各自可以独立开发的方式划分了职责，设计更加清晰，程序也更容易开发和调试。使用常量可确保共享值不会被任何一个函数损坏。

从函数定义中排除全局变量和全局常量并不能保证它在给定相同参数值时总是产生相同的结果；请考虑：

```
int compute(int n) {
    int favorite;
    std::cout << "Please enter your favorite number: ";
    std::cin >> favorite;
    return n + favorite;
}
```

compute 函数避免了全局变量，但我们无法预测表达式 compute(12) 的值。

回顾上面的 increment 函数：

```
int increment(int n) {
    return n + 1;
}
```

它的行为完全可预测。此外，increment 不会修改任何全局变量，这意味着它绝不会以任何方式影响整个程序的行为。我们称 increment 为纯函数。纯函数不能执行任何输入或输出（例如，使用 std::cout 和 std::cin 对象），也不允许使用全局变量。虽然 increment 是纯函数，但 compute 函数是非纯函数。下面的函数也是非纯函数，因为它执行输出：

```
int increment_and_report(int n) {
    std::cout << "Incrementing " << n << '\n';
    return n + 1;
}
```

纯函数只是计算其返回值，没有其他可观察的副作用。

仅使用纯函数且否则会被视为纯函数的函数本身也是纯函数；例如：

```
int double_increment(int n) {
    return increment(n) + 1;
}
```

double_increment 是纯函数，因为 increment 是纯函数；但是，double_increment_with_report：

```
int double_increment_with_report(int n) {
    return increment_and_report(n) + 1;
}
```

不是纯函数，因为它调用了非纯函数 increment_and_report。

## 10.2 静态变量

计算机内存中局部变量和函数参数的空间是在函数开始执行时在运行时分配的。当函数结束并返回时，用于函数局部变量和参数的内存会被释放用于其他目的。如果函数从未被调用，函数的局部变量和参数将永远不会占用计算机内存。

由于函数的局部变量是短暂的，函数通常无法在调用之间保留任何信息。C++ 提供了一种方法，使函数局部变量可以在调用之间保留。清单 10.3 (counter.cpp) 展示了如何将局部变量声明为 static，使其在程序执行期间一直保留在计算机内存中。

```
Listing 10.3: counter.cpp

#include <iostream>
#include <iomanip>

/* count
 * Keeps track of a count.
 * Returns the current count.
 */
int count() {
    // cnt's value is retained between calls because it
    // is declared static
    static int cnt = 0;
    return ++cnt; // Increment and return current count
}

int main() {
    // Count to ten
    for (int i = 0; i < 10; i++)
        std::cout << count() << ' ';
    std::cout << '\n';
}
```

