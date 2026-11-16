
程序不会记录输入值的数量。程序只是将输入值累加到名为 sum 的变量中。

在清单 6.4 (addnonnegatives.cpp) 中，相同的条件出现了两次，一次在 while 中，又一次在 if 中，这有点别扭。此外，如果用户希望同时输入负值和非负值怎么办？我们可以使用一种常见的 C++ 惯用法来简化代码，该惯用法将 std::cin 和提取运算符作为 while 语句中的条件。

如果 x 是整数，表达式
std::cin >> x

如果用户没有输入有效的整数字面量，则求值为 false。掌握了这些知识，我们可以像清单 6.5 (addnumbers.cpp) 所示那样简化和增强清单 6.4 (addnonnegatives.cpp)。

## 清单 6.5: addnumbers.cpp

```cpp
#include <iostream>

int main() {
  int input, sum = 0;
  std::cout << "Enter numbers to sum, type 'q' to end the list:";
  while (std::cin >> input) {
    sum += input;
  }
  std::cout << "Sum = " << sum << '\n';
}
```

该条件从输入流读取一个值，如果成功，则被解释为 true。当用户输入 'q' 时，循环终止。如果用户在开头输入 'q'，则不会进入循环。if 语句不再必要，因为只有在 input 被合法赋值后，语句

```
sum += input;
```

才会执行。此外，变量 input 不再需要仅为了第一次进入循环而初始化一个值；现在它在 while 的条件中被赋值然后检查。

在清单 6.5 (addnumbers.cpp) 中，程序执行将在用户输入任何字母时终止；输入 'x' 或 Ctrl+Z 将像 'q' 一样终止序列。

如果使用

```
while (std::cin >> x) {
  // Do something ...
}
```

惯用法，请注意，当由于输入流无法读取变量 x 类型的值而退出循环时，std::cin 输入流对象会保持在错误状态，并且在程序其余执行期间无法使用。如果你希望使用此技术并稍后重用 std::cin，则必须重置 std::cin 并提取并丢弃自上次有效使用提取运算符以来输入的按键。此恢复过程在第 13.2 节中介绍，但目前，只有在程序在其执行期间不需要稍后的额外用户输入时，才使用此惯用法来控制循环。

清单 6.6 (powersof10.cpp) 打印从 1 到 1,000,000,000 的 10 的幂（下一个 10 的幂 10,000,000,000 超出了 `int` 类型的范围）。

## 清单 6.6: powersof10.cpp

```cpp
#include <iostream>
int main() {
    int power = 1;
    while (power <= 1000000000) {
        std::cout << power << '\n';
        power *= 10;
    }
}
```

清单 6.6 (powersof10.cpp) 生成

```
1
10
100
1000
10000
100000
1000000
10000000
100000000
1000000000
```

通常将一列数字右对齐，但清单 6.6 (powersof10.cpp) 将 10 的幂的最高有效数字左对齐打印。我们可以使用称为流操纵器的流对象将数字右对齐。我们需要的特定流操纵器名为 `std::setw`。setw 意为“设置宽度”。它可以这样使用

```cpp
std::cout << std::setw(3) << x << '\n';
```

该语句将 x 的值在屏幕上的三个字符水平空间内右对齐打印。清单 6.7 (powersof10justified.cpp) 显示了 setw 的效果。

## 清单 6.7: powersof10justified.cpp

```cpp
#include <iostream>
#include <iomanip>
// Print the powers of 10 from 1 to 1,000,000,000
int main() {
    int power = 1;
    while (power <= 1000000000) {
        // Right justify each number in a field 10 wide
        std::cout << std::setw(10) << power << '\n';
        power *= 10;
    }
}
```

清单 6.7 (powersof10justified.cpp) 打印

![](img/e84ad11adb18201d71595b31ce6c9eff_141_0.png)

请注意，为了使用 `setw`，编译器需要了解它。关于 `std::setw` 所需的信息不在 `iostream` 头文件中，因此需要额外的预处理器包含指令：

```cpp
#include <iomanip>
```

`std::setw` 操纵器“调节”输出流以打印下一个项目。传递给“调节”流的值都在 `std::setw` 指定的空格数内右对齐。

顺便说一句，这是揭示另一个改进 C++ 程序输出技巧的好地方。清单 6.8 (powersof10withcommas.cpp) 通过在显示的数字中适当位置添加逗号来增强清单 6.7 (powersof10justified.cpp)。

## 清单 6.8: powersof10withcommas.cpp

```cpp
#include <iostream>
#include <iomanip>
#include <locale>

// Print the powers of 10 from 1 to 1,000,000,000
int main() {
    int power = 1;
    std::cout.imbue(std::locale(""));
    while (power <= 1000000000) {
        // Right justify each number in a field 10 wide
        std::cout << std::setw(13) << power << '\n';
        power *= 10;
    }
}
```

清单 6.8 (powersof10withcommas.cpp) 打印

![](img/e84ad11adb18201d71595b31ce6c9eff_141_1.png)

## 图 6.2 计算机系统故障排除决策树 清单 6.9 (troubleshootloop.cpp)

![](img/e84ad11adb18201d71595b31ce6c9eff_142_0.png)

语句

```cpp
std::cout.imbue(std::locale(""));
```

调整 std::cout 对象以打印带有适合当前国家的数字分隔符的数字。如果将该语句替换为

```cpp
std::cout.imbue(std::locale("german"));
```

输出将变为

| 1 |
| --- |
| 100 |
| 1.000 |
| 10.000 |
| 100.000 |
| 1.000.000 |
| 10.000.000 |
| 100.000.000 |
| 1.000.000.000 |
| 10.000.000.000 |
| 100.000.000.000 |
| 1.000.000.000.000 |

因为德语在数字分隔符中使用句点代替逗号。“german”区域设置还会在英语浮点数出现小数点的地方显示逗号。

我们可以使用 while 语句使清单 5.12 (troubleshoot.cpp) 对用户更方便。请记住，计算机故障排除程序在检测到潜在问题后会强制用户重新运行程序（例如，打开电源开关，然后再次运行程序以查看可能还有什么问题）。更理想的决策逻辑如图 6.2 所示。

清单 6.9 (troubleshootloop.cpp) 包含一个 while 语句，以便程序执行继续直到问题解决或问题的解决超出了程序的能力范围。

## 清单 6.9: troubleshootloop.cpp

```cpp
#include <iostream>

int main() {
    std::cout << "Help!  My computer doesn't work!\n";
    char choice;
    bool done = false; // Initially, we are not done

    while (!done) { // Continue until we are done
        std::cout << "Does the computer make any sounds "
                  << "(fans, etc.) or show any lights? (y/n): ";
        std::cin >> choice;
        // The troubleshooting control logic
        if (choice == 'n') { // The computer does not have power
            std::cout << "Is it plugged in? (y/n): ";
            std::cin >> choice;
            if (choice == 'n') { // It is not plugged in, plug it in
                std::cout << "Plug it in.\n";
            }
        } else { // It is plugged in
            std::cout << "Is the switch in the \"on\" position? (y/n): ";
            std::cin >> choice;
            if (choice == 'n') { // The switch is off, turn it on!
                std::cout << "Turn it on.\n";
            } else { // The switch is on
                std::cout << "Does the computer have a fuse? (y/n): ";
                std::cin >> choice;
                if (choice == 'n') { // No fuse
                    std::cout << "Is the outlet OK? (y/n): ";
                    std::cin >> choice;
                    if (choice == 'n') { // Fix outlet
                        std::cout << "Check the outlet's circuit "
                                  << "breaker or fuse. Move to a "
                                  << "new outlet, if necessary.\n";
                    }
                } else { // Beats me!
                    std::cout << "Please consult a service "
                              << "technician.\n";
                    done = true; // Exhausted simple fixes
                }
            }
        } else { // Check fuse
            std::cout << "Check the fuse. Replace if "
                      << "necessary.\n";
        }
    } // The computer has power
    std::cout << "Please consult a service technician.\n";
}
```

