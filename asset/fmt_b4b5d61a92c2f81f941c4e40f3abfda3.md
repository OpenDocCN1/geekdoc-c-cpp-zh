
```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main() {
    // 设置随机种子
    srand(static_cast<unsigned>(time(0)));

    // 掷三次骰子
    for (int i = 0; i < 3; i++) {
        // 生成1到6范围内的随机数
        int value = rand() % 6 + 1;

        // 显示骰子
        cout << "+--------+" << endl;
        switch (value) {
            case 1:
                cout << "|  *   |" << endl;
                cout << "|        |" << endl;
                cout << "+--------+" << endl;
                break;
            case 2:
                cout << "|  *    |" << endl;
                cout << "|    *  |" << endl;
                cout << "+--------+" << endl;
                break;
            case 3:
                cout << "|  *   |" << endl;
                cout << "|  *   |" << endl;
                cout << "+--------+" << endl;
                break;
            case 4:
                cout << "|    *  |" << endl;
                cout << "|    *  |" << endl;
                cout << "+--------+" << endl;
                break;
            case 5:
                cout << "|  *   |" << endl;
                cout << "|  *   |" << endl;
                cout << "|  *   |" << endl; // 注意：此处为简化后的逻辑表示
                cout << "+--------+" << endl;
                break;
            case 6:
                cout << "|  *   |" << endl;
                cout << "|  *   |" << endl;
                cout << "|  *   |" << endl;
                cout << "+--------+" << endl;
                break;
            default:
                cout << "*** Error:非法骰子值 ***" << endl;
                break;
        }
    }
}
```

列表 8.12 (`die.cpp`) 的一次运行输出为

![](img/e326304bd50fbc4f7d5a64c1487eb635_195_0.png)

由于值是伪随机生成的，实际输出在每次运行之间会有所不同。

- C 和 C++ 标准库提供了一系列可以包含到你编写的代码中的例程。
- 当在使用标准库函数或编写自己的代码解决相同问题之间面临选择时，请选择库函数。标准函数经过了充分良好的测试，并且比你编写的代码更高效。
- 该函数是 C++ 中标准的重用单元。

## 8.8. 练习

- 使用函数的代码被称为调用代码（calling code）。
- 函数包含一个名称、参数列表（可能为空）和一个结果类型（可能为 `void`）。函数执行某些对调用者有用的计算或操作。通常，函数会根据传递给它的参数产生结果。
- 调用者通过其参数（也称为实）向函数传递信息。
- 为了使用标准函数，调用者必须 `#include` 相应的头文件。
- 传递给函数的参数可以由括号括起来的逗号分隔列表组成。
- 调用代码（函数定义之外调用函数的代码）必须传递函数期望的正确数量和类型的参数。
- 标准库 `<cmath>` 包含了各种数学函数。
- `<time>` 库中的 `time` 函数返回自 1970 年 1 月 1 日午夜以来的秒数。
- 标准库 `<ctype>` 包含了各种字符处理函数。
- `rand` 函数（来自 `<cstdlib>`）返回一个伪随机整数。第一个伪随机数可以通过 `srand` 函数进行设置。常量 `RAND_MAX` 是 `rand` 返回的最大可能值。

## 8.8 练习

1. 假设你需要在 C++ 程序中计算一个数的平方根。编写执行平方根计算的代码是一个好主意吗？为什么？
2. 在 C++ 源码中，有哪种方法可以帮助区分变量名和函数名？
3. 下列值中哪会被 `rand` 函数计算？

| 4.5 34 -1 @RAND_MAX@ + 1 |

4. `clock_t` 代表什么？
5. `CLOCKS_PER_SEC` 代表什么？
6. 通常情况下程序应该多久调用一次 `srand` 函数？
7. 在列表 8.2 (`standardsqrt.cpp`) 中，当 `sqrt` 函数计算 `main` 提供的参数的平方根时，`main` 函数在做什么？
8. 考虑以下可能作为 C++ 程序部分的代码片段。每个片段都包含对标准 C/C++ 库函数的调用。通过以下三种方式回答每个问题：
    - 如果代码片段包含编译错误，答案写 `error`。
    - 如果代码片段不包含编译错误且你可以在编译时确定输出，请提供该片段的字面输出。
    - 如果代码片段不包含编译错误但你无法在编译时确定精确输出，请提供可能的评估结果并写 *example* 作为答案，同时提供该片段可能产生的一个可能的字面输出。

(a) `cout << sqrt(4.5) << endl;`

(b) `cout << sqrt(4.5, 3.1) << endl;`

(c) `cout << rand(4) << endl;`

```cpp
(d) double d = 16.0;
cout << sqrt(d) << endl;
```

(e) `cout << srand() << endl;`

(f) `cout << rand() << endl;`

```cpp
(g) int i = 16;
cout << sqrt(i) << endl;
```

(h) `cout << srand(55) << endl;`

(i) `cout << tolower('A') << endl;`

(j) `cout << exp() << endl;`

(k) `cout << sqrt() << endl;`

(l) `cout << toupper('E') << endl;`

(m) `cout << toupper('e') << endl;`

(n) `cout << toupper("e") << endl;`

(o) `cout << exp(4.5) << endl;`

(p) `cout << toupper('h'), 5 << endl;`

(q) `cout << isispunct('!') << endl;`

(r) `cout << toupper("F") << endl;`

```cpp
(s) char ch = 'D';
cout << tolower(ch) << endl;
```

(t) `cout << exp(4.5, 3) << endl;`

(u) `cout << toupper('7') << endl;`

(v) `double a = 5, b = 3;

cout << exp(a, b) << endl;`

(w) `cout << exp(3, 5, 2) << endl;`

(x) `cout << tolower(70) << endl;`

(y) `double a = 5;

cout << exp(a, 3) << endl;`

(z) `double a = 5;

cout << exp(3, a) << endl;`

9. 几何题：编写一个计算机程序，给出直角三角形中邻直角的两条边的长度，计算该三角形的斜边长度。（见图 8.6）。如果你不确定如何在数学上解决这个问题，请在网上搜索毕股定理。

![](img/e326304bd50fbc4f7d5a64c1487eb635_198_0.png)

图 8.6：直角三角形

10. 三角函数题：编写一个计算机程序，给出直角三角形中邻直角的两条边的长度，计算该三角形的斜边长度。如果你不确定如何在数学上解决这个问题，请在网上搜索毕股定理。

# 第 9 章

## 9.1 函数基础

回顾我们在列表 8.1 中看到的“手写”平方根代码（`computesquareoot.cpp`）。我们知道更好的选择是标准库函数 `sqrt`；然而，我们将根据 8.1 (`computesquareoot.cpp`) 中的代码编写自己的平方根函数来演示自定义函数的开发。在列表 9.1 (`customsqueroot.cpp`) 中我们看到了 `square_root` 函数的定义。

```cpp
Listing 9.1: customsqueroot.cpp
#include <iostream>
#include <iomanip>
#include <cmath>

using namespace std;

// 计算 x 的平方根的近似值
double square_root(double x) {
    double diff;
    // 计算初步平方根
    double root = 1.0;

    do {
        // 循环直到近似根
        // 足够接近真实的根
        root = (root + x/root) / 2.0;
        cout << "root is " << root << endl;
        // 估计误差有多大？
        diff = root * root - x;
    } while (diff > 0.0001 || diff < -0.0001);
    return root;
}

int main() {
    // 比较两种计算平方根的方法
    for (double d = 1.0; d <= 10.0; d += 0.5) {
        cout << setw(7) << square_root(d) << " : " << sqrt(d) << endl;
    }
}
```

## 9.1. 函数基础

| 1 | 1 |

| 1.22474 | 1.22474 |

| 1.41422 | 1.41421 |

| 1.58116 | 1.58114 |

| 1.73205 | 1.73205 |

| 1.87083 | 1.87083 |

| 2 | 2 |

| 2.21232 | 2.21232 |

| 2.23607 | 2.23607 |

| 2.34521 | 2.34521 |

| 2.44949 | 2.44949 |

| 2.54952 | 2.54951 |

| 2.64577 | 2.64575 |

| 2.73861 | 2.73861 |

| 2.82843 | 2.82843 |

| 2.91548 | 2.91548 |

| 3 | 3 |

| 3.08221 | 3.08221 |

| 3.16228 | 3.16228 |

显示了结果的一些细微差异。显然，我们应该使用标准的 `sqrt` 函数而不是我们自定义的。

每个 C++ 函数都有两个方面：

- **函数定义。** 函数的定义指定了函数的返回类型和参数类型，并提供了决定函数行为的代码。在列表 9.1 (`customsquareroot.cpp`) 中，**`square_root`** 函数的定义出现在 **`main`** 函数上方。
- **函数调用。** 程序员通过函数调用来使用函数。**`main` 函数**调用了我们定义的 **`square_root`** 函数和 **`sqrt`** 函数。每个函数恰好有一个定义，但可能有多次调用。

一个函数定义由四个部分组成：

- **名称 (Name)**——C++ 中的每个函数都有一个名称。该名称是一个标识符（见第 3.3 节）。与变量名一样，函数的名称应该准确地描述其意图或功能。
- **类型 (Type)**——每个函数都有一个返回类型。如果函数向调用者返回一个值，则其类型与它返回的值的类型相对应。特殊的 **`void`** 表示该函数不返回值。
- **参数 (Parameters)**——每个函数必须指定它从调用者处接收的参数。参数出现在括号内的逗号分隔列表中，就像函数原型中所示（见第 8.1 节）。与函数原型不同，参数通常与每个类型有一个联的名称。
- **体 (Body)**——每个函数定义都有一个用大括号包围的体。函数体包含了在被调用时执行的代码。

## 9.1. 函数基础

![](img/e326304bd50fbc4f7d5a64c1487eb635_202_0.png)

图 9.1：函数定义结构解析

9.1 析了一个 `square_root` 函数定义。

最简单的函数不接受参数，也不向调用者返回值。列表 9.2 (`simplefunction.cpp`) 是列表 4.1 (`adder.cpp`) 的变体，其中包含这样一个简单的函数定义。

```cpp
Listing 9.2: simplefunction.cpp
#include <iostream>

using namespace std;

// prompt 函数定义
void prompt() {
    cout << "Please enter an integer value: ";
}

int main() {
    int value1, value2, sum;
    cout << "This program adds two integers." << endl;
    // 调用函数
    prompt();
    cin >> value1;
    prompt();    // 再次调用函数
    cin >> value2;
    sum = value1 + value2;
    cout << value1 << " + " << value2 << " = " << sum << endl;
}
```

## 9.1. 函数基础

```cpp
}
```

**`prompt`** 函数简单地打印一条消息。程序的运行如下：

1. 程序的执行（与所有 C++ 程序一样）从名为 **`main`** 的函数中的第一个可执行语句开始。**`main`** 函数中的第一行声明了编译器内部工作所需的一些变量，因此下一行实际上开始了可执行代码。
2. 第一个可执行语句打印了程序的意图消息。
3. 下一个语句是对 **`prompt`** 函数的调用。此时，程序的执行转移到 **`prompt`** 函数的体。**`prompt`** 内部的代码一直执行，直到体结束或遇到 **`return`** 语句。由于 **`prompt`** 不包含 **`return`** 语句，**`prompt`** 的所有体（那条打印语句）都将被执行。
4. 当 **`prompt`** 完成后，控制将传回到 **`main`** 中调用 **`prompt`** *之后* 的点。
5. **`prompt`** 调用后的下一个动作是从键盘读取 `value1` 的值。
6. 第二次调用 **`prompt`** 将控制传回 **`prompt`** 函数内部的代码。它再次打印它的消息。
7. 当第二次调用 **`prompt`** 完成后，控制传回 **`main`**，在从键盘赋值 `value2` 的第二个输入语句处。
8. 剩余两个简单示例执行完毕，然后程序结束。

作为另一个例子，考虑 9.3：

```cpp
Listing 9.3: count10.cpp
#include <iostream>

using namespace std;

void count10(int n) {
    for (int i = 1; i <= n; i++) {
        cout << i << endl;
    }
}

int main() {
    count10(10);
    return 0;
}
```

## 9.1. 函数基础

`val value = prompt();`

将 `return` 语句执行时指定的值赋给变量 `value`。

请注意，在列表 9.6 (`betterprompt.cpp`) 中，我们在 `prompt` 内部声明了一个变量名 `result`。该变量是函数局部的，意味着我们无法在 `prompt` 外部使用这个特定的变量。这意味着我们可以在不同的上下文中自由在 `prompt` 函数之外使用相同的名称，这不会干扰 `prompt` 内部的 `result` 变量。我们称 `result` 为一个局部变量。

我们可以进一步增强 `prompt` 函数。目前，`prompt` 总是发送相同的消息。通过使用参数，我们可以自定义打印的消息。列表 9.7 (`evenprompt.cpp`) 展示了如何使用参数在 `prompt` 中提供自定义的消息。
