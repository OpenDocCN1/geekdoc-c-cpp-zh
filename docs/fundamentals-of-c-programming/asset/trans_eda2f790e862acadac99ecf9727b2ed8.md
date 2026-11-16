

在清单 10.3 (counter.cpp) 中，count 函数被调用了 10 次。每次调用都会返回它被调用次数的统计：

```
1 2 3 4 5 6 7 8 9 10
```

相比之下，如果从清单 10.3 (counter.cpp) 中删除单词 `static`，然后重新编译并重新运行，它将打印：

```
1 1 1 1 1 1 1 1 1 1
```

因为每次调用 `count` 时，都会为变量 `cnt` 分配新内存。

局部声明

```
static int cnt = 0;
```

为 `cnt` 分配空间，并在程序执行开始时只将其赋值为零一次。为 `cnt` 预留的空间在程序执行结束前不会被释放。

回顾清单 9.7 (evenbetterprompt.cpp)，其中包含了以下函数：

```
int prompt(int n) {
    int value;
    std::cout << "Please enter integer #" << n << ": ";
    std::cin >> value;
    return value;
}
```

调用者 main 使用 prompt 函数的方式如下：

```
int value1, value2, sum;
std::cout << "This program adds together two integers.\n";
value1 = prompt(1); // Call the function
value2 = prompt(2); // Call the function again
sum = value1 + value2;
```

第一次调用 prompt 会打印消息

```
Please enter integer #1:
```

并等待用户输入。第二次调用会打印消息

```
Please enter integer #2:
```

另一个调用者可能在循环中这样使用 prompt：

```
int sum = 0;
for (int i = 1; i < 10; i++)
    sum += prompt(i);
```

请注意，跟踪应传递给 prompt 的正确编号是调用者的责任。调用者可能会出错并传递错误的编号，或者可能不想管理此类细节。将跟踪输入计数的责任移交给 prompt 会更好。`static` 变量使这成为可能，如清单 10.4 (promptwithstatic.cpp) 所示。

```
#include <iostream>
/*
 * prompt requests an integer from the user and
 * keeps track of the cumulative number of entries.
 *
 * Returns the value entered by the user.
 */
int prompt() {
    static int count = 0;
    int value;
    std::cout << "Please enter integer #" << ++count << ": ";
    std::cin >> value;
    return value;
}

int main() {
    int value1, value2, sum;
    std::cout << "This program adds together two integers.\n";
    value1 = prompt(); // Call the function
    value2 = prompt(); // Call the function again
    sum = value1 + value2;
    std::cout << value1 << " + " << value2 << " = " << sum << "\n";
}
```

清单 10.4 (promptwithstatic.cpp) 的行为与清单 9.7 (evenbetterprompt.cpp) 完全相同，但在新版本中，main 不需要跟踪用户输入的次数。

局部静态变量继承自 C 编程语言，但随着 C++ 中对象的引入，其需求已有所减少（参见第 14 章）。带有静态变量的函数提供了一种实现具有持久状态的可执行代码的方法。对象提供了一种更自然、更灵活的方式来实现相同的效果。

## 10.3 重载函数

在 C++ 中，一个程序可以有多个同名函数。当程序中有两个或多个函数同名时，该函数被认为是重载的。这些函数必须以某种方式不同，否则编译器将无法知道如何将调用与特定的函数定义关联起来。编译器不仅通过函数名来识别函数；函数由其签名唯一标识。函数签名由函数名及其参数列表组成。在参数列表中，只有形式参数的类型重要，而不重要它们的名称。如果参数类型在数量和位置上都不完全匹配，则函数签名不同。请考虑以下重载函数：

- 1. void f() { /* ... */ }

此版本没有参数，因此其签名与所有其他版本（每个版本至少有一个参数）不同。

- 2. void f(int x) { /* ... */ }

此版本与版本 3 不同，因为其单个参数是 `int`，而不是 `double`。

```
3. void f(double x) { /* ... */ }
```

此版本与版本 2 不同，因为其单个参数是 `double`，而不是 `int`。

```
4. void f(int x, double y) { /* ... */ }
```

此版本与版本 5 不同，因为尽管版本 4 和 5 具有相同数量的参数且类型相同，但类型的顺序不同。

```
5. void f(double x, int y) { /* ... */ }
```

请参见版本 4 的注释。

重载函数为程序员提供了便利。如果不允许重载函数（许多编程语言不支持函数重载），则必须为执行基本相同任务但接受不同参数类型的不同函数创建新函数名。程序员最好为相似的函数选择相同的名称，并让编译器正确解决差异。对于构造函数（在对象创建期间调用的特殊函数，第 14 章），重载成为一个更重要的问题。

## 10.4 默认参数

我们可以定义接受可变数量参数的函数。请考虑清单 10.5 (countdown.cpp)，它指定了一个倒计时函数：

```
Listing 10.5: countdown.cpp

#include <iostream>

// Prints a count down from n to zero. The default
// starting value is 10.
void countdown(int n=10) {
  while (n > 0) // Count down from n to zero
    std::cout << n-- << '\n';
}

int main() {
  countdown(5);
  std::cout << "-------------" << '\n';
  countdown();
}
```

`countdown` 函数中表示为 `n=10` 的形式参数代表默认参数或默认实参。如果调用者未提供实际参数，则形式参数 `n` 被赋值为 10。以下调用

```
countdown()
```

打印

```
10
9
8
7
6
5
4
3
2
1
0
```

但调用

```
countdown(5)
```

显示

```
5
4
3
2
1
0
```

可以看出，当调用者未提供函数指定的参数，且该参数具有默认值时，调用期间将使用默认值。

我们可以在函数声明的参数列表中混合非默认参数和默认参数，但参数列表中的所有默认参数必须出现在所有非默认参数之后。这意味着以下定义是可接受的：

```
int sum_range(int n, int m=100) { // OK, default follows non-default
    int sum = 0;
    for (int val = n; val <= m; val++)
        sum += val;
    return val;
}
```

和

```
int sum_range(int n=0, int m=100) { // OK, both default
    int sum = 0;
    for (int val = n; val <= m; val++)
        sum += val;
    return val;
}
```

但以下定义是非法的，因为默认参数在函数的参数列表中位于非默认参数之前：

```
int sum_range(int n=0, int m) { // Illegal, non-default follows default
    int sum = 0;
    for (int val = n; val <= m; val++)
sum += val;
return val;
}
```

默认参数允许程序员提供高度可调的函数，为其典型用途提供更简单的接口。

重载（参见第 10.3 节）使程序员能够为两个同名的不同函数编写不同的函数定义。混合重载和默认参数可能会产生编译器不允许的歧义；例如，以下重载函数是可接受的：

```
void f() { /* ... */ }
void f(int n) { /* ... */ }
```

因为这重载了函数 f。如果调用者以 f() 调用 f，编译器将生成机器语言代码来调用 f 的第一个版本。如果我们尝试将 f 重载为

```
void f() { /* ... */ }
void f(int n=0) { /* ... */ }
```

编译器无法确定调用 f() 是指第一个重载版本还是参数默认为零的第二个版本。由于这种歧义，编译器会对尝试以无参数调用函数 f 的行为报告错误。另一种可能的组合是非法的：

```
void f(int m) { /* ... */ }
void f(int n=0) { /* ... */ }
```

因为这些函数具有相同的签名 f(int)。C++ 不允许程序包含具有相同签名的多个函数定义。

## 10.5 递归

阶乘函数在组合分析（数学中的计数理论）、概率论和统计学中广泛使用。n 的阶乘通常表示为 n!。阶乘对非负整数定义如下

n! = n · (n - 1) · (n - 2) · (n - 3) · ... 2 · 1

并且 0! 被定义为 1。因此 6! = 6 · 5 · 4 · 3 · 2 · 1 = 720。数学家以这种方式精确定义阶乘：

n! = {
     1 if n = 0
     (n - 1)! otherwise.

此定义是递归的，因为 ! 函数正在被定义，但 ! 也用于定义中。C++ 函数也可以递归定义。清单 10.6 (factorialtest.cpp) 包含一个阶乘函数，它精确模拟了数学定义。

### 清单 10.6: factorialtest.cpp

```
#include <iostream>

/*
 * factorial(n)
```

