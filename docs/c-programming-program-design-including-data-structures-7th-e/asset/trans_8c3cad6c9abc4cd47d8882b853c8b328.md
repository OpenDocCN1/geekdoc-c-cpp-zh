

## 静态变量与自动变量

到目前为止讨论的变量遵循两条简单规则：

- 1. 只要程序执行，全局变量的内存就保持已分配状态。
- 2. 在块内声明的变量，其内存在进入块时分配，在退出块时释放。例如，函数的形式参数和局部变量的内存在函数被调用时分配，在函数退出时释放。

在进入块时分配内存、在退出块时释放内存的变量称为**自动变量**。只要程序执行其内存就保持已分配状态的变量称为**静态变量**。全局变量是静态变量，默认情况下，在块内声明的变量是自动变量。可以使用保留字 `static` 在块内声明静态变量。声明静态变量的语法是：

```cpp
static dataType identifier;
```

语句：

```cpp
static int x;
```

将 x 声明为 `int` 类型的静态变量。

在块内声明的静态变量是该块的局部变量，其作用域与该块中任何其他局部标识符的作用域相同。

大多数编译器会将静态变量初始化为其默认值。例如，`static int` 变量会被初始化为 0。不过，最好由你自己初始化静态变量，尤其是当初始值不是默认值时。在这种情况下，静态变量在声明时初始化。语句：

```cpp
static int x = 0;
```

将 x 声明为 `int` 类型的静态变量，并在第一次调用函数时将 x 初始化为 0。

### 示例 6-18

下面的程序展示了静态变量和自动变量的行为。

```cpp
//Program: Static and automatic variables

#include <iostream>

using namespace std;

void test();

int main()
{
    int count;

    for (count = 1; count <= 5; count++)
        test();

    return 0;
}

void test()
{
    static int x = 0;
    int y = 10;

    x = x + 2;
    y = y + 1;

    cout << "Inside test x = " << x << " and y = "
         << y << endl;
}
```

**示例运行：**

```
Inside test x = 2 and y = 11
Inside test x = 4 and y = 11
Inside test x = 6 and y = 11
Inside test x = 8 and y = 11
Inside test x = 10 and y = 11
```

在函数 test 中，x 是初始化为 0 的静态变量，y 是初始化为 10 的自动变量。函数 main 调用函数 test 五次。每次调用函数 test 时都会为变量 y 分配内存，并在函数退出时释放。因此，每次调用函数 test 时，它都会打印相同的 y 值。然而，由于 x 是静态变量，只要程序执行，x 的内存就保持已分配状态。变量 x 在第一次调用函数时被初始化一次为 0。后续对函数 test 的调用使用程序上一次离开（执行完）函数 test 时 x 所具有的值。

由于静态变量的内存在函数调用之间保持已分配状态，静态变量允许你在一次函数调用到另一次函数调用之间使用变量的值。即使你想在函数调用之间使用某些值时可以使用全局变量，静态变量的局部作用域也能防止其他函数操纵其值。

## 调试：使用驱动程序与桩函数

在本章和前面几章中，你学习了如何编写函数，将一个问题划分为若干子问题，求解每个子问题，然后组合这些函数形成完整程序，从而得到问题的解。一个程序可能包含若干函数。在复杂程序中，通常当一个函数编写完成后，会单独对其进行测试和调试。你可以编写一个单独的程序来测试该函数。用于测试函数的程序称为**驱动程序**。例如，示例 6-15 中的程序包含将长度从英尺和英寸转换为米和厘米以及反向转换的函数。在编写完整程序之前，你可以编写单独的驱动程序，以确保每个函数都能正常工作。

有时，一个函数计算出的结果在另一个函数中需要用到。在这种情况下，依赖于另一个函数的函数无法单独测试。例如，考虑下面这个确定注满游泳池所需时间的程序。

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

const double GALLONS_IN_A_CUBIC_FOOT = 7.48;

double poolCapacity(double len, double wid, double dep);
void poolFillTime(double len, double wid, double dep,
                  double fRate, int& fTime);
void print(int fTime);

int main()
{
    double length, width, depth;
    double fillRate;
    int fillTime;

    cout << fixed << showpoint << setprecision(2);

    cout << "Enter the length, width, and the depth of the "
         << "pool (in feet): ";
    cin >> length >> width >> depth;
    cout << endl;

    cout << "Enter the rate of the water (in gallons per minute): ";
    cin >> fillRate;
    cout << endl;

    poolFillTime(length, width, depth, fillRate, fillTime);
    print(fillTime);

    return 0;
}

double poolCapacity(double len, double wid, double dep)
{
    double volume;
    double poolWaterCapacity;

    volume = len * wid * dep;
    poolWaterCapacity = volume * GALLONS_IN_A_CUBIC_FOOT;

    return poolWaterCapacity;
}

void poolFillTime(double len, double wid, double dep,
                  double fRate, int& fTime)
{
    double poolWaterCapacity;

    poolWaterCapacity = poolCapacity(len, wid, dep);
    fTime = static_cast<int> (poolWaterCapacity / fRate + 0.5);
}

void print(int fTime)
{
    cout << "The time to fill the pool is approximately: "
         << fTime / 60 << " hour(s) and " << fTime % 60
         << " minute(s)." << endl;
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

输入游泳池的长度、宽度和深度（以英尺为单位）：30 15 10

输入水的流速（以加仑/分钟为单位）：100

注满游泳池的时间约为：5 小时 37 分钟。

如你所见，该程序包含用于求出注满游泳池所需水量的函数 poolCapacity、用于求出注满游泳池所需时间的函数 poolFillTime，以及其他一些函数。现在，要计算注满游泳池的时间，你必须知道所需的水量以及水注入游泳池的速率。由于函数 poolFillTime 需要函数 poolCapacity 的结果，因此函数 poolFillTime 无法单独测试。这是否意味着我们必须按特定顺序编写这些函数？不一定，尤其是当不同的人负责程序的不同部分时。在这种情况下，我们使用函数桩。函数桩是一个尚未完整编码的函数。对于 void 函数，函数桩可能只包含函数头和一对空花括号 { }；对于有返回值的函数，它可能只包含一条 return 语句，并带有一个合理且易于使用的返回值。例如，函数 poolCapacity 的函数桩可以是：

```cpp
double poolCapacity(double len, double wid, double dep)
{
    return 1000.00;
}
```

函数的**签名**由函数名及其形式参数列表组成。如果两个函数具有不同的名称或不同的形式参数列表，则它们具有不同的签名。（注意，函数的签名不包括函数的返回类型。）

如果函数名被重载，那么该集合中的所有函数都具有相同的名称。因此，重载集合中的所有函数必须具有不同的形式参数列表。因此，以下函数头正确地重载了函数 `functionXYZ`：

```
void functionXYZ()
void functionXYZ(int x, double y)
void functionXYZ(double one, int y)
void functionXYZ(int x, double y, char ch)
```

考虑以下用于重载函数 `functionABC` 的函数头：

```
void functionABC(int x, double y)
int functionABC(int x, double y)
```

这两个函数头具有相同的名称和相同的形式参数列表。因此，这些用于重载函数 functionABC 的函数头是不正确的。在这种情况下，编译器将生成语法错误。（注意，这些函数头的返回类型不同。）

如果函数被重载，那么在调用该函数时，函数的形式参数列表决定执行哪个函数。

> **注意**
> 有些作者将函数的签名定义为形式参数列表，有些则将函数的整个函数头视为其签名。然而，在本书中，函数的签名由函数的函数头及其形式参数列表组成。如果函数名称不同，那么编译器当然可以毫无问题地识别调用的是哪个函数，并会正确地翻译代码。然而，如果函数名被重载，那么如前所述，函数的形式参数列表决定执行哪个函数体。

假设你需要编写一个函数来确定两个项中较大的那个。这两个项可以是整数、浮点数、字符或字符串。你可以编写如下几个函数：

```
int largerInt(int x, int y);
char largerChar(char first, char second);
double largerDouble(double u, double v);
string largerString(string first, string second);
```

函数 largerInt 确定两个整数中较大的那个；函数 largerChar 确定两个字符中较大的那个，依此类推。所有这些函数执行类似的操作。与其给这些函数起不同的名称，不如为每个函数使用相同的名称——比如 larger；也就是说，你可以重载函数 larger。因此，你可以将前面的函数原型简写为：

