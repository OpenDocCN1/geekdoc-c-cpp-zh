

## 编程提示 5.1

![](img/23fb3582e93ebc95909e1de029c3d388_226_0.png)

## 函数注释

每当编写函数时，都应该用*注释*说明它的行为。注释是给人看的，而不是给编译器看的，并且函数注释的排版没有通用标准。本书将采用以下格式：

```cpp
/**
   计算立方体的体积。
   @param side_length 立方体的边长
   @return 体积
*/
double cube_volume(double side_length)
{
   double volume = side_length * side_length * side_length;
   return volume;
}
```

函数注释会说明函数的用途、参数变量和返回值的含义，以及任何特殊要求。

这种文档风格借鉴自 Java 编程语言。C++ 工具也广泛支持这种风格，例如 Doxygen 工具（www.doxygen.org）。

注释的第一行描述函数的用途。每个 `@param` 子句都会描述一个参数变量，`@return` 子句则描述返回值。

请注意，函数注释记录的不是实现（函数如何完成其工作），而是设计（函数的作用、输入及结果）。注释使其他程序员可以将函数当作“黑盒”来使用。

## 5.3 参数传递

参数变量保存函数调用中提供的实参值。

本节将介绍向函数传递实参的机制。调用函数时，会创建它的*参数变量*。（参数变量的另一个常用术语是*形式参数*。）在函数调用中，会为每个参数变量提供一个表达式，这个表达式称为*实参*。（这个表达式的另一个常用术语是*实际参数*。）每个参数变量都会用对应实参的值初始化。

请看图 3 所示的函数调用：

```cpp
double result1 = cube_volume(2);
```

![](img/23fb3582e93ebc95909e1de029c3d388_226_1.png)

水果派的食谱可能会要求使用任意种类的水果。这里，“水果”就是参数变量的一个例子。苹果和樱桃则是实参的例子。

## 5.4 返回值

> `return` 语句会终止函数调用并返回函数结果。

使用 `return` 语句指定函数的结果。执行到 `return` 语句时，函数会*立即*退出。利用这一特性，可以方便地在函数开头处理特殊情况：

```cpp
double cube_volume(double side_length)
{
    if (side_length < 0) { return 0; }
    double volume = side_length * side_length * side_length;
    return volume;
}
```

如果调用函数时为 `side_length` 传入了负值，那么函数会返回 0，且不会执行函数的其余部分。（参见图 4。）

在前面的示例中，每个 `return` 语句都返回了常量或变量。实际上，`return` 语句可以返回任意表达式的值。与其先将返回值保存到变量中再返回该变量，通常不如省去变量，直接返回一个更复杂的表达式：

```cpp
double cube_volume(double side_length)
{
    return side_length * side_length * side_length;
}
```

函数的每个分支都必须返回一个值。请看下面这个错误函数：

```cpp
double cube_volume(double side_length)
{
    if (side_length >= 0)
    {
        return side_length * side_length * side_length;
    } // 错误
}
```

假设你用负边长调用了 `cube_volume`。当然，你不应该这样调用，但编程错误可能会导致这种情况发生。因为如果条件不成立，`return` 语句就不会执行。然而，函数必须返回*某个值*。根据具体情况，编译器可能会

![](img/23fb3582e93ebc95909e1de029c3d388_229_0.png)

**图 4** `return` 语句会立即退出函数

将此标记为错误，或者函数可能会返回一个随机值。返回*某个*安全值即可避免这个问题：

```cpp
double cube_volume(double side_length)
{
    if (side_length >= 0)
    {
        return side_length * side_length * side_length;
    }
    return 0;
}
```

每个函数的最后一条语句都应该是 `return` 语句。这样可以确保函数执行到末尾时会返回*某个*值。

### 常见错误 5.1：缺少返回值

![](img/23fb3582e93ebc95909e1de029c3d388_230_0.png)

函数总是需要返回某个值。如果函数代码包含多个分支，请确保每个分支都返回一个值：

```cpp
int sign(double x)
{
    if (x < 0) { return -1; }
    if (x > 0) { return 1; }
    // 错误：当 x 等于 0 时缺少返回值
}
```

此函数用于计算数字的符号：负数返回 -1，正数返回 +1。然而，如果实参为零，函数就不会返回任何值。在这种情况下，大多数编译器都会发出警告；但如果你忽略警告，并且函数确实接收了实参 0，那么它就会返回一个*随机值*。

### 专题 5.1：函数声明

![](img/23fb3582e93ebc95909e1de029c3d388_230_1.png)

调用编译器不认识的函数会导致编译时错误，就像使用未定义的变量一样。可以通过在首次使用函数之前定义所有函数来避免此错误。先定义较低层级的辅助函数，再定义中层的核心函数，最后定义程序中的 `main` 函数。

有些程序员喜欢将 `main` 函数放在程序的开头。如果你也有这样的偏好，就需要了解如何在程序顶部声明其他函数。函数声明会列出返回类型、函数名和参数变量，但不包含函数体：

```cpp
double cube_volume(double side_length);
```

这是一个声明，表示该函数已在其他地方实现。区分声明和定义很容易：声明以分号结尾，而定义后面跟着一个 `{ ... }` 代码块。声明也称为*原型*。

在函数原型中，参数名是可选的。也可以这样写：

```cpp
double cube_volume(double);
```

不过，最好包含参数名，以便说明每个参数的用途。

常用函数（如 `pow`）的声明包含在头文件中。如果查看 `<cmath>`，就能找到 `pow` 和其他数学函数的声明。

下面是 `cube.cpp` 文件的另一种组织方式：

```cpp
#include <iostream>

using namespace std;

// cube_volume 的声明
double cube_volume(double side_length);

int main()
{
    double result1 = cube_volume(2);  // 调用 cube_volume
    double result2 = cube_volume(10);
    cout << "A cube with side length 2 has volume " << result1 << endl;
    cout << "A cube with side length 10 has volume " << result2 << endl;
    return 0;
}

// cube_volume 的定义
double cube_volume(double side_length)
{
    return side_length * side_length * side_length;
}
```

如果你喜欢这种写法，就可以在程序中采用它。只需要注意它的一个缺点：每当更改函数名或某个参数的类型时，都需要同时修改声明和定义。

### 方法 5.1——实现函数

![](img/23fb3582e93ebc95909e1de029c3d388_231_0.png)

函数是一种可以使用不同参数多次执行的计算，既可以在同一个程序中重复使用，也可以在不同程序中重复使用。每当某项计算需要执行多次时，就应该将它写成函数。

为了说明这一过程，假设你正在帮助研究埃及金字塔的考古学家。你承担了一项任务：编写一个函数，根据金字塔的高度和底边长度计算其体积。

- **步骤 1** 描述函数应完成的工作。

  用简单的英语描述，例如：“计算底面为正方形的金字塔的体积。”

- **步骤 2** 确定函数的“输入”。

  列出所有可能变化的参数。初学者编写的函数常常过于具体。例如，你可能知道埃及最大的金字塔——吉萨大金字塔——高 146 米，底边长 230 米。即使原题只要求计算大金字塔的体积，也*不应该*在计算中使用这些数字。编写一个能计算*任意*金字塔体积的函数同样简单，而且实用得多。

![](img/23fb3582e93ebc95909e1de029c3d388_231_1.png)

