

Q: 一个函数中可以有多个 return 语句吗？

A: 当然可以。事实上，你可能希望使用多个 return 语句来指定函数的不同结束点。

Q: 什么是局部变量？

A: 在某个作用域中定义的变量。函数中定义的所有变量都是局部变量；它们对该函数是局部的。

Q: 隐藏一个变量是什么意思？

A: 当你在新的作用域中用与外部作用域中变量相同的名称声明它时，该变量就被隐藏了。结果是，你无法通过在内部作用域中使用其变量名来访问外部作用域中的变量。

Q: 变量何时超出作用域？

A: 变量在其被创建的作用域结束时超出作用域。

Q: 变量超出作用域是什么意思？

A: 这意味着变量不再存在。

Q: 什么是嵌套作用域？

A: 在现有作用域内创建的作用域。

Q: 参数必须与传递给它的参数名相同吗？

A: 不必。你可以自由使用不同的名称。只有值是从函数调用传递到函数。

Q: 我可以编写一个函数调用另一个函数吗？

A: 当然可以。事实上，每当你编写一个从 main() 调用的函数时，你就是在这样做。此外，你可以编写一个（除 main() 之外的）函数来调用另一个函数。

Q: 什么是代码分析？

A: 它是记录程序各个部分使用多少 CPU 时间的过程。

Q: 为什么要分析代码？

A: 为了确定程序中的任何瓶颈。有时重新审视这些代码段以尝试优化它们是有意义的。

Q: 程序员何时分析代码？

A: 通常在游戏项目编程接近尾声时。

Q: 什么是过早优化？

A: 在开发过程过早地尝试优化代码。代码优化通常在游戏项目编程接近尾声时才有意义。

### Discussion Questions

- 1. 函数封装如何帮助你编写更好的程序？
- 2. 全局变量如何使代码变得混乱？
- 3. 全局常量如何使代码更清晰？
- 4. 优化代码的利弊是什么？
- 5. 软件重用如何使游戏行业受益？

### Exercises

- 1. 以下原型有什么问题？

```
int askNumber(int low = 1, int high);
```

- 2. 使用函数重写第 4 章的 Hangman 游戏。包含一个用于获取玩家猜测的函数，以及另一个用于确定玩家猜测是否在秘密单词中的函数。

- 3. 使用默认参数，编写一个函数，要求用户输入一个数字并返回该数字。函数应从调用代码接受一个字符串提示。如果调用者未提供字符串提示，函数应使用通用提示。接下来，使用函数重载，编写一个实现相同结果的函数。

## CHAPTER 6: REFERENCES: Tic-Tac-Toe

![](img/34f09be0ed6217c465debc4490197d4f_209_0.png)

引用的概念很简单，但其影响是深远的。在本章中，你将学习引用以及它们如何帮助你编写更高效的游戏代码。具体来说，你将学习如何：

- 创建引用
- 访问和更改被引用值
- 将引用传递给函数以更改参数值或提高效率
- 从函数返回引用以提高效率或更改值

### USING REFERENCES

*引用* 为变量提供了另一个名称。你对引用所做的任何操作都对它所引用的变量执行。你可以将引用视为变量的昵称——变量的另一个名称。在本章的第一个程序中，我将向你展示如何创建引用。然后，在接下来的几个程序中，我将向你展示为什么你会想要使用引用以及它们如何改进你的游戏程序。

#### Introducing the Referencing Program

引用程序演示了引用。该程序声明并初始化一个变量来保存分数，然后创建一个引用该变量的引用。程序使用变量和引用显示分数，以表明它们访问的是同一个值。接下来，程序显示该单一值可以通过变量或引用进行更改。图 6.1 说明了该程序。

![](img/34f09be0ed6217c465debc4490197d4f_210_0.png)

**Figure 6.1** 变量 myScore 和引用 mikesScore 都是对单个分数值的名称。

你可以从 Course Technology 网站 (www.courseptr.com/downloads) 下载此程序的代码。该程序位于第 6 章文件夹中；文件名是 referencing.cpp。

```
// Referencing
// Demonstrates using references

#include <iostream>

using namespace std;

int main()
{
    int myScore = 1000;
    int& mikesScore = myScore;  //create a reference

    cout << "myScore is: " << myScore << "\n";
    cout << "mikesScore is: " << mikesScore << "\n\n";

    cout << "Adding 500 to myScore\n";
    myScore += 500;
    cout << "myScore is: " << myScore << "\n";
    cout << "mikesScore is: " << mikesScore << "\n\n";

    cout << "Adding 500 to mikesScore\n";
    mikesScore += 500;
    cout << "myScore is: " << myScore << "\n";
    cout << "mikesScore is: " << mikesScore << "\n\n";

    return 0;
}
```

#### Creating References

我在 `main()` 中做的第一件事是创建一个变量来保存我的分数。

```
int myScore = 1000;
```

然后我创建一个引用 myScore 的引用。

```
int& mikesScore = myScore;  //create a reference
```

前一行声明并初始化 `mikesScore`，这是一个引用 `myScore` 的引用。`mikesScore` 是 `myScore` 的别名。`mikesScore` 不保存自己的 `int` 值；它只是获取 `myScore` 所保存的 `int` 值的另一种方式。

要声明并初始化一个引用，请从引用将引用的值的类型开始，后跟引用运算符 (&)，后跟引用名称，后跟 =，后跟引用将引用的变量。

#### Trick

> 有时程序员会在引用名称前加上字母“r”，以提醒他们正在处理引用。程序员可能会包含以下行：

```
int playerScore = 1000;
int& rScore = playerScore;
```

理解引用的一种方法是将其视为昵称。例如，假设你有一个朋友叫 Eugene，他（可以理解地）要求用昵称称呼他——Gibby（改进不大，但这是 Eugene 想要的）。因此，当你和朋友在派对上时，你可以使用 Eugene 或 Gibby 中的任何一个来叫他过来。你的朋友只有一个，但你可以用他的名字或对他的昵称来称呼他。这与变量及其引用变量的工作方式相同。你可以通过其变量名或对该变量的引用的名称来访问存储在变量中的单个值。最后，无论你做什么，请尽量不要给你的变量命名为 Eugene——为了他们的缘故。

#### Trap

> 因为引用必须始终引用另一个值，所以你在声明它时必须初始化引用。如果不这样做，你会得到编译错误。以下行是完全非法的：

```
int& mikesScore; //don't try this at home!
```

#### Accessing Referenced Values

接下来我将 myScore 和 mikesScore 发送到 cout。

```
cout << "myScore is: " << myScore << "\n";
cout << "mikesScore is: " << mikesScore << "\n\n";
```

这两行代码都显示 1000，因为它们各自访问存储数字 1000 的同一块内存。记住，只有一个值，它存储在变量 myScore 中。mikesScore 只是获取该值的另一种方式。

#### Altering Referenced Values

接下来我将 myScore 的值增加 500。

```
myScore += 500;
```

当我将 myScore 发送到 cout 时，显示 1500，就像你期望的那样。当我将 mikesScore 发送到 cout 时，也显示 1500。同样，这是因为 mikesScore 只是变量 myScore 的另一个名称。从本质上讲，我两次都向 cout 发送同一个变量。

接下来我将 mikesScore 增加 500。

```
mikesScore += 500;
```

因为 mikesScore 只是 myScore 的另一个名称，所以前一行代码将 myScore 的值增加了 500。因此，当我接下来将 myScore 发送到 cout 时，显示 2000。当我将 mikesScore 发送到 cout 时，再次显示 2000。

