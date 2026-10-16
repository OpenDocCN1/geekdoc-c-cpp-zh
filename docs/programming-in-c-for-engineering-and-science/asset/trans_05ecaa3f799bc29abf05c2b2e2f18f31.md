

## 警告

1. 调用函数时，实参的数量应与函数头中形参的数量相同。⁶
2. 与值参数对应的实参的类型应该与该参数的类型兼容。
3. 与引用参数对应的实参必须是其类型与该参数类型匹配的变量；它不能是常量或表达式。
4. 仔细检查所用每个函数的原型，看它是否有引用参数；这些参数值的变化可能导致实参值发生意外或非预期的变化。
5. 任何在函数外部使用函数参数的尝试都会产生错误，因为参数仅在该函数执行期间分配内存；在该函数执行之前或之后都没有与它们关联的内存。
6. 标识符必须先声明后使用。例如，如果函数 f() 调用函数 g()，那么 g() 的原型（或定义）必须位于 f() 的定义之前。
7. 内联函数不能拆分为原型放在头文件（.h）中、定义放在实现文件（.cpp）中。
8. 内联函数要有所节制，否则可能导致代码膨胀。

⁶ 一个例外是参数列表末尾的一个或多个参数带有默认实参；例如，

```cpp
void f(int x, int y = 0, double z = 3.5);
```

如下面的示例所示，该函数可以用 1 个、2 个或 3 个实参调用：

```
f(1, 2, 4.9); Within f, x will have the value 1, y the value 2, and z the value 4.9
f(1, 2); Within f, x will have the value 1, y the value 2, and z the value 3.5
f(1); Within f, x will have the value 1, y the value 0, and z the value 3.5
```

## 自测

### 10.3 节

1. 默认情况下发生的参数传递机制是按________调用。
2. ________参数包含对应实参的一个副本。
3. 如果在函数体内修改了________参数，则对应实参的值不会改变。
4. 如果在函数体内修改了________参数，则对应实参的值也会改变。
5. 在参数的类型与名称之间放置一个________，表示该参数是引用参数。

问题6-11假设有如下函数定义：

```cpp
void f(int x, int & y, int & z)
{
    z = y = x * x + 1;
}
```

并且在调用函数中有如下声明：

```cpp
int a = 0, b = 1, c = 2, d = 3;
const int E = 4;
```

6. （对或错）执行 `d = f(a, b, c);` 后，d 的值将为 1。

7. （对或错）执行 `f(a, b, c);` 后，b 和 c 的值都将为 1。

8. （对或错）执行 `f(c, d, E);` 后，d 的值将为 5。

9. （对或错）执行 `f(c+1, c-1, d);` 后，d 的值将为 10。

10. （对或错）函数调用 `f(c, d, E);` 使 z 成为 const 引用参数。

11. 重写 f() 的定义，使 x 成为 const 引用参数。

12. 给定函数定义

```cpp
void change(int number, string & a, string & b, string & c)
{
    const string BAT = "bat";
    if (number < 3)
    {
        a = BAT;
        b = BAT;
    }
    else
        c = BAT;
}
```

以下程序段将产生什么输出？

```cpp
string str1 = "cat", str2 = "dog", str3 = "elk";
change(2, str1, str2, str3);
cout << "String = " << str1 << str2 << str3 << endl;
```

### 10.4 节

1. 程序中标识符引用特定对象或函数的部分称为该标识符的________。
2. （对或错）如果在标识符的作用域内访问该标识符，就会产生编译错误。
3. 在块内声明的标识符，其作用域从声明处开始，一直到__________。
4. 参数的作用域是__________。
5. 以下语句将产生什么结果？

```cpp
for (int i = 0; i < 3; i++)
    cout << i << endl;
cout << "i is now " << i << endl;
```

### 10.5 节

1. __________是函数引用自身的现象。
2. 命名并描述函数递归定义的两个部分。
3. （对或错）计算某个值的非递归函数可能比计算相同值的递归函数执行得更快。
4. 对于下面的递归函数，求 f(5)。

```cpp
int f(int n)
{
    if (n == 0)
        return 0;
    else
        return n + f(n - 1);
}
```

5. 对于问题4中的函数，求 f(0)。

6. 对于问题4中的函数，假设在归纳步骤中把 + 改为 *。求 f(5)。

7. 对于问题4中的函数，函数调用 f(-1) 会发生什么？

### 10.6 节

1. 函数的__________是其参数类型的列表。
2. 如果两个函数具有相同的__________，则称它们被重载。
3. 只要该函数的任意两个定义不具有相同的__________，函数名就可以被重载。
4. __________是一种模式，可以从中构造一个函数。
5. 模板可以有__________参数，但普通函数不能。

6. 给定模板定义

```cpp
template<typename something>
void print(something x)
{
    cout << "***" << x << "***\n";
}
```

描述编译器在遇到以下语句时将会做什么：

```cpp
int number = 123;
print(number);
```

## 练习

### 10.3 节

练习1-11假设有以下程序框架：

```cpp
#include <cmath>
using namespace std;

void calculate(double a, double &b,
    int m, int &k, int &n, char &c);

int main()
{
    const double PI = 3.14159;
    const int TWO = 2;
    const char INITIAL = 'N';

    int month, day, year, p, q;
    double hours, rate, amount, u, v;
    char code, dept;
}
```

确定给定的语句是否可用于调用函数 calculate()。如果不可以使用，请解释原因。

1. `calculate(u, v, TWO, p, q, code);`
2. `calculate(PI, u, TWO, p, v, dept);`
3. `calculate(hours, PI, TWO, day, year, dept);`
4. `calculate(13, hours, PI, 13, year, dept);`
5. `calculate(PI * hours, PI, TWO, day, year, dept);`
6. `calculate(PI, PI * hours, TWO, day, year, dept);`
7. `while (u > 0)`
   `calculate(u, v, TWO, p, q, code);`
8. `calculate(0, hours, (p + 1) / 2, day, year, code)`
9. `calculate(sqrt(amount), rate, 7, p, q, INITIAL);`
10. `while (amount > 0)`
    `calculate(TWO, amount, day, p + q, day, dept);`
11. `cout << calculate(u, v, TWO, p, q, code);`

以下练习要求你编写函数来计算各种量。为了测试这些函数，你应按照编程问题1-4中的说明编写驱动程序。

12. 示例1中的找零钱函数在将实金额转换为分之前，先将其四舍五入到最接近的百分位。编写一个函数，接收一个实数值和一个非负整数，并返回该实数值四舍五入到该整数指定的小数位数——若接收的整数为0，则返回最接近的整数；若为1，则返回最接近的十分位；若为2，则返回最接近的百分位；依此类推。

13. 编写一个函数，接收以磅和盎司表示的重量，并返回相应的以克为单位的重量。（1 oz = 28.349527 g）

14. 编写一个函数，接收以克为单位的重量，并返回相应的以磅和盎司表示的重量。

15. 编写一个函数，接收以码、英尺和英寸表示的长度，并返回相应的以厘米为单位的测量值。（1 in = 2.54001 cm）

16. 编写一个函数，接收以厘米为单位的长度，并返回相应的以码、英尺和英寸表示的测量值。

17. 编写一个函数，接收以通常方式表示的时间：小时、分钟以及一个指示是上午（“A”）还是下午（“P”）的字符值，并返回相应的24小时制时间。

18. 编写一个函数，接收24小时制格式的时间，并返回相应的通常表示法，即小时、分钟和上午/下午。例如，时间0100应返回1小时、0分钟和“A”以表示上午；时间1545应返回3小时、45分钟和“P”以表示下午。

### 10.5 节

练习1-12假设有以下函数 f()：

```cpp
void f(int num)
{
    if ((1 <= num) && (num <= 8))
    {
        f(num - 1);
        cout << num;
    }
    else
        cout << endl;
}
```

对于练习1-3，说明函数调用产生什么输出。

1. `f(3);`
2. `f(7);`

