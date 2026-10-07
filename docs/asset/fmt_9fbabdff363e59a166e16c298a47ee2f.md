
```cpp
46 #include <iostream>
47 int get_one_total() {
48     int total;
49     cout << "Enter the number of eggs in each nest:\n";
50     cout << "Place a negative integer ";
51     cout "at the end of your list:\n";
52
53     total = 0;
54     int next;
55     cin >> next;
56     while (next >= 0) {
57         total = total + next;
58         cin >> next;
59     }
60     return total;
61 }
```

## 示例对话

每个保护人员的报告由数字列表组成。每个数字都是在一个绿颈秃龟巢中观察到的蛋的数量。程序随后计算总数。
How many conservationist reports are there? 3
Enter the report of conservationist number 1
Enter the number of eggs in each nest:
Place a negative integer at the end of your list: -1
Total egg count for conservationist 1 is 3
Enter the report of conservationist number 2
Enter the number of eggs in each nest:
Place a negative integer at the end of your list: -1
Total egg count for conservationist 2 is 4
Enter the report of conservationist number 3
Enter the number of eggs in each nest:
Place a negative integer at the end of your list: -1
Total egg count for conservationist 3 is 0
Total egg count for all reports = 7

## 过程抽象与返回值的函数

### 示例 9 良好的嵌套循环（3部分中的第3）

## 案例研究购买披萨

“经济型”尺寸并不总是比小尺寸好。在购买披萨时尤其如此。披萨的尺寸是以英寸给出的，但披萨的数量是由面积决定的，而面积与直径不成正比。大多数人无法轻易估计10英寸披萨和12英寸披萨之间的面积差异，也无法判断哪个更划算。在这个案例中，我们将设计一个比较两种尺寸披萨的程序来判断哪个更好。

### 问题定义

程序输入输出的精确规范如下：

### 输入

输入将包括两种披萨的英寸直径和价格。

### 输出

输出将给出两种披萨的每英寸成本，并告知哪个更划算，即每英寸成本最低。（如果每英寸成本相同，我们认为较小的更划算。）

### 问题分析

我们使用自顶向的设计将程序要解决的任务分为以下子任务：

- 子任务 1：获取大、小披萨的输入数据。
- 子任务 2：计算小披萨的每英寸成本。
- 子任务 3：计算大披萨的每英寸成本。
- 子任务 4：判断哪个更划算。
- 子任务 5：输出结果。

### 子任务 2 和 3

注意子任务 2 和 3。它们有两个重要的属性：

1. 它们是完全相同的任务。区别在于它们使用不同的数据进行计算。子任务 2 和子任务 3 之间变化的是披萨的尺寸和价格。
2. 子任务 2 的结果和子任务 3 的结果都是单一值：披萨的每英寸成本。

### 何时定义函数

当子任务接收某些值（如某些数字）并返回单一值时，将该子任务实现为函数是自然的。当两个或多个子任务执行相同的计算时，它们可以通过每次使用时不同参数的同一个函数来实现。因此，我们决定使用函数 `unitprice` 来计算披萨的每英寸成本。该函数的声明和解释性注释如下：

```
double unitprice(int diameter, double price);

// 返回披萨的每英寸成本。

// 参数名为 diameter 是披萨的英寸直径。

// 形式参数名为 price 是披萨的价格。
```

子任务 1：子任务 1 非常简单。程序将只需请求输入值并将其存储四个变量中，我们将其称为 `diameter_small`、`diameter_large`、`price_small` 和 `price_large`。

子任务 4 和 5：子任务 4 是常规操作。为了确定哪种披萨最划算，我们使用小于运算符比较两种披萨的每英寸成本。子任务 5 是结果的常规输出。

子任务 2 和 3：子任务 2 和 3 实现为对 `unitprice` 的调用。接下来，我们为该函数设计算法。算法困难的部分是确定披萨的面积。一旦知道了面积，我们就可以通过除法轻松地确定每英寸成本，如下：

`price/area`

其中 `area` 是存储披萨面积的变量。这个表达式将由 `unitprice` 函数返回。但我们仍然需要一种计算披萨面积的方法。

披萨基本上是一个圆（由饼壳、奶酪、酱料等组成）。圆（以及披萨）的面积为 $\pi r^2$，其中 $r$ 是圆的半径，$\pi$ 是被称为“圆周率”的数字，约等于3.14159。半径是直径的一半。

# 过程抽象与返回值的函数

在将大纲翻译成 C++ 代码之前，我们将对该大纲进行更详细的说明。我们将用伪代码来表达这个更详细的算法版本。伪代码是 C++ 和普通英语的混合体。伪代码允许我们在不担心 C++ 语法细节的情况下，使我们的算法精确化。然后，我们就可以将伪代码翻译成 C++ 代码。在我们的伪代码中，`radius` 和 `area` 将用于存储其名称所指数值的变量。

# 函数 unitprice 的伪代码

```
radius = one half of diameter;

area = π * radius;

return (price/area);
```

我们的 `unitprice` 的大纲到此完成。我们现在准备好将子任务 1 到 5 的解决方案转换为一个完整的 C++ 程序了。

# 编码

子任务 1 的编码是常规操作，因此我们接下来考虑子任务 2 和 3。我们的程序可以通过对函数 `unitprice` 的以下两次调用来实现任务 2 和 3：

```
unitprice_small = unitprice(diameter_small, price_small);

unitprice_large = unitprice(diameter_large, price_large);
```

其中 `unitprice_small` 和 `unitprice_large` 是两个 `double` 类型的变量。函数定义的好处之一是你可以在程序中多次调用该函数。这节省了你重复相同（或几乎相同）代码的麻烦。但我们仍然必须为函数 `unitprice` 编写代码。

当我们将伪代码翻译成 C++ 代码时，我们得到了 `unitprice` 函数体的以下内容：

```
//First draft of the function body for unitprice

const double PI = 3.14159;

double radius, area;

radius = diameter/2;

a = PI * radius;

return (price/area);
```

注意，我们使用 `const` 修饰符将 `PI` 设为了命名常量。此外，请注意代码中的以下行：

```
radius = diameter/2;
```

这只是一个简单的除以 2 的操作，你可能认为没有比这更常规的操作了。但正如写所示，这一行包含一个严重的错误。我们希望除法能产生披萨的半径，包括任何小数部分。

# 过程抽象与返回值的函数

例如，如果我们正在考虑购买“倒霉特惠款”（这是一个 13 英寸的披萨），那么半径就是 6.5 英寸。但变量 *diameter* 的类型是 *int*。常量 2 也是 *int* 类型。因此，这一行代码将执行整数除法，并计算出 13/2 的结果为 6 而不是正确的数值 6.5，这导致我们忽略了半英寸的披萨半径。在极可能的情况下，这不会被察觉，但结果可能是披萨消费者联盟的数百万订阅者因购买错误尺寸的披萨而浪费金钱。这不太可能导致全球经济衰退，但程序将无法实现帮助消费者找到最佳购买目标的目标。这样一个简单的错误结果可能是灾难性的。

我们该如何修复它？我们希望除以 2 的除法是普通除法，在答案中包含任何小数部分。那种形式的除法要求至少有一个参数是 *double* 类型。我们可以使用类型转换将常量 2 转换为 *double* 类型的值。回想 *static_cast<double>(2)*，这被称为类型转换，它将 `int` 值 2 转换为 *double* 类型的值。因此，如果我们将 2 替换为 *static_cast<double>(2)*，那么除法中的第二个参数将产生我们想要的结果。重写的赋值语句是：

```
radius = diameter/static_cast<double>(2);
```

函数 `unitprice` 的完整代码以及程序的其余部分显示在显示 10 中。
类型转换 *static_cast<double>(2)* 返回值 2.0，因此我们可以用 2.0 代替 *static_cast<double>(2)*。无论哪种方式，函数 `unitprice` 将返回相同的值。然而，通过使用 *static_cast<double>(2)*，我们显而易见地表明我们想要进行包含小数部分的除法版本。如果我们使用 2.0，那么在修改或复制代码时，我们很容易犯将 2.0 改为 2 的错误，这会产生一个微妙的问题。

关于程序的编码，我们还需要说明一点。正如你在显示 10 中所示，我们编写了任务 4 和 5，我们将这两个任务合并成了一个代码部分，该部分由一系列代码语句后面紧跟一个 *if-else* 语句组成。当两个任务非常简单且密切相关时，将它们合并成一个任务有时是有意义的。

# 程序测试

仅仅程序通过了编译并产生了看起来正确的答案，并不意味着程序是正确的。为了增加你对程序的信心，你应该在某些输入值上对其进行测试，你通过其他方式知道这些值的正确答案，例如用纸笔计算答案或使用手持计算器。例如，购买一个 2 英寸的披萨是没有意义的，但它仍然可以用于：

# 过程抽象与返回值的函数

# 显示 10 购买披萨（第一部分，共 2 部分）

```
//确定两种披萨尺寸中哪种最划算。

#include <iostream>

using namespace std;

double unitprice(int diameter,double price);

//返回披萨每平方英寸的价格。

int main() {

    int diameter_small, diameter_large;

    double price_small, price_large;
```
显示 10 购买披萨（第一部分，共 2 部分）

```
//确定两种披萨尺寸中哪种最划算。

#include <iostream>

using namespace std;

double unitprice(int diameter,double price);

//返回披萨每平方英寸的价格。

int main() {

    int diameter_small, diameter_large;

    double price_small, price_large;
```

（注：此处原文文本在显示 10 处出现中断和重复，根据逻辑翻译完整内容）

**显示 10 购买披萨（第一部分，共 2 部分）**

```
//确定两种披萨尺寸中哪种最划算。

#include <iostream>

using namespace std;

double unitprice(int diameter,double price);

//返回披萨每平方英寸的价格。

int main() {

    int diameter_small, diameter_large;

    double price_small, price_large;

    double unitprice_small, unitprice_large;

    cout << "Welcome to the Pizza Union\n";

    cout << "Enter diameter of a small pizza (inches): ";

    cin >> diameter_small;

    cout << "Enter the price of small pizza: $";

    cin >> price_small;

    cout << "Enter diameter of a large pizza (inches): ";

    cin >> diameter_large;

    cout << "Enter the price of large pizza: $";

    cin >> price_large;

    unitprice_small = unitprice(diameter_small, price_small);

    unitprice_large = unitprice(diameter_large, price_large);

    cout << fixed;

    cout.precision(2);

    cout << "Small pizza: " << diameter_small << " inches\n";

    cout << "Price: $" << price_small << "\n";

    cout << "Per square inch: $" << unitprice_small << "\n";

    cout << "Large pizza: " << diameter_large << " inches\n";

    cout << "Price: $" << price_large << "\n";

    cout << "Per square inch: $" << unitprice_large << "\n";

    if (unitprice_large < unitprice_small)

        cout << "The large one is the better buy.\n";

    else

        cout << "The small one is the better buy.\n";

    cout << "Bon Appetito!\n";

    return 0;

}
```
（注：由于原始文本在显示 10 处存在严重的格式混乱和重复，上述译文基于文档工程师的逻辑对代码块和结构进行了整理，以确保逻辑连贯。）

**更正基于提供的凌乱文本，完整翻译如下：**

# 过程抽象与返回值的函数

# 显示 10 购买披萨（第一部分，共 2 部分）

```cpp

//确定两种披萨尺寸中哪种最划算。

#include <iostream>

using namespace std;

double unitprice(int diameter,double price);

//返回披萨每平方英寸的价格。

int main() {

    int diameter_small, diameter_large;

    double price_small, price_large;

    double unitprice_small, unitprice_large;

    cout << "Welcome to the Pizza Union\n";

    cout << "Enter diameter of a small pizza (inches): ";

    cin >> diameter_small;

    cout << "Enter the price of small pizza: $";

    cin >> price_small;

    cout << "Enter diameter of a large pizza (inches): ";

    cin >> diameter_large;

    cout << "Enter the price of large pizza: $";

    cin >> price_large;

    unitprice_small = unitprice(diameter_small, price_small);

    unitprice_large = unitprice(diameter_large, price_large);

    cout << fixed;

    cout.precision(2);

    cout << "Small pizza: " << diameter_small << " inches\n";

    cout << "Price: $" << price_small << "\n";

    cout << "Per square inch: $" << unitprice_small << "\n";

    cout << "Large pizza: " << diameter_large << " inches\n";

    cout << "Price: $" << price_large << "\n";

    cout << "Per square inch: $" << unitprice_large << "\n";

    if (unitprice_large < unitprice_small)

        cout << "The large one is the better buy.\n";

    else
```
