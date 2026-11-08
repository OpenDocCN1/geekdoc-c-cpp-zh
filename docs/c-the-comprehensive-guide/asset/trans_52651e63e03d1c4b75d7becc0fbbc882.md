

## 7.3 使用函数

在我们进一步深入探讨如何自己编写函数之前，先来看看函数的使用方法。

```cpp
// https://godbolt.org/z/TdrebYodx
#include <iostream>                 // cout
#include <cmath>                    // sin
#include <string>
#include <vector>
using std::sin;
int main() {
    std::cout << "sin(0.0): " << sin(0.0) << "\n";        // call sin() with literal
    double angle = 3.1415/2;
    std::cout << "sin(" << angle << "): " << sin(angle) << "\n"; // call with variable
    std::string name = "Han Solo";
    std::cout << name.length() << "\n"; // call a method
                                      // ... conceptually like length(name)
    std::vector<int> data{};
    data.push_back(5);                 // further method call with parameter
    data.push_back(10);
    std::cout << data.back() << " ";
    data.pop_back();
    std::cout << data.back() << "\n";
    data.pop_back();
}
```

**代码清单 7.1** 使用函数。

函数 *sin()* 被调用了一次，传入字面量 0.0——字面量也是常量值——另一次传入变量 angle。正如你对数学函数 *sin* 的预期，这里返回的是计算结果。

可以看到，我用来调用 *sin()* 的变量是 double 类型。这很合适，因为在标准库中，该函数声明为 double sin(double)：它接受一个 double，也返回一个 double。调用时参数类型必须彼此匹配：你不能调用 sin("Han Solo")，因为 sin() 并不用于字符串。存在会发生转换的例外情况；你将会了解它们，并自己编写其中一些。

注意，我这里还展示了*方法*调用，例如 name.length() 和 data.push_back(5)。主要区别在于，像 sin() 这样的函数是“自由”的（一个*自由函数*），而 length() 则与 std::string 类紧密关联。当你使用 *variable.functionname* 调用函数时，这就是*方法*的特殊形式。这个术语来自面向对象，将在类那一章详细讨论（见*第 12 章*）。

此处。如果你只是在此声明函数（而不是*定义*它），或者函数中根本不使用该参数，那么可以省略它。不过，我建议使用清晰、描述性的名称，使函数头变得有意义。

- **函数体**  
  函数体（连同其外围的花括号）由语句组成：没有语句、一条语句或多条语句，随你决定。如果函数有返回值，那么这里至少必须有一条 return 语句。

```cpp
int func();                         // returns an int
std::string func();                 // a string from the standard library
void func();                        // no return value
std::pair<int,std::string> func();  // composite type from the stdlib
vector<int> func();                 // returns a new container
vector<int>& func();                // reference to some container
const vector<int>& func();          // same, but you cannot change it
```

**代码清单 7.2** 函数的不同返回类型。

> **C++20：简写函数模板**
>
> 自 C++20 起，你可以使用 `auto` 作为参数类型。这样你就能定义函数模板，而无需使用 `template` 和尖括号这种繁琐的表示法。编译器会将
>
> ```cpp
> void func(auto a) { ... }
> ```
>
> 转换为
>
> ```cpp
> template<typename A> void func(A a) { ... }
> ```
>
> 你可以在 [第 23 章] 中阅读更多关于模板的内容。我在这里提到它，是因为一方面，这种写法并不显式暴露模板；另一方面，它为编写通用而紧凑的代码提供了很好的机会。

## 7.5 关于参数的更多内容

在 C++ 中，函数头中参数的声明决定了参数在调用时的行为方式。最重要的区别在于参数是按*值*传递还是按*引用*传递。

### 7.5.1 按值调用

如果不采取任何特殊措施，C++ 中函数的参数会按*值（按值调用）*传递。这意味着，如果变量 x 当前值为 5，而你把 x 传给一个函数，那么进入函数的是 5——而不是 x。

```cpp
// https://godbolt.org/z/8zcVMdM3b
#include <iostream>

void print_val8(int n) {          // parameter as value
    std::cout << n << " ";
    n = 8;                        // sets parameter to 8
    std::cout << n << "\n";
}

int main() {
    int x = 5;
    print_val8(x);                // x as value: prints 5, then 8
    std::cout << x << "\n";       // x remains unchanged at 5
    print_val8(42);               // 42 as value: prints 42, then 8
}
```

**代码清单 7.3** 参数最初按值传递。

当调用 `print_val8` 时，编译器会将实参的_值_复制到函数的 `n` 位置。因此，`n = 8` 处的修改不会影响最初用来调用 `print_val8(x)` 的变量 `x`。

> **带指针结构体的按值传递**
>
> 此时我必须提醒你，当（尤其是）与指针交互时，情况会变得稍微复杂一些。如果指针 `*` 是你按值传递的结构体或类的一部分，那么该结构体中只复制了指针，而不是它指向的内容。这意味着，如果你改变了指针所指向的内容，你也会改变原始对象。

### 7.5.2 按引用调用

如果你希望赋值影响外部变量，那么在 C++ 中需要以这样的方式声明函数：让它将参数接收为引用（按引用调用）。为此，请使用与号 `&`。

在向你展示有意义的用法之前，我会先修改前面的示例以作比较。

```cpp
// https://godbolt.org/z/63dTshz3Y
#include <iostream>
void print_ref8(int& n) {         // parameter as reference
    std::cout << n << " ";
    n = 8;                        // sets parameter to 8
    std::cout << n << "\n";
}

int main() {
    int x = 5;
    print_ref8(x);              // x as reference: prints 5, then 8
    std::cout << x << "\n";     // x is now 8
}
```

**代码清单 7.4** 添加与号使其成为引用参数。

函数 `print_ref8` 与前一个清单中的 `print_val8` 完全对应，不同之处在于本示例中 `print_ref8` 的参数用 & 声明为引用——即 `int& n`。因此，在 `main()` 中调用 `print_ref8(x)` 时，编译器不会将 `x` 的值复制到函数中，而是将 `x` 本身作为引用传递；在函数内部，随后用参数名 `n` 来指代它。这样，你可以从完全不同的程序位置调用 `print_ref8`，并传入完全不同的变量；在 `print_ref8` 内部，它们始终被称为 `n`。

还有另一个区别：你不能使用 `print_ref8(42)`。你能看出原因吗？在 `print_ref8` 内部，42 会被名称 `n` 指代——而且随后在 `print_ref8` 中会执行 `n = 8` 赋值。这意味着它会变成 42 = 8，而这显然是不可能的。然而，编译器不仅在赋值 `n = 8` 处阻止这一点，在调用 `print_ref8(42)` 处也会阻止：参数类型是 `int&`（读作“对 int 的引用”）而不是 `int`，编译器无法以这种方式引用 42；42 与 `int&` 不兼容，编译器会报错。

### 7.5.3 常量引用

要将 `x` 和 `42` 都传递给一个以引用为参数的函数，你必须向编译器“承诺”不会给该引用赋任何值。使用 `const int& n`，你告诉编译器 `n` 在函数内部是常量。

```cpp
// https://godbolt.org/z/dckXn3pO
#include <iostream>
void print_cref(const int& n) {  // parameter as constant reference
    std::cout << n << " ";
}

int main() {
    int x = 5;
    print_cref(x);              // call with a variable
    print_cref(42);             // call with a constant literal
}
```

**代码清单 7.5** 你可以将常量引用用作任何调用的参数。

