
此对 `fill_up` 的调用将用从键盘输入的五个整数填充 `score` 数组。注意，形式参数 `a[]`（在函数声明和函数定义头部中使用）带有方括号但没有索引表达式（你可以在数组参数的方括号内插入一个数字，编译器将简单地忽略该数字，因此我们在文中不使用此类数字）。

形式参数 `a[]`（在函数声明和函数定义头部中使用）带有方括号但没有索引表达式（你可以在数组参数的方括号内插入一个数字，编译器将简单地忽略该数字，因此我们在文中不使用此类数字）。此对 `fill_up` 的调用将用从键盘输入的五个整数填充 `score` 数组。

# 数组

你打算修改数组参数，计算机随后将检查并你的代码没有无意中改变数组中的任何值。为了告诉编译器某个数组参数不应被你的函数修改，你可以在参数位置的数组之前插入修饰符 `const`。使用 `const` 修饰的数组参数被称为常量数组参数。

例如，以下函数输出了数组中的值，但没有改变数组中的值：

```
void show_the_world(int a [], int size_of_a)
//前置条件：size_of_a 是数组 a 的声明大小。
//a 的所有索引变量都已赋值。
//后置条件：a 中的值已写入
//到屏幕上。
{
    cout << "The array contains the following values:\n";
    for (int i = 0; i < size_of_a; i++)
        cout << a[i] << " ";
    cout << endl;
}
```

该函数可以正常工作。但是，作为额外的安全措施，你可以如下所示所示在函数头中添加 `const` 修饰符：

```
void show_the_world(const int a [], int size_of_a)
```

添加了此 `const` 修饰符后，如果你的函数定义中包含改变数组参数中任何值的错误，计算机将发出错误消息。

| 数组形式参数与实参 |
| :--- |
| 函数的参数可以是整个数组，但整个数组的参数既不是按值传递参数也不是按引用传递参数。它被称为数组参数。这是一种新类型的参数。当用数组参数传递给数组参数时，传递给函数的所有只是该数组参数第一个索引变量在内存中的地址（索引为 0 的那个）。数组参数不会告知数组的大小。因此，当你给函数提供一个数组参数时，通常还需要另一个类型为 `int` 的另一个形式参数来提供数组的大小（见下文示例）。 |
| 数组参数在以下方面类似于按引用传递的参数。如果函数体更改了数组参数，那么当调用该函数时，该更改实际上是应用在数组参数上的。因此，函数可以改变数组参数的值（也就是说，可以改变其索引变量的值）。 |

# 数组

带有数组参数的函数声明语法如下：语法：返回类型_函数名(..., 基本类型_数组名[],...); 示例：`void sum_array(double&sum, double a[], int size);`

例如，以下是 `show_the_world` 函数的一个版本，它包含一个无意改变数组参数值的错误。幸运的是，这个定义包含了 `const` 修饰符，因此错误消息会告诉我们数组被更改了。该错误消息有助于解释错误：

```
void show_the_world(const a[], int size_of_a)
//前置条件：size_of_a 是数组 a 的声明大小。
//a 的所有索引变量都已赋值。
//后置条件：a 中的值已写入
{
    cout << "The array contains the following values:\n";
    for (int i = 0; i < size_of_a; i++)
        cout << a[i] << " ";
        // 错误，但除非你
        // 使用修饰符，否则编译器
        // 将不会发现。
    cout << endl;
}
```

如果我们没有在这个函数中使用中使用 `const` 且我们犯了错误，该函数将编译并运行，没有任何错误消息。代码将包含一个无限循环，不断增加 `a[0]` 并将其新值写入屏幕。

这个不准确的 `show_the_world` 版本的问题在于，`for` 循环中增加了错误的项。索引变量 `a[i]` 被增加了，但本应该增加的是索引 `i`。在这个错误的版本中，索引 `i` 从值 0 开始，且该值从未被改变。但 `a[i]`（等同于 `a[0]`）被增加了。当索引变量 `a[i]` 增加时，它会改变数组中的一个值，由于由于我们包含了 `const` 修饰符，计算机将发出警告消息。该错误消息应该作为发现何处错误的线索。

通常情况下，在你的程序中除了函数定义外，还有一个函数声明。当你在函数定义中使用 `const` 修饰符时，你必须在函数声明中也使用它，以便函数头和函数声明保持一致。

# 数组

`const` 修饰符可以用于任何类型的参数，但通常只用于数组参数和类的按引用传递参数。

## 陷阱 `const` 参数的使用不一致

`const` 参数修饰符是一个“全或无”的假设。如果你对某个特定类型的一个数组参数使用了它，你就应该对所有其他具有该类型且不被函数修改的数组参数都使用它。原因在于函数调用中的函数调用。

考虑 `show_difference` 函数的定义，如下所示，以及在定义中使用的函数声明：

```
double compute_average(int a[], int number_used);
//返回 a 中前 number_used 个
// 元素的平均值。数组未改变。
```

```
void show_difference(const a[], int number_used) {
  double average = compute_average(a, number_used);
  cout << "Average of the " << number_used << " elements is " << average << endl;
  cout << "The numbers are: " << endl;
  for (int i = 0; i < number_used; i++)
    cout << a[i] << " ";
  cout << endl;
}
```

这段代码将产生错误消息或警告，因为 `show_difference` 尝试将 `const` 数组传递给 `compute_average`，而后者期望的是非 `const` 数组。为了修复这个问题，你应该更改 `compute_average` 的声明以接受 `const` 数组。因此，`compute_average` 的函数声明如下：

```
double compute_average(const a[], int number_used);
```

# 返回数组的函数

函数不能像返回 `int` 或 `double` 值那样返回数组。有一种方法是可以返回数组的。然而，我们还没有学习指针。我们在讨论数组和指针时会讨论返回数组。在此之前你没有方法编写返回数组的函数。

# 案例研究 生产图

在这个案例中，我们在程序的自顶设计中使用数组。我们使用索引变量和整个数组作为子任务的参数

# 问题定义

Apex 塑料勺公司委托我们编写一个程序，显示其四个工厂在任何给定周内的生产率条形图。工厂按部门分开生产数据，例如茶勺部门、汤勺部门、平勺部门、彩色搅拌勺部门等。此外，每个工厂都有若干个部门。例如，只有一个工厂制造彩色搅拌勺。输出将是

```
Plant #1 ******
Plant #2 ******
Plant #3 #################
Plant #4 *****
```

每个星号代表 1000 单位的输出。

我们决定为每个部门单独读取输入。由于部门不能生产负数量的勺子，我们知道每个部门的生产数据是非负的。因此，我们可以使用负数作为哨兵值来标记每个工厂生产数据的结束。

# 输入

有四个编号为 1 到 4 的工厂。对于这四个工厂中的每一个都提供以下输入：一组给出该工厂每个部门产量的数字。列表以负数作为哨兵值结束。

# 输出

一个显示每个工厂总产量的柱状图。柱状图中的每个星号等于 1000 个单位。每个工厂的产量都会四舍五入到最近的 1000 单位。

# 问题分析

我们将使用一个名为 `production` 的数组，它将存储四个工厂每个工厂的总产量。在 C++ 中，数组索引始终从 0 开始。但由于工厂的编号是 1 到 4，而不是 0 到 3，因此我们不会使用工厂编号作为数组索引。相反，我们将第 $n$ 号工厂的总产量存放在索引 `production[n-1]` 中。1 号工厂的总产量将位于 `production[0]` 中，2 号工厂的数据将位于 `production[1]` 中，以此此类推。

产量是以千位为单位的，程序将缩放数组元素的值。如果 3 号工厂的总产量为 4040，那么 `production[2]` 的值最初将被设置为 4040。然后，这个 4040 的值将被缩放为 4，图中用四个星号来表示 3 号工厂的产量。

我们程序的任务可以分为以下几个子任务：

- 读取每个工厂的输入数据，并将索引变量 `production[plant_number-1]` 的值设置为该工厂的总产量，其中 `plant_number` 是工厂的编号。
- 缩放：对于每个 `plant_number`，将索引变量 `plant[plant_number - 1]` 的值更改为正确的星号数量。
- 输出柱状图。

整个 `production` 数组将作为执行这些子任务的函数的参数。按照数组参数的惯例，这意味着我们必须有一个额外的形式参数来表示数组的大小，在本例中，该大小等于工厂的数量。我们将使用一个定义常量表示工厂的数量，该常量将作为 `production` 数组的大小。我们程序的主部分连同执行子任务的函数声明以及工厂数量的定义常量，如显示 5 所示。注意，由于没有理由通过添加 `const` 修饰符将数组参数改为常量参数。显示 5 中的内容是我们程序的大纲，如果它位于一个单独的文件中，可以对其进行编译，以便我们在定义与所示函数声明对应的函数之前，检查该大纲中的任何语法错误。

编译了显示 5 中的文件后，我们就准备好设计三个子任务的函数实现了。对于这三个函数中的每一个，我们都设计一个算法，编写函数代码，并在进入下一个函数设计之前对函数进行测试。

# 子任务

# 数组

### input_data 的算法设计

`input_data` 函数的声明和描述性注释在显示 5 中。正如程序主部分体（也显示在显示 5 中）所示，当调用 `input_data` 时，形式数组参数将被数组 `production` 替换，由于最后一个工厂编号与工厂总数相同，形式参数 `last_plant_number` 将被 `NUMBER_OF_PLANTS` 替换。`input_data` 的算法是直观的。

- 对于 `plant_number` 等于 1, 2 直到 `last_plant_number` 的每一个值，执行以下操作：
    - 读取编号为 `plant_number` 的工厂的所有数据。
    - 对这些数字求和。
    - 将 `production[plant_number - 1]` 设置为总和。

### input_data 的编码

`input_data` 函数的算法转换为以下代码：

```cpp
// 使用 iostream
void input_data(int a[ ], int last_plant_number)
{
    using namespace std;
    for (int plant_number = 1;
        plant_number <= last_plant_number; plant_number++)
    {
        cout << "Enter production data for plant number" << plant_number << endl;
        get_total(a,plant_number - 1);
    }
}
```

代码是常规的，因为所有的工作由 `get_total` 函数完成，但在讨论 `get_total` 函数之前，让我们观察一下 `input_data` 函数的几点。注意，我们将 `plant_number` 号的数据存储在索引为 `plant_number-1` 的变量中；这是因为数组从 0 开始，而工厂从 1 开始。此外，注意 `get_total` 函数的参数索引变量。`get_total` 函数实际上完成了 `input_data` 函数的工作。

`get_total` 函数完成一个工厂的工作。它读取该工厂的产量数据，存储这些数据，并将总和存储在工厂的索引变量中。但 `get_total` 不需要知道其参数是一个索引变量。对于 `get_total` 来说，索引变量与任何 `int` 类型变量一样。因此，`get_total` 将有一个普通的 `int` 类型引用传递参数。这意味着

# 数组

# 显示 5 图程序大纲

```cpp
// 读取数据并显示每个工厂产量的柱状图。
#include <iostream>
const int NUMBER_OF_PLANTS = 4;

void input_data(int a[], int last_plant_number);
// 前提：last_plant_number 是数组 a 的大小。
// 后置条件：对于 plant_number = 1 直到 last_plant_number，
// a[plant_number - 1] 等于该工厂的总产量。

void scale(int size);
// 前提：a[0] 到 a[size-1] 均为非负值。
// 后置条件：对于所有 0 <= i < size - 1，
// a[i] 已更改为原始在 a[i] 中的千位（四舍五入为整数）。

void graph(int asterisk_count[], int last_plant_number);
// 前提：asterisk_count[0] 到 asterisk_count[last_plant_number-1]
// 均为非负值。
// 后置条件：显示了一个柱状图，说明
// 每个工厂产了 asterisk_count[N-1] 千单位，对于每个 1 <= N <= last_plant_number

int main() {
	using namespace std;
	cout << "This program displays a graph showing\n";
	cout << "production for each plant in\n";
	input_data(production, NUMBER_OF_PLANTS);
	scale(production, NUMBER_OF_PLANTS);
	graph(production, NUMBER_OF_PLANTS);
	return 0;
}
```

`get_total` 完成一个工厂的工作。它读取该工厂的产量数据，存储这些数据，并将总和存储在工厂的索引变量中。但 `get_total` 不需要知道其参数是一个索引变量。对于 `get_total` 来说，索引变量与任何 `int` 类型变量一样。因此，`get_total` 将有一个普通的 `int` 类型引用传递参数。这意味着

# 数组

# 测试输入数据

程序中的每个函数都应该经过测试。`input_data` 函数应该对各种产量进行测试。在测试 `input_data` 时，我们应该包括

- 没有产量的工厂。
- 只有一个产量数据的工厂。
