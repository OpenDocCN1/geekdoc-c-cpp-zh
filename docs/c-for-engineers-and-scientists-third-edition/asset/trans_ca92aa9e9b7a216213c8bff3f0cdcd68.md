

## 330 使用函数的模块化

两个变量之间的值交换是通过使用三步交换算法完成的：

- 1. 将第一个参数的值保存在临时位置（见图 6.9a）。
- 2. 将第二个参数的值存储在第一个变量中（见图 6.9b）。
- 3. 将临时值存储在第二个参数中（见图 6.9c）。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_349_0.png)

图 6.9a 保存第一个值

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_349_1.png)

图 6.9b 用第二个值替换第一个值

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_349_2.png)

图 6.9c 改变第二个值

以下是根据这些规范编写的 swap() 函数：

```cpp
void swap(double& num1, double& num2)
{
    double temp;

    temp = num1;      // 保存 num1 的值
    num1 = num2;      // 将 num2 的值存储在 num1 中
    num2 = temp;      // 改变 num2 的值

    return;
}
```

注意 swap 头文件中引用的使用使得 swap() 可以访问调用函数中的等效参数。因此，swap() 中对两个引用参数的任何更改都会自动改变调用函数中参数的值。程序 6.10 包含一个完整程序中的 swap()。

## 第 6 章

## 331 返回多个值

### 程序 6.10

```cpp
#include <iostream>
using namespace std;

void swap(double&a, double&b); // 函数接收两个引用

int main()
{
    double firstnum = 20.5, secnum = 6.25;

    cout << "The value stored in firstnum: " << firstnum << endl;
    cout << "The value stored in secnum: " << secnum << "\n\n";

    swap(firstnum, secnum); // 使用引用调用函数

    cout << "The value stored in firstnum is now: "
    << firstnum << endl;
    cout << "The value stored in secnum is now: "
    << secnum << endl;

    return 0;
}

void swap(double&num1, double&num2)
{
    double temp;
    temp = num1; // 保存 num1 的值
    num1 = num2; // 将 num2 的值存储在 num1 中
    num2 = temp; // 改变 num2 的值

    return;
}
```

以下是程序 6.10 的示例运行：

The value stored in firstnum is: 20.5
The value stored in secnum is: 6.25

The value stored in firstnum is now: 6.25
The value stored in secnum is now: 20.5

如程序 6.10 的输出所示，main() 变量中的值在 swap() 内部被修改了，这是通过使用引用参数实现的。如果使用按值传递，那么 swap() 中的交换将只会影响 swap() 的参数，而对 main() 的变量产生任何影响。像 swap() 这样的函数只有通过使用引用或其他某种提供访问 main() 变量的其他方法才能编写。（这种其他方法是指针，这是第 12 章的主题。）

在使用引用时，需要提到两点注意事项。首先，引用参数必须是引用的（即，它们不能用于更改常量）。例如，用两个字面量调用 swap()，如在调用 `swap(20.5, 6.5)` 中，向函数传递了两个常量。然而，尽管 swap() 可以执行，但它不会改变这些常量的值。

其次，函数调用指示了返回值将是引用形式。在 C++ 中，这是通过引用而不是按引用传递来实现的，特别地限于被调用的函数()。每尽可能都应遵循这一调用过程，这意味着引用参数应该只在需要多个返回值的限制情况下使用，如程序 6.10 中的 swap() 函数。程序 6.9 中包含的 calc() 函数虽然为了说明有用，但可以写成两个独立的函数，每个函数返回一个值。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_351_0.png)

## 练习 6.3

- 1. (练习) 为以下内容编写参数声明：
   a. 一个名为 *slope* 的参数，将是双精度引用
   b. 一个名为 *energy* 的参数，将是双精度引用
   c. 一个名为 *minutes* 的参数，将是整数引用
   d. 一个名为 *key* 的参数，将是双精度引用
   e. 一个名为 *yield* 的参数，将是双精度引用
- 2. (练习) 使用三个整数参数调用 time() 函数，假设它接收 sec, min 和 hours
- 3. (修改) 重写程序 6.5 中的 findMax() 函数，使得 main() 中声明的变量 max 用于存储两个数字中的最大值。（提示：findMax() 接收 max 的引用 ）。
- 4. (练习) 编写一个名为 *change* 的函数，它有一个整数参数和三个引用参数 *hundreds*, *twenties*, *fives*, *ones*。
- 5. (练习) 编写一个名为 *time* 的函数，它有一个整数参数和引用参数 hours, mins 和 secs。

> ¹³大多数编译器会捕捉此错误。

## 第 6 章 333 直角坐标到极坐标的案例研究

## 6.4 直角坐标到极坐标的案例研究

准备一个良好的程序就像准备论文一样，从一个大纲开始。这个大纲可以写下来，对于小型程序，也可以记在脑子里。在任务定义清楚之后，就可以按照任何顺序开始编码。如果任务超过一个程序员的范围，就可以将其分配给多个程序员。这种工作负载分配等同于很多人参与一个大型项目，每个人负责一个特定的组件。适用于许多工程科学任务的通用大纲如下算法：

- 获取问题的输入
- 计算结果
- 报告结果

这三个任务是每个程序的主要职责，这个算法被称为问题解决算法。图 6.10 显示了它的初级结构图。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_353_0.png)

**图 6.10** 问题解决算法

### **第一步** 问题定义

要编写一个程序，将点的直角坐标 (x,y) 转换为极坐标。也就是说，给定笛卡尔坐标系（如图 6.11 所示）中的 x 和 y 位置，你必须计算到原点的距离 $r$ 以及点相对于 x 轴的角 $\theta$。$r$ 和 $\theta$ 的值被称为该点的极坐标。

当已知 x 和 y 坐标时，可以使用以下公式计算等效的 $r$ 和 $\theta$ 坐标：

```
$r = \sqrt{x^2 + y^2}$
$\theta = \tan^{-1}(y/x) \quad x \neq 0$
```

