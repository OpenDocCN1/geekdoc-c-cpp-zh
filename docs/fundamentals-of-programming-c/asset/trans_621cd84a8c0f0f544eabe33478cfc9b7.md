

## 7.5 总结

用于立即检查以确定迭代是否继续的条件，而 `goto` 跳转到函数中某处的标签。然而如前所述，`for` 循环的控制应限制在其头部，并应避免在 `for` 循环内部使用 `break`、`continue` 和 `goto`。任何 `for` 循环都可以重写为 `while` 循环且行为完全相同。例如，考虑 `for` 循环：

```cpp
for (int i = 1; i < 10; i++)
cout << i << endl;
```

再考虑 `while` 循环的行为完全相同：

```cpp
int i = 1;
while (i <= 10) {
  cout << i << endl;
  i++;
}
```

哪个更好？`for` 循环方便地将循环控制信息封装在其头部，但在 `while` 循环中，信息分布在整个小段代码中。`for` 循环提供了更好的循环控制组织。其中一个性能优于另一个吗？不，大多数编译器为这两种结构产生本质相同的代码。因此，在示例中优选 `for` 循环。

## 7.5 总结

- `switch` 语句是多路 if/else 语句的替代方案。
- 并非所有多路 if/else 语句都可以直接转换为 `switch` 语句。
- 在 `switch` 语句内求值的表达式必须求出一个整数值（int、short、long、char 或 bool）。
- `switch` 语句中的 `case` 必须是整型字面量或常量（int、short、long、char 或 bool）。具体而言，`case` 标签可以是变量或其他表达式。
- 程序执行跳转到与 `switch` 表达式值匹配的 `case`。
- 一旦匹配到 `case`，程序执行在 `switch` 语句内继续，直到遇到 `break`。
- 如果没有 `case` 标签匹配 `switch` 表达式，程序执行跳转到 `default` 标签（如果存在）。如果既没有 `case` 标签也没有 `default` 标签，则不执行 `switch` 体的任何部分。
- 条件运算符是一个根据条件求值为两个值之一的表达式。
- `do/while` 循环是后置检查循环，与 `while` 循环的前置检查循环不同。
- 无论条件如何，`do/while` 循环体至少执行一次。如果条件初始为假，则不执行 `while` 循环体。

## 7.6. 练习题

- `for` 循环是一种前置检查循环，当使用得当时，它将关于控制的所有信息集中在一个方便的位置。
- `for` 循环的三个部分是初始化、条件和修改。
- `for` 语句用于具有确定起始值、结束值和常规变量更新方式的循环。
- `for` 循环是计数的理想选择。
- `for` 循环头部可以省略；然而，如果你觉得需要一个或多个部分，`while` 语句可能是更好的选择。
- 最佳实践避免在 `for` 语句体内部修改变量。
- `<iomanip>` 库提供了 `setw` 对象，为输出提供格式化。

## 7.6 练习题

1. 考虑以下代码：

```cpp
int x;
cin >> x;
switch (x + 3) {
case 5:
cout << x << endl;
break;
case 10:
cout << x - 3 << endl;
break;
case 20:
cout << x + 3 << endl;
break;
}
```
(a) 用户输入 2 时会输出什么？
(b) 用户输入 5 时会输出什么？
(c) 用户输入 7 时会输出什么？
(d) 用户输入 17 时会输出什么？
(e) 用户输入 20 时会输出什么？
(f) 用户输入 5 时会输出什么？

2. 考虑以下代码：

```cpp
char ch;
cin >> ch;
switch (ch) {
case 'a':
cout << "*" << endl;
break;
case 'A':
cout << "**" << endl;
break;
case 'B':
// 缺少部分
case 'b':
cout << "****" << endl;
break;
case 'C':
case 'c':
cout << "*****" << endl;
break;
default:
cout << "******" << endl;
}
```
(a) 用户输入 a 时会输出什么？
(b) 用户输入 A 时会输出什么？
(c) 用户输入 b 时会输出什么？
(d) 用户输入 B 时会输出什么？
(e) 用户输入 C 时会输出什么？
(f) 用户输入 c 时会输出什么？
(g) 用户输入 t 时会输出什么？

3. 以下代码会输出什么？

```cpp
int x = 0;
do {
    cout << " ";
    x++;
} while (x < 10);
cout << endl;
```

4. 以下代码会输出什么？

```cpp
int x = 20;
do {
    cout << " ";
    x++;
} while (x < 10);
cout << endl;
```

5. 以下代码会输出什么？

```cpp
for (int x = 0; x < 10; x++)
    cout << "*";
cout << endl;
```

6. 重写代码，用 `switch` 代替 if/else 语句。

```cpp
int value;
char ch;
cin >> ch;
if (ch == 'A')
value = 10;
else if (ch == 'P')
value = 20;
else if (ch == 'T')
value = 30;
else if (ch == 'V')
value = 40;
else
value = 50;
cout << endl;
```

7. 重写代码，用多路 if/else 代替 `switch` 语句。

```cpp
int value;
char ch;
cin >> ch;
switch(ch) {
case 'A':
value = 10;
break;
case 'P':
cin >> value;
break;
case 'T':
value = ch;
break;
case 'V':
value = ch + 1000;
break;
default:
value = 50;
}
cout << endl;
```

8. 重写代码，用多路 if/else 代替 `switch` 语句。

```cpp
int value;
char ch;
cin >> ch;
switch (ch) {
case 'A':
cout << ch << endl;
value = 10;
break;
case 'P':
case 'E':
cin >> value;
break;
case 'T':
cin >> ch;
value = ch;
case 'C':
value = ch;
cout << "value=" << value << "=" << ch << endl;
break;
case 'V':
value = ch + 1000;
break;
}
```

9. 重写以下代码，用 `while` 循环代替 `for` 语句。

```cpp
for (int i = 100; i > 0; i--)
    cout << value << endl;
```

10. 重写代码，用条件运算符代替 if 语句。

```cpp
if (value % 2 != 0) // value 是偶数吗？
    value = value + 1; // 如果不是，使其变为偶数。
```

11. 重写代码，用条件运算符代替 if/else 语句。

```cpp
if (value % 2 == 0) // value 是偶数吗？
    value = 0; // 如果是，将其设为 0。
else
    value = value + 1; // 否则，使其变为偶数。
```

12. 以下多路 if/else 适合重写为 `switch` 语句吗？如果是，用 `switch` 重写代码；否则，说明为什么这样做不可。

```cpp
int x, y;
cin >> x >> y;
if (x < 10)
    y = 10;
else if (x == 5)
    y = 5;
else if (x == y)
    y = 0;
else if (y > 10)
    x = 10;
else
    x = y;
```

# 第8章

# 使用函数

假设你需要编写一个 C++ 程序来计算用户提供的数字的平方根。列表 8.1（computquareeroot.cpp）提供了一个简单的实现。

```cpp
Listing 8.1: computesquareeroot.cpp
// File squareroot.cpp

#include <iostream>

using namespace std;

int main() {
    double input;

    // 从用户处获取值
    cout << "Enter number: ";
    cin >> input;
    double diff;

    // 计算一个近似平方根
    double root = 1.0;

    do {
        // 循环直到近似平方根
        // 接近实际平方根
        root = (root + input/root) / 2.0;
        cout << "root is " << root << endl;
        // 近似值有多大？
        diff = root - input;
    } while (diff > 0.0001 || diff < -0.0001);

    // 报告近似平方根
    cout << "Square root of " << input << " = " << root << endl;
}
```

该程序基于一种简单的算法牛顿法，它通过连续近似来获得与真实答案误差在 0.0001 以内的结果。

