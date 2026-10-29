

## 自测练习（续）

32. 这个循环的输出是什么？请对代码进行注释。（这与前面的练习不同。）

```
int n = 1024;
int log = 0;
for (int i = 1; i < n; i = i * 2) {
    log++;
}
cout << n << " " << log << endl;
```

33. 这个循环的输出是什么？请对代码进行注释。（这与前面两个练习都不同。）

```
int n = 1024;
int log = 0;
for (int i = 0; i < n; i = i * 2) {
    log++;
}
cout << n << " " << log << endl;
```

34. 针对以下每种情况，说明哪种循环类型（while、do-while 或 for）最合适。

- a. 对一个数列求和，例如 1/2 + 1/3 + 1/4 + 1/5 + ... + 1/10。
- b. 读取一名学生的考试成绩列表。
- c. 读取一个部门员工请病假的天数。
- d. 测试一个函数，观察其在不同参数值下的表现。

35. 以下代码的输出是什么？（x 是 int 类型。）

```
int x = 10;
while (x > 0)
{
    cout << x << endl;
    x = x + 3;
}
```

## break 和 continue 语句

在前面的小节中，我们描述了 while、do-while 和 for 循环的基本控制流程。这是循环的正常使用方式，也是通常的使用方式。不过，你可以通过两种方式改变控制流程，在少数情况下，这是一种有用且安全的技术。这两种改变控制流程的方式是插入 break 或 continue 语句。break 语句结束整个循环。continue 语句结束循环体的当前迭代。break 语句可用于 C++ 的任何循环语句。

我们在讨论 switch 语句时已经介绍过 break 语句。break 语句由关键字 break 后跟一个分号组成。执行时，break 语句会结束最近的封闭 switch 或循环语句。显示 2.8 包含一个 break 语句的示例，当输入不合适的值时，该语句会结束循环。

## 显示 2.8 循环中的 break 语句

```
1 #include <iostream>
2 using namespace std;

3 int main( )
4 {
5     int number, sum = 0, count = 0;
6     cout << "Enter 4 negative numbers:\n";

7     while (++count <= 4)
8     {
9         cin >> number;

10        if (number >= 0)
11        {
12            cout << "ERROR: positive number";
13            cout << " or zero was entered as the\n";
14            cout << count << "th number! Input ends ";
15            cout << "with the " << count << "th number.\n";
16            cout << count << "th number was not added in.\n";
17            break;
18        }
19        sum = sum + number;
20    }

21    cout << sum << " is the sum of the first "
22        << (count - 1) << " numbers.\n";

23    return 0;
24 }
```

## 示例对话

Enter 4 negative numbers:
-1 -2 -3 4
ERROR: positive number or zero was entered as the 4th number! Input ends with the 4th number.
4th number was not added in.
-6 is the sum of the first 3 numbers.

## continue 语句

continue 语句由关键字 continue 后跟一个分号组成。执行时，continue 语句会结束最近的封闭循环语句的当前循环体迭代。显示 2.9 包含一个含有 continue 语句的循环示例。

## 显示 2.9 循环中的 continue 语句

```
1 #include <iostream>
2 using namespace std;

3 int main() {
4 {
5     int number, sum = 0, count = 0;
6     cout << "Enter 4 negative numbers, ONE PER LINE:\n";
7     while (count < 4)
8     {
9         cin >> number;
10        if (number >= 0)
11        {
12            cout << "ERROR: positive number (or zero)!\n";
13            cout << "Reenter that number and continue:\n";
14            continue;
15        }
16        sum = sum + number;
17        count++;
18    }
19    cout << sum << " is the sum of the "
20    << count << " numbers.\n";
21    return 0;
22 }
```

## 示例对话

```
Enter 4 negative numbers, ONE PER LINE:
1
ERROR: positive number (or zero)!
Reenter that number and continue:
-1
-2
3
ERROR: positive number!
Reenter that number and continue:
-3
-4
-10 is the sum of the 4 numbers.
```

在 for 循环中使用 continue 语句时，需要注意的一点是：continue 语句会将控制权转移到更新表达式。因此，在 continue 语句执行后，任何循环控制变量都会立即被更新。

请注意，break 语句会完全结束循环。相比之下，continue 语句仅仅结束一次循环迭代；下一次迭代（如果有的话）会继续循环。对比显示 2.8 和 2.9 中程序的细节，你会发现很有启发。请特别注意控制布尔表达式的变化。

请注意，你并非绝对需要 break 或 continue 语句。显示 2.8 和 2.9 中的程序可以重写，使两者都不使用 break 或 continue 语句。continue 语句可能特别棘手，并且可能使你的代码难以阅读。最好完全避免使用 continue 语句，或者至少只在极少数情况下使用。

## 嵌套循环

在一个循环语句内部嵌套另一个循环语句是完全合法的。这样做时，请记住，任何 break 或 continue 语句都适用于包含该 break 或 continue 语句的最内层循环（或 switch）语句。最好通过将内层循环放在函数定义中，并在外层循环中放置函数调用来避免嵌套循环。我们将在第 3 章介绍如何编写自己的函数。

## 自测练习

- 36. break 语句的作用是什么？在何处放置 break 语句是合法的？
- 37. 预测以下嵌套循环的输出：

```
int n, m;
for (n = 1; n <= 10; n++)
    for (m = 10; m >= 1; m--)
        cout << n << " times " << m
             << " = " << n * m << endl;
```

## 2.4 文件输入简介

> 你将在精美的四开页上看到它们，一条整齐的文字小溪蜿蜒流过木兰花的草地。

> 理查德·布林斯利·谢里丹，《造谣学校》。第一幕，第一场。1777年

到目前为止，你应该已经熟悉使用 cin 从键盘读取数据。cin 是所谓输入流的一个例子。我们还可以将输入流连接到磁盘上的文件。一旦设置完成，我们就可以几乎以与从 cin 读取完全相同的方式从文件中读取。关于从文件读取和写入文件的细节要到第 12 章才讨论，并且需要理解我们尚未涵盖的编程概念。不过，我们可以在这里提供足够的内容，使你的程序能够从文本文件中读取。这将使你能够处理具有真实世界数据的问题，否则每次运行程序时手动输入这些数据的工作量会太大。

![](img/c76bba8c1d927f399768ffe2ab5f5bee_113_0.png)

## 使用 ifstream 从文本文件读取

文本文件是以文本格式存储的文件。你可以使用 Windows 中的记事本、Mac 上的 TextEdit 或 UNIX 机器上的 vi/nano/emacs 等程序创建它们。大多数文字处理器和许多其他程序也会以文本格式保存文件。

要从文本文件读取，我们需要包含 fstream 库，并创建一个位于 std 命名空间中的 ifstream 对象。因此，你的程序应包含

```
#include <fstream>
using namespace std;
```

然后，你可以像声明任何其他变量一样声明一个输入流：

```
ifstream inputStream;
```

接下来，你必须将 inputStream 变量连接到磁盘上的文本文件：

```
inputStream.open("filename.txt");
```

在指定文件名时，你可以指定路径名（目录或文件夹）。指定路径名的细节因系统而异，因此请咨询当地的专家以了解详细信息（或进行一些试错编程）。在我们的示例中，我们将使用简单的文件名，这假定文件与程序运行的目录（文件夹）相同。

一旦你声明了输入流变量并使用 open 函数将其连接到文件，你的程序就可以使用提取运算符 >> 从文件中获取输入，方式与 cin 相同。

例如，你可以使用 inputStream >> intVar 从文件中读取整数，使用 inputStream >> strVar 从文件中读取字符串（直到空白字符），等等。C++ 从文件开头开始读取，并在读取数据时向文件末尾推进。当程序完成文件操作后，应使用 inputStream.close( ) 关闭文件，这将释放与该文件关联的所有已分配资源。

