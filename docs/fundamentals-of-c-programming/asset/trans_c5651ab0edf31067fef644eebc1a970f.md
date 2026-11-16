
## 清单 8.12: die.cpp

```
#include <iostream>
#include <cstdlib>
#include <ctime>

int main() {
  // Set the random seed value
  srand(static_cast<unsigned>(time(0)));

  // Roll the die three times
  for (int i = 0; i < 3; i++) {
    // Generate random number in the range 1..6
    int value = rand() % 6 + 1;

    // Show the die
    std::cout << " +-------+\n";
    switch (value) {
      case 1:
        std::cout << " |\n";
        std::cout << " * |\n";
        std::cout << " |\n";
        break;
      case 2:
        std::cout << " * |\n";
        std::cout << " |\n";
        std::cout << " * |\n";
        break;
      case 3:
        std::cout << " * |\n";
        std::cout << " * |\n";
        std::cout << " * |\n";
        break;
      case 4:
        std::cout << " * * |\n";
        std::cout << " |\n";
        std::cout << " * * |\n";
        break;
      case 5:
        std::cout << " * * |\n";
        std::cout << " * |\n";
        std::cout << " * * |\n";
        break;
      case 6:
        std::cout << " * * * |\n";
        std::cout << " |\n";
        std::cout << " * * * |\n";
        break;
      default:
        std::cout << " *** Error: illegal die value ***\n";
        break;
    }
    std::cout << " +-------+\n";
  }
}
```

## 8.7 练习

- 1. 假设你需要在 C++ 程序中计算一个数的平方根。编写代码来执行平方根计算是个好主意吗？为什么或为什么不？

- 2. 在 C++ 源代码中，有什么方法可以帮助你区分变量名和函数名？

- 3. 以下哪个值可能由 rand 函数计算得出？
  - 4.5   34   -1   RAND_MAX + 1

- 4. clock_t 表示什么？

- 5. CLOCKS_PER_SEC 表示什么？

- 6. 通常，程序应该多久调用一次 srand 函数？

- 7. 在清单 8.2 (standardsquareroot.cpp) 中，当 sqrt 函数计算 main 提供的参数的平方根时，main 函数在做什么？

- 8. 考虑以下每个可能成为 C++ 程序一部分的代码片段。每个片段都包含对标准 C/C++ 库函数的调用。以以下三种方式之一回答每个问题：
  - 如果代码片段包含编译时错误，请将答案写为单词 error。
  - 如果代码片段不包含编译时错误且你可以在编译时确定其输出，请提供片段的字面输出。
  - 如果代码片段不包含编译时错误但你无法在编译时确定其确切输出，请提供一个可能的求值，并将答案写为单词 example，并提供代码片段可能产生的一个可能的字面输出。
  - (a) std::cout << sqrt(4.5) << '\n';
  - (b) std::cout << sqrt(4.5, 3.1) << '\n';
  - (c) std::cout << rand(4) << '\n';
  - (d) double d = 16.0;
    std::cout << sqrt(d) << '\n';
  - (e) std::cout << srand() << '\n';
  - (f) std::cout << rand() << '\n';
  - (g) int i = 16;
    std::cout << sqrt(i) << '\n';
  - (h) std::cout << srand(55) << '\n';
  - (i) std::cout << tolower('A') << '\n';
  - (j) std::cout << exp() << '\n';
  - (k) std::cout << sqrt() << '\n';
  - (l) std::cout << toupper('E') << '\n';
  - (m) std::cout << toupper('e') << '\n';
  - (n) std::cout << toupper("e") << '\n';
  - (o) std::cout << exp(4.5) << '\n';
  - (p) std::cout << toupper('h', 5) << '\n';
  - (q) std::cout << ispunct('!') << '\n';
  - (r) std::cout << tolower("FF") << '\n';
  - (s) char ch = 'D';
    std::cout << tolower(ch) << '\n';
  - (t) std::cout << exp(4.5, 3) << '\n';
  - (u) std::cout << toupper('7') << '\n';
  - (v) double a = 5, b = 3;
    std::cout << exp(a, b) << '\n';
  - (w) `std::cout << exp(3, 5, 2) << '\n';`
  - (x) `std::cout << tolower(70) << '\n';`
  - (y) `double a = 5;
    std::cout << exp(a, 3) << '\n';`
  - (z) `double a = 5;
    std::cout << exp(3, a) << '\n';`

## 图 8.6 直角三角形

![](img/e84ad11adb18201d71595b31ce6c9eff_210_0.png)

- 9. 从几何角度：编写一个计算机程序，给定直角三角形直角两边的长度，计算该三角形斜边的长度。（参见图 8.6。）如果你不确定如何在数学上解决这个问题，请进行网络搜索以了解勾股定理。

## 第 9 章

## 编写函数

随着程序变得越来越复杂，程序员必须以这种方式构建他们的程序，以便有效地管理其复杂性。大多数人很难一次跟踪太多信息。很容易在复杂问题的细节中陷入困境。管理复杂性的诀窍是将问题分解为更易于管理的部分。每个部分都有必须处理的自身细节，但这些细节尽可能在该部分内部被隐藏。问题最终通过将这些部分组合在一起形成完整的解决方案来解决。

迄今为止，我们的所有程序都已编写在一个函数——main 中。随着函数内语句数量的增加，该函数可能变得难以处理。在这样的函数中，自己完成所有工作的代码称为单体代码。冗长且复杂的单体代码因多种原因不受欢迎：

- 编写正确比较困难。在编写该代码中的任何语句时，都必须考虑整段代码中的所有细节。

- 调试比较困难。如果代码序列无法正确工作，通常很难找到错误的来源。代码中较早出现的错误语句的影响可能要等到后面的正确语句使用该错误语句的错误结果时才会显现出来。

- 扩展比较困难。在修改之前，必须充分理解整个代码序列中的所有细节。如果代码复杂，这可能是一项艰巨的任务。

使用分治策略，程序员可以将一个复杂的函数（如 main）分解为几个更简单的函数。然后，原始函数可以通过将工作委托给这些其他函数来完成其工作。这样一来，原始函数可以被视为“工作协调者。”

除了代码组织方面，函数还允许我们将功能打包成可重用的部分。在第 8 章中，我们了解到库函数可以大大增强程序的功能。虽然我们应该尽可能利用库函数，但有时我们需要一个表现出自定义行为且没有任何标准函数提供的函数。幸运的是，我们可以创建自己的函数，并且同一个函数可以在程序的多个位置中使用（调用）。如果函数的目的足够通用且我们正确编写该函数，我们可能还能在其他程序中重用该函数。

### 9.1 函数基础

回顾我们在清单 8.1 (computesquareroot.cpp) 中看到的“手写”平方根代码。我们知道更好的选择是标准库函数 sqrt；然而，我们将通过基于清单 8.1 (computesquareroot.cpp) 中的代码编写自己的平方根函数来说明自定义函数开发。在清单 9.1 (customsquareroot.cpp) 中，我们看到了 square_root 函数的定义。

```
Listing 9.1: customsquareroot.cpp

#include <iostream>
#include <iomanip>
#include <cmath>

// Compute an approximation of
// the square root of x
double square_root(double x) {
    double diff;
    // Compute a provisional square root
    double root = 1.0;

    do { // Loop until the provisional root
        // is close enough to the actual root
        root = (root + x/root) / 2.0;
        //std::cout << "root is " << root << '\n';
        // How bad is the approximation?
        diff = root * root - x;
    } while (diff > 0.0001 || diff < -0.0001);

    return root;
}

int main() {
    // Compare the two ways of computing the square root
    for (double d = 1.0; d <= 10.0; d += 0.5)
        std::cout << std::setw(7) << square_root(d) << " : " << sqrt(d) << '\n';
}
```

清单 9.1 (customsquareroot.cpp) 中的 main 函数将我们自定义的 square_root 函数与 sqrt 库函数的行为进行比较。其输出：

```
1 : 1
1.22474 : 1.22474
1.41422 : 1.41421
1.58116 : 1.58114
1.73205 : 1.73205
1.87083 : 1.87083
2 : 2
2.12132 : 2.12132
2.23607 : 2.23607
2.34521 : 2.34521
2.44949 : 2.44949
2.54952 : 2.54951
2.64577 : 2.64575
2.73861 : 2.73861
2.82843 : 2.82843
2.91548 : 2.91548
```
