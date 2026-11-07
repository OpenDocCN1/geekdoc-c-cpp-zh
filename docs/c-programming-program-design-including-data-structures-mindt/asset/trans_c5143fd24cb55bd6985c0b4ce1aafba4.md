

```cpp
    if (numOfItems < 0)                         //第9行
        throw numOfItems;                       //第10行

    cout << "Enter the cost of one item: ";    //第11行
    cin >> unitCost;                            //第12行
    cout << endl;                               //第13行

    if (unitCost < 0)                           //第14行
        throw unitCost;                         //第15行

    cout << "Total cost: $"                     //第16行
         << numOfItems * unitCost << endl;      //第16行
}                                               //第17行
catch (int num)                                 //第18行
{                                               //第19行
    cout << "Negative number of items: " << num //第20行
         << endl;
    cout << "Number of items must be nonnegative." //第21行
         << endl;                               //第21行
}                                               //第22行
catch (double dec)                              //第23行
{                                               //第24行
    cout << "Negative unit cost: " << dec       //第25行
         << endl;
    cout << "Unit cost must be nonnegative."    //第26行
         << endl;
}                                               //第28行
```

- a. 在这段代码中，指出`try`块。
- b. 在这段代码中，指出`catch`块。
- c. 在这段代码中，指出`catch`块参数及其类型。
- d. 在这段代码中，指出`throw`语句。

13. 假设习题12中给出的代码。（3，4）

- a. 如果输入是`25 5.50`，输出是什么？
- b. 如果输入是`-55 2.8`，输出是什么？
- c. 如果输入是`37 -4.5`，输出是什么？
- d. 如果输入是`-10 -2.5`，输出是什么？

14. 考虑以下C++代码：（3，4）

```cpp
int lowerLimit;

try
{
    cout << "Entering the try block." << endl;

    if (lowerLimit < 100)
        throw exception("Lower limit violation.");

    cout << "Exiting the try block." << endl;
}
catch (exception eObj)
{
    cout << "Exception: " << eObj.what() << endl;
}
cout << "After the catch block" << endl;
```

如果出现以下情况，输出是什么：

- a. `lowerLimit`的值是50？
- b. `lowerLimit`的值是150？

15. 考虑以下C++代码：（3，4）

```cpp
int totalScore;
int numOfTests;

try
{
    if (numOfTests == 0)
        throw 0;
    if (totalScore < 0 || totalScore > 400)
        throw string("Total score is out of range.");

    cout << totalScore / numOfTests << endl;
    cout << "Exiting the try block." << endl;
}
catch (int x)
{
    cout << "Exception: Division by " << x << endl;
}
catch (string str)
{
    cout << "Exception: " << str << endl;
}
```

如果出现以下情况，输出是什么：

- a. `totalScore`的值是275，`numOfTests`的值是5？
- b. `totalScore`的值是300，`numOfTests`的值是0？
- c. `totalScore`的值是-175，`numOfTests`的值是5？
- d. `totalScore`的值是-250，`numOfTests`的值是0？

16. 说出C++中专门用于处理异常的基类。（5）

- a. 哪个类用于处理字符串下标越界？（5）
- b. 当字符串对象的长度超过最大允许长度时，使用哪个类？
- c. 哪个类用于处理只能在程序执行期间检测到的错误？

18. 如果你定义自己的异常类，该类中通常包含什么？（6）

- 19. 什么类型的语句用于重新抛出异常？（7）
- 20. 定义一个名为`tornadoException`的异常类。该类应包含两个构造函数，包括默认构造函数。如果使用默认构造函数抛出异常，`what`方法应返回**“Tornado: Take cover immediately!”**。另一个构造函数有一个`int`类型的参数，比如`m`。如果使用此构造函数抛出异常，`what`方法应返回**“Tornado: m miles away; and approaching!”**。（6，7）
- 21. 编写一个C++程序来测试习题20中指定的`tornadoException`类。（6，7）
- 22. 假设异常类`myException`定义如下：（6，7）

```cpp
class myException
{
public:
    myException()
    {
        message = "myException thrown!";
        cout << "Immediate attention required!"
             << endl;
    }

    myException(string msg)
    {
        message = msg;
        cout << "Attention required!" << endl;
    }

    string what()
    {
        return message;
    }

private:
    string message;
};
```

假设在用户程序中，`catch`块的形式如下：

```cpp
catch (myException eM)
{
    cout << eM.what() << endl;
}
```

如果使用默认构造函数抛出异常，将产生什么输出？另外，如果使用带有以下实际参数的构造函数抛出异常，将产生什么输出？

“May Day, May Day”

- 23. 如果一个函数抛出异常，它如何指定该异常？（7）
- 24. 说出三种异常处理技术。（8）
- 25. 假设在函数中抛出了一个异常。该函数可以做的三件事是什么？（9）

### 编程练习

- 1. 编写一个程序，提示用户输入以英尺和英寸为单位的长度，并输出等效的厘米长度。如果用户输入负数或非数字，则抛出并处理适当的异常，并提示用户输入另一组数字。
- 2. 重做第4章编程练习8，使你的程序能够处理诸如除零和无效输入之类的异常。
- 3. 重做第7章编程练习7，使你的程序能够处理诸如除零和无效输入之类的异常。
- 4. 编写一个程序，提示用户以12小时制输入时间。然后程序以24小时制输出时间。你的程序必须包含三个异常类：`invalidHr`、`invalidMin`和`invalidSec`。如果用户输入了无效的小时值，程序应抛出并捕获一个`invalidHr`对象。对于无效的分钟和秒值，遵循类似的约定。
- 5. 编写一个程序，提示用户以数字形式输入某人的出生日期，例如8-27-1980。然后程序以以下形式输出出生日期：August 27, 1980。你的程序必须至少包含两个异常类：`invalidDay`和`invalidMonth`。如果用户输入了无效的日值，程序应抛出并捕获一个`invalidDay`对象。对于无效的月和年值，遵循类似的约定。（注意：你的程序必须处理闰年。）

## 第15章
## 递归

![](img/b217c421655b51e7494cf3b89bb5432d_1100_0.png)

© HunThomas/Shutterstock.com

在本章中，你将：

- 1. 学习递归定义
- 2. 探索递归定义中的基线条件（base case）和一般条件（general case）
- 3. 了解什么是递归算法
- 4. 学习递归函数
- 5. 熟悉直接递归和间接递归
- 6. 探索如何使用递归函数实现递归算法
- 7. 了解递归与迭代的区别

在前面的章节中，为了设计问题的解决方案，我们使用了最常见的技术——迭代。然而，对于某些问题，使用迭代技术来获得解决方案相当复杂。本章介绍另一种问题求解技术——递归，并提供几个示例演示递归如何工作。

### 递归定义

通过将问题归约为其自身较小的版本来求解问题的过程称为**递归**。对于某些问题，递归是一种非常强大的求解方式，否则解决方案会非常复杂。让我们考虑一个大多数人都熟悉的问题。

在数学中，非负整数的阶乘定义如下：

0! = 1                         (15-1)

n! = n × (n - 1)! 如果 n > 0       (15-2)

在这个定义中，0! 被定义为1，如果n是大于0的整数，首先我们求 (n - 1)!，然后将其乘以n。为了求 (n - 1)!，我们再次应用该定义。如果 (n - 1) > 0，则使用公式15-2；否则，使用公式15-1。因此，对于大于0的整数n，n! 是通过先求 (n - 1)!（即 n! 被归约为自身较小的版本），然后将 (n - 1)! 乘以n得到的。

让我们应用这个定义来求3!。这里，n = 3。因为 n > 0，我们使用公式15-2得到

3! = 3 × 2!

接下来，我们求2!。这里，n = 2。因为 n > 0，我们使用公式15-2得到

2! = 2 × 1!

现在，为了求1!，我们再次使用公式15-2，因为 n = 1 > 0。因此

1! = 1 × 0!

最后，我们使用公式15-1求0!，其值为1。将0!代入1!得到 1! = 1。这给出 2! = 2 × 1! = 2 × 1 = 2，进而给出 3! = 3 × 2! = 3 × 2 = 6。

公式15-1中的解是直接的——也就是说，等号右边不包含阶乘符号。公式15-2中的解是以自身较小版本的形式给出的。公式15-1和15-2中给出的阶乘定义称为**递归定义**。公式15-1称为**基线条件**（即直接获得解的情况），公式15-2称为**一般条件**。**递归定义：** 一种以自身较小版本来定义某个事物的定义。

从前面的示例（阶乘）可以清楚地看出：

- 1. 每个递归定义必须有一个（或多个）基线条件。

