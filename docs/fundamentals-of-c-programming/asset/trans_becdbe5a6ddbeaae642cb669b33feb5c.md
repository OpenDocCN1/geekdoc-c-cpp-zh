

std::cin >> input;
// Report square root
std::cout << "Square root of " << input << " = "
<< square_root(input) << '\n';
}

清单 9.24（squarerootfunction.cpp）是否比清单 8.2（standardsquareroot.cpp）更好，后者使用 cmath 库中的标准 sqrt 函数？一般来说，如果你可以选择使用标准库函数或编写提供相同功能的自定义函数，请选择使用标准库例程。使用标准库例程的优势包括：

- 编写自定义代码的工作被完全消除；你可以将更多精力投入到应用程序开发的其他部分。
- 如果你编写自己的自定义代码，必须对其进行彻底测试以确保其正确性；标准库代码虽然不能免疫错误，但通常已经过完整测试套件的检验。库代码被许多开发者使用，因此任何潜在错误通常会早期暴露；你的代码仅由你编写的程序使用，错误可能不会立即显现。如果你的程序没有被广泛受众使用，错误可能会长期潜伏。标准库例程广为人知且值得信赖；自定义代码由于曝光有限，在获得更广泛的曝光和采用之前是可疑的。
- 标准例程通常经过调优以实现高效；要使自定义代码高效需要付出大量努力。
- 标准例程文档齐全；记录自定义代码需要额外工作，编写良好的文档是艰苦的工作。

清单 9.25（squarerootcomparison.cpp）在 1,000,000,000 个浮点数值范围内测试了我们的自定义平方根函数。

```
Listing 9.25: squarerootcomparison.cpp
#include <iostream>
#include <cmath>
// Consider two floating-point numbers equal when
// the difference between them is very small.
bool equals(double a, double b, double tolerance) {
return a == b || fabs(a - b) < tolerance;
}
double square_root(double x) {
// Compute a provisional square root
double root = 1.0;
do { // Loop until the provisional root
// is close enough to the actual root
root = (root + x/root) / 2.0;
} while (!equals(root*root, x, 0.0001));
return root;
}

int main() {
    for (double d = 0.0; d < 100000.0; d += 0.0001) {
        if (!equals(square_root(d), sqrt(d), 0.001))
            std::cout << d << ": Expected " << sqrt(d) << ", but computed "
                << square_root(d) << "\n";
    }
}
```

清单 9.25（squarerootcomparison.cpp）使用了来自清单 9.17（floatequals.cpp）的 equals 函数。第三个参数指定容差；如果前两个参数之间的差小于指定容差，则认为前两个参数相等。我们的新自定义 square_root 函数使用 equals 函数。main 函数也使用 equals 函数。然而，请注意，平方根计算中使用的容差比 main 用于检查结果的容差更小。因此，main 函数使用较不严格的相等性概念。

清单 9.25（squarerootcomparison.cpp）的输出：

```
0: Expected 0, but computed 0.0078125
0.0001: Expected 0.01, but computed 0.0116755
0.0008: Expected 0.0282843, but computed 0.0298389
0.0009: Expected 0.03, but computed 0.0313164
0.001: Expected 0.0316228, but computed 0.0327453
```

表明我们的自定义平方根函数对五个值产生的结果超出了 main 可接受的容差。十亿次测试中有五个错误答案，代表 0.0000005% 的错误率。虽然这个错误率非常小，但表明我们的 square_root 函数并不完美。导致函数失败的值之一可能对特定应用非常重要，因此我们的函数不可信。

## 9.8 练习

- 1. 以下是合法的 C++ 程序吗？

```
int proc(int x) {
    return x + 2;
}
```

```
int proc(int n) {
    return 2*n + 1;
}
```

```
int main() {
    int x = proc(5);
}
```

- 2. 以下是合法的 C++ 程序吗？

```
int proc(int x) {
    return x + 2;
}
```

```
int main() {
    int x = proc(5),
     y = proc(4);
}
```

- 3. 以下是合法的 C++ 程序吗？

```
#include <iostream>

void proc(int x) {
    std::cout << x + 2 << '\n';
}

int main() {
    int x = proc(5);
}
```

- 4. 以下是合法的 C++ 程序吗？

```
#include <iostream>

void proc(int x) {
    std::cout << x + 2 << '\n';
}

int main() {
    proc(5);
}
```

- 5. 以下是合法的 C++ 程序吗？

```
#include <iostream>

int proc(int x, int y) {
    return 2*x + y*y;
}

int main() {
    std::cout << proc(5, 4) << '\n';
}
```

- 6. 以下是合法的 C++ 程序吗？

```
#include <iostream>

int proc(int x, int y) {
    return 2*x + y*y;
}

int main() {
    std::cout << proc(5) << '\n';
}
```

- 7. 以下是合法的 C++ 程序吗？

```
#include <iostream>

int proc(int x) {
    return 2*x*x;
}

int main() {
    std::cout << proc(5, 4) << '\n';
}
```

- 8. 以下是合法的 C++ 程序吗？

```
#include <iostream>

proc(int x) {
    std::cout << 2*x*x << '\n';
}

int main() {
    proc(5);
}
```

- 9. 程序员期望以下程序打印 200。它实际上打印什么？为什么打印这个？

```
#include <iostream>

void proc(int x) {
    x = 2*x*x;
}

int main() {
    int num = 10;
    proc(num);
    std::cout << num << '\n';
}
```

- 10. 由于变量 x 在两个不同的位置（proc 和 main）中使用，该程序是否合法？为什么或为什么不？

```
#include <iostream>

int proc(int x) {
    return 2*x*x;
}

int main() {
    int x = 10;
    std::cout << proc(x) << '\n';
}
```

- 11. 由于实际参数与形式参数名称不同（y 与 x），该程序是否合法？为什么或为什么不？

```
#include <iostream>

int proc(int x) {
    return 2*x*x;
}

int main() {
    int y = 10;
    std::cout << proc(y) << '\n';
}
```

- 12. 完成在第 9.6 节中开始的 distance 函数。使用几个点坐标测试它，以确信你的实现是正确的。

- 13. 如果调用者向函数传递了过多参数，会发生什么？

- 14. 如果调用者向函数传递了过少参数，会发生什么？

- 15. 在 C++ 中命名函数的规则是什么？

- 16. 考虑以下函数定义：

```
#include <iostream>

int fun1(int n) {
    int result = 0;
    while (n) {
        result += n;
        n--;
    }
    return result;
}
```

```
void fun2(int stars) {
    for (int i = 0; i < stars; i++)
        std::cout << "*";
    std::cout << '\n';
}
```

```
double fun3(double x, double y) {
    return 2*x*x + 3*y*y;
}
```

```
bool fun4(char ch) {
    return ch >= 'A' && ch <= 'Z';
}
```

```
bool fun5(int a, int b, int c) {
    return (a <= b) ? (b <= c) : false;
}
```

```
int fun6() {
    return rand() % 2;
}
```

检查以下每个打印语句。如果语句非法，解释为什么非法；否则，指出该语句将打印什么。

- (a) std::cout << fun1(5) << '\n';
- (b) std::cout << fun1() << '\n';
- (c) std::cout << fun1(5, 2) << '\n';
- (d) std::cout << fun2(5) << '\n';
- (e) fun2(5);
- (f) std::cout << fun3(5, 2) << '\n';
- (g) std::cout << fun3(5.0, 2.0) << '\n';
- (h) std::cout << fun3('A', 'B') << '\n';
- (i) std::cout << fun3(5.0) << '\n';
- (j) std::cout << fun3(5.0, 0.5, 1.2) << '\n';
- (k) std::cout << fun4("T") << '\n';
- (l) std::cout << fun4('t') << '\n';
- (m) std::cout << fun4(5000) << '\n';
- (n) fun4(5000);
- (o) std::cout << fun5(2, 4, 6) << '\n';
- (p) std::cout << fun5(4, 2, 6) << '\n';
- (q) std::cout << fun5(2, 2, 6) << '\n';
- (r) std::cout << fun5(2, 6) << '\n';
- (s) if (fun5(2, 2, 6))
    std::cout << "Yes\n";
else
    std::cout << "No\n";
- (t) std::cout << "No\n";
- (u) std::cout << fun6(4) << '\n';
- (v) std::cout << fun3(fun1(3), 3) << '\n';
- (w) std::cout << fun3(3, fun1(3)) << '\n';
- (x) std::cout << fun1(fun1(fun1(3))) << '\n';
- (y) std::cout << fun6(fun6()) << '\n';

