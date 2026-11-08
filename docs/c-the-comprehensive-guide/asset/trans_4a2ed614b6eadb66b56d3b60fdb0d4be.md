
-   对于 `const char[]`——例如字面量 `"Text"`——可以转换为 `std::string`（不过，这并不是由编译器提供的，而是由标准库提供的）。

下一个代码清单展示了一些可行的转换以及你可能遇到的问题。不过要注意，类型宽度可能因系统而异，你可能会遇到不同的转换。此外，应当严格避免溢出，因为某些行为可能变得任意（技术术语：*未定义*）。示例输出是在使用 GCC 4.9 的 64 位 Intel Linux 系统上生成的。

```cpp
// https://godbolt.org/z/zbTT7Kr3G
#include <iostream>
#include <format>
void prints(short s, int i, float f, double d) {
    std::cout << std::format("short: {} int: {} float: {:.2f} double: {:.2f}\n",
        s, i, f, d);
}
int main() {
    int mill = 1000*1000;           // 1 Million
    prints(mill, mill, mill, mill); // short overflows
    // Output: short: 16960 int: 1000000 float: 1000000.00 double: 1000000.00
    long bill = 1000L*1000L*1000L*1000L; // 1 Trillion
    prints(bill, bill, bill, bill); // even int overflows, float becomes inaccurate
    // Output: short: 4096 int: -727379968
    // float: 999999995904.00 double: 1000000000000.00
    float three = 3.75f;
    prints(three, three, three, three); // decimal places are lost
    // Output: short: 3 int: 3 float: 3.75 double: 3.75
}
```

**代码清单 7.8** 这里会发生一些转换。在你的系统上，这些转换可能看起来有所不同。

在 `prints(mill,...)` 中，参数 `short s` 在值 1000000（100 万）的转换过程中发生溢出，其内容没有意义。转换为 `float` 或 `double` 没有问题。`format` 自 C++20 起可用；在此之前，你可以使用 `std::cout << s ...`

更大的值 1 万亿也会导致 `prints(bill, ...)` 中的 `int` 溢出。转换为 `float` 确实避免了溢出，但 `float` 没有足够的精度来存储精确值。

任何整数类型（例如 `short` 和 `int`）都无法保存像 3.75f 这样的小数。在 `prints(three, ...)` 中进行转换时，小数部分会被直接截断。不过，float 可以无损转换为 double。反过来则可能丢失信息。

> **展望：自定义类型的转换**
>
> 如果你以后定义自己的类型，就可以自行决定允许哪些与你的类型之间的转换。你可以通过定义构造函数 MyType(A)，将类型 A 转换为你的类型 MyType。而如果在 MyType 中定义方法 operator B()，就可以将 MyType 转换为类型 B。

## 7.8 函数重载

如果你定义了函数

```cpp
void print(int value) {
    std::cout << "int value: " << value;
}
```

但不希望 print(3.75) 输出无意义的 int 值：3，那么你也可以为 double 类型的参数定义 print 函数。如果同名函数被定义多次，就称为重载。

```cpp
// https://godbolt.org/z/9YcPraT15
#include <iostream>
void print(int value) { std::cout << "int value: " << value << ";" }
void print(double value) { std::cout << "double value: " << value << ";" }
void print(int v1, double v2) { std::cout << "Values: " << v1 << ", " << v2 << ";" }
int add(int n, int m) { return n + m; }
double add(double a, double b) { return a + b; }
int main() {
    print(add(3, 4));        // add(int, int) and print(int)
    print(add(3.25f, 1.5f)); // add(double, double) and print(double)
    print(7, 3.25);          // print(int, double)
}
```

**代码清单 7.9** “print”和“add”函数已针对多种类型进行重载。

你可以看到 print 有三个重载。如果用 int 调用它，就会调用 print(int value)；如果用 double 调用，当然会调用 print(double value)。你也可以定义参数个数不同的重载，正如你在第三个 print 变体中所看到的。对 print(7, 3.25) 的调用就符合这一点。

在选择正确的重载时，编译器遵循一些规则。如果参数与某个重载完全匹配，那就简单。但如果某个参数不能完全匹配，编译器就必须做出选择。例如，我写了：

`add(3.25f, 1.5f)`

现在，`3.25f` 和 `1.5f` 是 *float* 字面量；如果我写的是 `3.25` 和 `1.5`，它们就会是 *double* 字面量。不过，编译器选择 `add(double, double)` 变体而不是 `add(int, int)` 显然更好，因为从 float 转换为 double 不会丢失任何东西，而从 float 转换为 int 则不然。

如果你尝试 `print(1.25, 2.75)`，编译器显然既不能选择 `print(int)`，也不能选择 `print(double)`；参数个数根本不匹配。因此，它会调用 `print(int, double)`，并把 `1.25` 转换为 `int`。你会得到输出 `Values: 1, 2.75`。

如果编译器无法通过它能执行的转换找到合适的重载，就会向你报错。

不过，有时编译器会找到多个同样合适或同样不合适重载。在这种情况下，编译器也会给出错误消息，指出重载解析不明确。如果你调用

```cpp
add(4, 2.85);           // ✗ Overloading unclear
```

编译器就无法决定使用 `add(int, int)` 还是 `add(double, double)`。它随后会告诉你，这个调用无法明确解析。

为了避免让你感到意外，需要说明的是：虽然参数类型参与重载解析，但返回类型不参与。对于仅在返回类型上不同的重载，编译器会报错：

```cpp
// https://godbolt.org/z/58cTfVYhe
int two() { return 2; }       // ✗ once with int as return type...
double two() { return 2.0; }  // ✗ ...and once with double
int main() {
    int x = two();
    double y = two();
}
```

不过，如果参数类型可以区分，返回类型也可以不同：

```cpp
// https://godbolt.org/z/evGqC1oqa
int twice(int a) { return a * 2; }
double twice(double a) { return a * 2.0; }
int main() {
    int x = twice(7);
    double y = twice(7.0);
}
```

这在标准库中被广泛使用。例如，容器的 `begin()` 和 `end()` 方法有时返回 *迭代器*，有时返回 *const_iterator*，这取决于（隐式的）this 参数是否用 `const` 标记为不可变。除了参数类型上的 `*` 和 `&` 之外，像 `const` 这样的修饰符也参与重载解析。

还有一点：在为一个函数编写无数重载之前，考虑改用函数模板（见第 23 章）。从 C++20 起，使用形式为 `void func(auto a)` 的缩写函数模板会让这更加容易。

> **重载**
>
> 我在这里只是简要涉及了重载这一主题。我建议你做一些实验，体会一下。尤其是在结合类型转换和默认参数时，C++ 中的函数重载是一项强大且无处不在的特性。如果你掌握了它，你就已经理解了很多。

## 7.9 默认参数

在上一节中，我定义了一个将两个值相加的函数：

```cpp
int add(int n, int m) { return n + m; }
```

如果你想编写一个不仅相加两个值的函数，现在就可以重载它：

```cpp
int add(int n, int m, int o) { return n+m+o; }
int add(int n, int m, int o, int p) { return n+m+o+p; }
int add(int n, int m, int o, int p, int q) { return n+m+o+p+q; }
```

这里你有 `add` 的各种版本，它们允许你一次最多对五个数求和。它们都共享同一个名字 `add`。但是，只写一个函数不是更方便吗？如果你需要超过五种变体，这就更加实用了。

你可以借助 *默认实参* 来实现这一点。只需为参数写出默认值，当你用较少的实参调用它们时，就会使用这些默认值。

```cpp
// https://godbolt.org/z/fjc37rVEr
int add(int n=0, int m=0, int o=0, int p=0, int q=0) {
    return n+m+o+p+q;
}
int main() {
    std::cout << add(1,2,3,4,5) << " ";
    std::cout << add(1,2,3,4) << " "; // like add(1,2,3,4,0)
    std::cout << add(1,2,3) << " ";   // like add(1,2,3,0,0)
    std::cout << add(1,2) << " ";      // like add(1,2,0,0,0)
}
```
