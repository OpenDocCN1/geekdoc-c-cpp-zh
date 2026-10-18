

## 显示 4.18 重载函数名（第 1 部分，共 2 部分）

//判断是圆形披萨还是矩形披萨更划算。
#include <iostream>

double unitPrice(int diameter, double price);
//返回圆形披萨每平方英寸的价格。
//名为 diameter 的形参是披萨的直径，单位为英寸。
//名为 price 的形参是披萨的价格。

double unitPrice(int length, int width, double price);
//返回尺寸为 length 英寸 × width 英寸的矩形披萨
//每平方英寸的价格。
//形参 price 是披萨的价格。

int main()
{
    using namespace std;
    int diameter, length, width;
    double priceRound, unitPriceRound,
    priceRectangular, unitPriceRectangular;

    cout << "欢迎来到披萨消费者联盟。\n";
    cout << "请输入圆形披萨的直径（英寸）：";
    cin >> diameter;
    cout << "请输入圆形披萨的价格：$";
    cin >> priceRound;
    cout << "请输入矩形披萨的长度和宽度（英寸）\n";
    cin >> length >> width;
    cout << "请输入矩形披萨的价格：$";
    cin >> priceRectangular;

    unitPriceRectangular =
            unitPrice(length, width, priceRectangular);
    unitPriceRound = unitPrice(diameter, priceRound);

    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);
    cout << endl
         << "圆形披萨：直径 = "
         << diameter << " 英寸\n"
         << "价格 = $" << priceRound
         << " 每平方英寸价格 = $" << unitPriceRound
         << endl
         << "矩形披萨：长度 = "
         << length << " 英寸\n"

## 自动类型转换

假设你的程序中出现了以下函数定义，并且你没有重载函数名 mpg（因此这是名为 mpg 的函数的唯一定义）：

```
double mpg(double miles, double gallons)
//返回每加仑英里数。
{
    return (miles/gallons);
}
```

如果你用 int 类型的实参调用函数 mpg，C++ 会自动将任何 int 类型的实参转换为 double 类型的值。因此，下面这条语句将在屏幕上输出 22.5 英里每加仑：

```
cout << mpg(45, 2) << " miles per gallon";
```

C++ 将 45 转换为 45.0，将 2 转换为 2.0，然后执行除法 45.0/2.0，得到返回值 22.5。

如果一个函数需要 double 类型的实参，而你给它一个 int 类型的实参，C++ 会自动将该 int 实参转换为 double 类型的值。这非常有用且自然，我们几乎不会去注意它。然而，重载可能会干扰这种自动类型转换。让我们看一个例子。

现在，假设你（愚蠢地）重载了函数名 mpg，使你的程序中除了之前的定义之外，还包含以下 mpg 的定义：

```
int mpg(int goals, int misses)
//返回完美进球衡量值
//计算公式为 (goals - misses)。
{
    return (goals - misses);
}
```

在同时包含这两个 mpg 函数定义的程序中，下面这条语句将（不幸地）输出 43 英里每加仑（因为 43 是 45 − 2 的结果）：

```
cout << mpg(45, 2) << " miles per gallon";
```

当 C++ 看到函数调用 mpg(45, 2)（两个实参都是 int 类型）时，C++ 首先查找具有两个 int 类型形参的 mpg 函数定义。如果找到了这样的函数定义，C++ 就使用该定义。除非找不到匹配的函数定义，否则 C++ 不会将 int 实参转换为 double 类型的值。

mpg 的例子还说明了关于重载的另一点：你不应该对两个不相关的函数使用相同的函数名。这种对函数名的粗心使用最终必定会造成混乱。

## 重载与类型转换的交互

## 自测练习

24. 假设你有两个函数定义，其函数声明如下：

```
double score(double time, double distance);
int score(double points);
```

在下面的函数调用中会使用哪个函数定义？为什么使用它？（x 的类型是 double。）

```
finalScore = score(x);
```

25. 假设你有两个函数定义，其函数声明如下：

```
double theAnswer(double data1, double data2);
double theAnswer(double time, int count);
```

在下面的函数调用中会使用哪个函数定义？为什么使用它？（x 和 y 的类型是 double。）

```
x = theAnswer(y, 6.0);
```

26. 假设你有两个函数定义，其函数声明如自测练习 25 所示。在下面的函数调用中会使用哪个函数定义？为什么使用它？

```
x = theAnswer(5, 6);
```

27. 假设你有两个函数定义，其函数声明如自测练习 25 所示。在下面的函数调用中会使用哪个函数定义？为什么使用它？

```
x = theAnswer(5, 6.0);
```

28. 这个问题与编程示例“修订版披萨购买程序”有关。假设那个总是试图欺骗顾客的可恶的披萨店推出了一种方形披萨。你是否可以重载函数 unitprice，使其既能计算圆形披萨每平方英寸的价格，也能计算方形披萨每平方英寸的价格？为什么可以或为什么不可以？

29. 查看显示 4.18 中的程序。main 函数包含了 using 指令：

```
using namespace std;
```

为什么 unitprice 方法不包含这个 using 指令？

## 章节总结

- 为程序设计算法的好的策略是：将需要完成的任务分解为几个子任务，然后将每个子任务进一步分解为更小的子任务，如此继续，直到子任务简单到可以轻松地用 C++ 代码实现。这种方法称为**自顶向下设计**。
- 返回值的函数就像一个小程序。函数的实参充当这个“小程序”的输入，返回的值类似于这个“小程序”的输出。
- 当程序中的某个子任务接收一些值作为输入，并只产生一个值作为其结果时，该子任务就可以实现为一个函数。
- 函数应该被定义成可以当作黑盒使用。使用函数的程序员不需要知道函数编码的任何细节。程序员只需要知道函数声明以及描述返回值的注释即可。这一规则有时被称为**过程抽象原则**。
- 在函数定义中声明的变量称为**函数的局部变量**。
- 全局命名常量使用 *const* 修饰符声明。全局命名常量的声明通常放在程序开头，位于 include 指令之后、函数声明之前。
- 按值传递的形参（这是本章讨论的唯一一种形参）是函数内部的局部变量。偶尔，将形参用作局部变量是很有用的。
- 当你对同一个函数名有两个或更多函数定义时，这称为**重载函数名**。当你重载一个函数名时，各函数定义的形参数量必须不同，或者某些形参的类型必须不同。

## 自测练习答案

```
1.  4.0       4.0       8.0
    8.0       8.0       1.21
    3         3         0
    3.0       3.5       3.5
    6.0       6.0       5.0
    5.0       4.5       4.5
    3         3.0       3.0
```

7. 函数声明为：

```
double ave(int n1, double n2);
//返回 n1 和 n2 的平均值。
```

函数定义为：

```
double ave(int n1, double n2)
{
    return ((n1 + n2)/2.0);
}
```

8. 函数声明为：

```
char positiveTest(double number);
//如果 number 为正数，返回 'P'。
//如果 number 为负数或零，返回 'N'。
```

函数定义为：

```
char positiveTest(double number)
{
    if (number > 0)
        return 'P';
    else
        return 'N';
}
```

9. 假设函数定义了形参，比如说 param1 和 param2。然后用对应的实参 arg1 和 arg2 调用该函数。实参的值被“代入”对应的形参，arg1 代入 param1，arg2 代入 param2。之后函数体内使用这些形参。

10. 预定义（库）函数通常要求你 #include 一个头文件。对于程序员自定义的函数，程序员将函数代码放在包含主程序的文件中，或放在另一个与主程序一同编译和链接的文件中。

```
bool inOrder(int n1, int n2, int n3)
{
    return ((n1 <= n2) && (n2 <= n3));
}
```

```
bool even(int n)
{
    return ((n % 2) == 0);
}
```

