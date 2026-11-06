
将其标记为错误，否则函数可能会返回一个随机值。通过返回某个安全值来防范此问题：

```c
double cube_volume(double side_length)
{
    if (side_length > 0)
    {
        return side_length * side_length * side_length;
    }
    return 0;
}
```

每个函数的最后一条语句都应当是 return 语句。这确保当函数执行到末尾时，会返回*某个*值。

## 常见错误 5.1

### 缺少返回值

函数总是需要返回某些内容。如果函数的代码包含多个分支，请确保每个分支都返回一个值：

```c
int sign(double x)
{
    if (x < 0) { return -1; }
    if (x > 0) { return 1; }
    // Error: missing return value if x equals 0
}
```

此函数计算一个数的符号：负数返回 –1，正数返回 +1。然而，如果参数为零，则不会返回任何值。大多数编译器会在此情况下发出警告，但如果你忽略该警告，并且函数曾以 0 作为参数被调用，就会返回一个随机量。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_230_0.png)

## 专题 5.1

### 函数声明

调用编译器不知道的函数是编译时错误，就像使用未定义的变量一样。如果你在首次使用所有函数之前先定义它们，就可以避免此错误。首先定义底层辅助函数，然后定义中层主力函数，最后在程序中定义 `main`。

有些程序员喜欢在程序中首先列出 `main` 函数。如果你也有此偏好，就需要学习如何在程序顶部**声明**其他函数。函数声明列出返回类型、函数名和参数变量，但不包含函数体：

```c
double cube_volume(double side_length);
```

这是一则声明，承诺该函数在其他地方实现。区分声明和定义很容易：声明以分号结尾，而定义后面跟一个 `{ ... }` 块。声明也称为**原型**。

在函数原型中，参数名是可选的。你也可以写成

```c
double cube_volume(double);
```

不过，为了说明每个参数的用途，在声明中包含参数名是个好主意。

常见函数（如 `pow`）的声明包含在头文件中。如果查看 `<cmath>` 内部，你会找到 `pow` 和其他数学函数的声明。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_230_1.png)

下面是 cube.cpp 文件的另一种组织方式：

```cpp
#include <iostream>

using namespace std;

// Declaration of cube_volume
double cube_volume(double side_length);

int main()
{
    double result1 = cube_volume(2);  // Use of cube_volume
    double result2 = cube_volume(10);
    cout << "A cube with side length 2 has volume " << result1 << endl;
    cout << "A cube with side length 10 has volume " << result2 << endl;
    return 0;
}

// Definition of cube_volume
double cube_volume(double side_length)
{
    return side_length * side_length * side_length;
}
```

如果你喜欢这种方法，尽可在程序中使用它。你只需要注意一个缺点。每当你更改函数名或某个参数类型时，都需要在两个地方修改：声明和定义中。

## 如何做 5.1 实现函数

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_231_0.png)

函数是一种可以多次使用不同参数的计算，既可以在同一程序中使用，也可以在不同程序中使用。每当某项计算需要多次使用时，就把它做成一个函数。

为了说明这个过程，假设你正在帮助研究埃及金字塔的考古学家。你接到的任务是编写一个函数，在给定高度和底边长度的情况下确定金字塔的体积。

- **第 1 步** 描述函数应该做什么。  
  提供一段简单的英文描述，例如“计算底面为正方形的金字塔的体积。”

- **第 2 步** 确定函数的“输入”。  
  列出所有可能变化的参数。初学者常常会实现过于具体的函数。例如，你可能知道吉萨大金字塔是埃及金字塔中最大的一座，高 146 米，底边长 230 米。即使最初的问题只问到大金字塔，你也不应在计算中使用这些数字。编写一个计算任意金字塔体积的函数同样简单——而且有用得多。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_231_1.png)

在我们的例子中，参数是金字塔的高度和底边长度。此时，我们已有足够信息来编写函数文档：

```cpp
/**
   Computes the volume of a pyramid whose base is a square.
   @param height the height of the pyramid
   @param base_length the length of one side of the pyramid's base
   @return the volume of the pyramid
*/
```

### 第 3 步 确定参数变量和返回值的类型。

高度和底边长度都可以是浮点数。因此，我们将为两个参数变量选择类型 `double`。计算出的体积也是浮点数，因此返回类型为 `double`。于是，函数将定义为

```cpp
double pyramid_volume(double height, double base_length)
```

### 第 4 步 编写伪代码以获得所需结果。

大多数情况下，函数需要执行若干步骤才能得到所需答案。你可能需要使用数学公式、分支或循环。用伪代码表达你的函数。通过互联网搜索可知，金字塔体积的计算公式为

```text
volume = 1/3 x height x base area
```

由于底面是正方形，我们有

```text
base area = base length x base length
```

使用这两个等式，我们可以根据参数变量计算体积。

### 第 5 步 实现函数体。

在我们的示例中，函数体相当简单。注意使用 return 语句返回结果。

```cpp
{
   double base_area = base_length * base_length;
   return height * base_area / 3;
}
```

### 第 6 步 测试函数。

实现函数后，应当单独测试它。这样的测试称为单元测试。手工设计测试用例，并确保函数产生正确结果。例如，对于高度为 9、底边长为 10 的金字塔，我们期望体积为 1/3 × 9 × 100 = 300。如果高度为 0，我们期望体积为 0。

```cpp
int main()
{
   cout << "Volume: " << pyramid_volume(9, 10) << endl;
   cout << "Expected: 300" << endl;
   cout << "Volume: " << pyramid_volume(0, 10) << endl;
   cout << "Expected: 0" << endl;
   return 0;
}
```

输出确认函数按预期工作：

```text
Volume: 300
Expected: 300
Volume: 0
Expected: 0
```

### 示例 5.1 匹配并替换字符串中的部分内容

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_233_0.png)

本示例创建一个函数，用于查找一个字符串在给定字符串中首次出现的位置，并将其替换为第二个字符串。

### 示例 5.2 使用调试器

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_233_1.png)

在本示例中，你将学习如何使用调试器查找程序中的错误。

## 5.5 无返回值的函数

使用返回类型 `void` 表示函数不返回值。

有时，你需要执行一系列不产生值的指令。如果该指令序列出现多次，你会希望将其打包成一个函数。在 C++ 中，使用返回类型 `void` 表示没有返回值。

下面是一个典型示例。你的任务是在一个方框中打印一个字符串，如下所示：

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_233_2.png)

```text
-------
|Hello!|
-------
```

不过，可以用不同的字符串替换 `Hello`。用于此任务的函数可以定义如下：

```cpp
void box_string(string str)
```

现在，你按通常方式开发函数体，即制定解决该任务的通用方法。

- 打印一行，其中包含 `-` 字符 `n * 2` 次，其中 `n` 是字符串的长度。
- 打印一行，包含该字符串，左右两侧用 `|` 包围。
- 再打印一行，其中包含 `-` 字符 `n * 2` 次。

以下是函数实现：

```cpp
/**
   Prints a string in a box.
   @param str the string to print
*/
void box_string(string str)
{
