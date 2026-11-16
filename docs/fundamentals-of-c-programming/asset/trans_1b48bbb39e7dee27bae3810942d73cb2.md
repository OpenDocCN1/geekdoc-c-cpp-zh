
## 5.6. 复合布尔表达式

```
! (x == y)
(x < y || x > y)
```

在表达式 e1 && e2 中，子表达式 e1 和 e2 必须都为真，整体表达式才为真。由于 && 运算符从左到右求值，这意味着如果 e1 为假，则无需求值 e2。如果 e1 为假，则无论 e2 取何值，都无法使表达式 e1 && e2 为真。逻辑 && 运算符首先测试其左侧的表达式。如果发现该表达式为假，则不会费心去检查右侧表达式。这种方法称为短路求值。类似地，在表达式 e1 || e2 中，如果 e1 为真，那么 e2 的值无关紧要——除非两个子表达式都为假，否则逻辑或表达式为真。|| 运算符也使用短路求值。

为什么短路求值很重要？以下两种情况说明了为什么需要考虑它：

- 子表达式的顺序会影响性能。程序运行时，复杂表达式的求值时间比简单表达式更长。我们将求值时间相对较长的表达式称为昂贵表达式。如果复合布尔表达式由一个昂贵的布尔子表达式和一个较不昂贵的布尔子表达式组成，则应将较昂贵的布尔表达式放在第二位。如果第一个子表达式为假且使用的是 &&，则不会求值昂贵的第二个子表达式；如果第一个子表达式为真且使用的是 ||，则同样会避免求值昂贵的第二个子表达式。

- 可以对子表达式进行排序以防止运行时错误。当一个子表达式以某种方式依赖于另一个子表达式时，这一点尤其正确。请考虑以下表达式：

```
(x != 0) && (z/x > 1)
```

在这里，如果 x 为零，则避免了除以零的情况。如果子表达式互换位置，当 x 为零时会导致运行时错误。

| 目数 | 运算符 | 结合性 |
|---|---|---|
| 一元 | (post) ++ (post) -- static_cast | |
| 一元 | (pre) ++ (pre) -- - + ! ~ | |
| 二元 | * / % | 左 |
| 二元 | + - | 左 |
| 二元 | << >> | 左 |
| 二元 | < > <= >= | 左 |
| 二元 | == != | 左 |
| 二元 | & | 左 |
| 二元 | ^ | 左 |
| 二元 | \| | 左 |
| 二元 | && | 左 |
| 二元 | \|\| | 左 |
| 二元 | =, +=, -=, *=, /=, %= | 右 |

假设你希望当变量 x 为 1、2 或 3 时打印单词“OK”。从英语非正式翻译可能会产生：

```
if (x == 1 || 2 || 3)
    std::cout << "OK\n";
```

不幸的是，x 的值无关紧要；代码始终打印单词“OK”。由于 == 运算符的优先级高于 ||，表达式

```
x == 1 || 2 || 3
```

![](img/e84ad11adb18201d71595b31ce6c9eff_112_0.png)

```
(x == 1) || 2 || 3
```

表达式 x == 1 要么为真要么为假，但整数 2 始终被解释为真，整数 3 也被解释为真。

正确的语句应为

```
if (x == 1 || x == 2 || x == 3)
    std::cout << "OK\n";
```

修订后的布尔表达式更为冗长，也与英文表述不那么相似，但它是 C++ 的正确写法。

当前的 C++ 运算符列表如表 5.4 所示。

## 5.7 嵌套条件语句

if 或 else 语句块中的语句可以是任何 C++ 语句，包括其他 if/else 语句。我们可以使用嵌套 if 语句来构建任意复杂的控制流逻辑。请考虑清单 5.7（checkrange.cpp），它用于判断一个数字是否在 0 到 10 之间（包含 0 和 10）。

```
Listing 5.7: checkrange.cpp

#include <iostream>
int main() {
int value;
std::cout << "Please enter an integer value in the range 0...10: ";
std::cin >> value;
if (value >= 0) // First check
if (value <= 10) // Second check
std::cout << "In range";
std::cout << "Done\n";
}
```

清单 5.7（checkrange.cpp）的行为如下：

- 程序首先检查 value >= 0 条件。如果 value 小于零，执行中的程序不会求值第二个条件，也不会打印 In range，而是立即执行外部 if 语句后面的打印语句，该语句打印 Done。

- 如果执行中的程序发现 value 大于或等于零，则检查第二个条件。如果满足第二个条件，则显示 In range 消息；否则不显示。无论如何，程序在终止前都会打印 Done。

要使程序显示 In range 消息，必须满足这个嵌套 if 的两个条件。换句话说，必须同时满足第一个条件和第二个条件，才能打印 In range 消息。从这个角度来看，我们可以重写程序，只使用一个 if 语句即可实现相同的行为，如清单 5.8（newcheckrange.cpp）所示。

### 清单 5.8: newcheckrange.cpp

```
#include <iostream>
int main() {
int value;
std::cout << "Please enter an integer value in the range 0...10: ";
std::cin >> value;
if (value >= 0 && value <= 10)
std::cout << "In range\n";
}
```

清单 5.8（newcheckrange.cpp）使用逻辑 && 同时检查两个条件。其逻辑更简单，只使用一个 if 语句，代价是条件中的布尔表达式稍微复杂一些。在这里，第二个版本更可取，因为更简单的逻辑通常是一个可取的目标。

有时，程序的逻辑无法像清单 5.8（newcheckrange.cpp）那样简化。在清单 5.9（enhancedcheckrange.cpp）中，仅一个 if 语句不足以实现所需的行为。

### 清单 5.9: enhancedcheckrange.cpp

```
#include <iostream>
int main() {
int value;
std::cout << "Please enter an integer value in the range 0...10: ";
std::cin >> value;
if (value >= 0) // First check
if (value <= 10) // Second check
std::cout << value << " is acceptable\n";
else
std::cout << value << " is too large\n";
else
std::cout << value << " is too small\n";
}
```

清单 5.9（enhancedcheckrange.cpp）提供了更具体的消息，而不是简单的接受通知。程序根据变量的值恰好打印三条消息中的一条。单个 if 或 if/else 语句无法从两个以上的不同执行路径中进行选择。

清单 5.10（binaryconversion.cpp）使用一系列 if 语句来打印一个 10 位二进制字符串，表示用户提供的十进制整数的二进制等效值。（第 4.8 节提供了关于二进制数系统的一些背景信息。）我们使用 if/else 语句从左到右打印各个数字，本质上是组装表示二进制数的位序列。

### 清单 5.10: binaryconversion.cpp

```
#include <iostream>

int main() {
  int value;
  // Get number from the user
  std::cout << "Please enter an integer value in the range 0...1023: ";
  std::cin >> value;
  // Integer must be less than 1024
  if (0 <= value && value < 1024) {
    if (value > 512) {
      std::cout << 1;
      value %= 512;
    }
    else {
      std::cout << 0;
      if (value > 256) {
        std::cout << 1;
        value %= 256;
      }
      else {
        std::cout << 0;
        if (value > 128) {
          std::cout << 1;
          value %= 128;
        }
        else {
          std::cout << 0;
          if (value > 64) {
            std::cout << 1;
            value %= 64;
          }
          else {
            std::cout << 0;
            if (value > 32) {
              std::cout << 1;
              value %= 32;
            }
            else {
              std::cout << 0;
              if (value > 16) {
                std::cout << 1;
                value %= 16;
              }
              else {
                std::cout << 0;
                if (value > 8) {
                  std::cout << 1;
                  value %= 8;
                }
                else {
                  std::cout << 0;
                  if (value > 4) {
                    std::cout << 1;
                    value %= 4;
                  }
                  else {
                    std::cout << 0;
                    if (value > 2) {
                      std::cout << 1;
                      value %= 2;
                    }
                    else {
                      std::cout << 0;
                      std::cout << value << "\n";
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

在清单 5.10（binaryconversion.cpp）中：

- 外部 `if` 检查用户提供的值是否在适当范围内。该程序仅适用于小于 1,024 的非负整数值，因此范围是 0-1023。

- 每个内部 `if` 将用户提供的整数与递减的二的幂进行比较。如果数字足够大，程序：
    - 向控制台打印数字 1；以及
    - 通过余数运算符移除该二的幂对值的贡献。
  如果数字不大于等于给定的二的幂，程序改为打印 0 并继续，而不修改输入值。

- 对于末尾的个位不需要检查——剩余值将是 0 或 1，因此程序打印剩余的任何值。

以下是清单 5.10（binaryconversion.cpp）的示例运行：

```
Please enter an integer value in the range 0...1023: 805
1100100101
```

图 5.3 说明了当用户输入 805 时清单 5.10（binaryconversion.cpp）的执行情况。

清单 5.11（simplerbinaryconversion.cpp）以一些额外的算术为代价简化了清单 5.10（binaryconversion.cpp）的逻辑。它只使用一个 `if` 语句。
