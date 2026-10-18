

- 如果要插入的值大于当前节点的值：
  - 然后，如果当前节点的右指针为空，将当前节点的右指针设置为指向新节点。
  - 如果当前节点的右指针不为空，将当前节点的指针设置为右节点的地址并从步骤 2 重复。

在你的基类 BinaryTree 中编写一个名为 printInOrder 的方法，该方法可递归操作，如下：对于每个 Node，你应首先在不为空时跟随左指针，然后打印当前 Node 的值，然后在不为空时跟随右指针。

编写一个驱动程序，构造一个 BinaryTree 和一个 BinarySearchTree 并向两者插入相同的值。然后在两个树上调用 printInOrder 方法。BinarySearchTree 对象应按排序顺序打印输出。

> 这是证明规则的例外。

COMMON MAXIM *(possibly a corruption of something like: It’s the exception that tests the rule.)*

## INTRODUCTION

一种编写程序的方法是首先假设不会发生任何异常或错误。例如，如果程序从列表中取出一个条目，你可能会假设列表不为空。一旦你让程序在一切按计划进行的核心情况下正常工作，你就可以添加代码来处理异常情况。在 C++ 中，有一种方法可以在代码中体现这种方法。基本上，你编写代码时假设不会发生非常异常的事情。之后，你使用 C++ 的异常处理机制为那些异常情况添加代码。异常处理通常用于处理错误情况，但也许更好的看法是将其视为处理“异常情况”的方式。毕竟，如果你的代码正确处理了“错误”，那么它就不再是错误了。

也许异常最重要用途是处理某些特殊情况的处理方式取决于函数的使用方式。也许该函数将在许多程序中使用，其中一些程序会以一种方式处理特殊情况，而另一些程序会以另一种方式处理。例如，如果函数中出现除零，则可能对于函数的某些调用，程序应结束，但对于其他调用则应发生其他事情。你会看到，这种函数可以被定义为在特殊情况发生时抛出异常，而该异常将允许在函数外部处理特殊情况。这样，特殊情况就可以针对函数的不同调用以不同方式处理。

在 C++ 中，异常处理如下进行：要么某些库软件或你的代码提供一种机制来在发生异常时发出信号。这称为*抛出异常*。在程序的另一处，你放置处理异常情况的代码。这称为*捕获异常*。这种编程方法使代码更清晰。当然，我们仍然需要解释在 C++ 中如何做到这一点。

## PREREQUISITES

除一个可跳过的子部分外，第 16.1 节仅使用第 2 章至第 6 章和第 10 章至第 11 章的材料。第 16.1 节中题为“派生类中的异常规范”的 Pitfall 子部分使用了第 15 章的材料。此 Pitfall 子部分可以跳过而不影响连贯性。

除一个可跳过的子部分外，第 16.2 节使用第 2 章至第 8 章和第 10 章至第 12 章以及第 15 章第 15.1 节的材料，再加上第 16.1 节。第 16.2 节中题为“测试可用内存”的子部分使用了第 15 章的材料。此子部分可以跳过而不影响连贯性。

## 16.1 EXCEPTION-HANDLING BASICS

> 好吧，程序在大多数情况下都能工作。我不知道它需要适用于这种情况。

COMPUTER SCIENCE STUDENT, APPEALING A GRADE

异常处理旨在谨慎使用，并且在比简单入门示例中合理包含的情况更为复杂的情况下使用。因此，我们将通过简单的示例来教你 C++ 的异常处理细节，这些示例在正常情况下不会使用异常处理。这对于学习异常处理很有意义，但不要忘记这些第一个示例是玩具示例，实际上，你不会对如此简单的事情使用异常处理。

### A Toy Example of Exception Handling

对于此示例，假设牛奶是我们文化中如此重要的食物，人们几乎从不缺它，但我们仍然希望我们的程序能够适应极不可能的缺奶情况。基本代码，假设我们不会缺奶，可能如下：

```cpp
cout << "Enter number of donuts:\n";
cin >> donuts;
cout << "Enter number of glasses of milk:\n";
cin >> milk;
dpg = donuts/static_cast<double>(milk);
cout << donuts << " donuts.\n"
     << milk << " glasses of milk.\n"
     << "You have " << dpg
     << " donuts for each glass of milk.\n";
```

如果没有牛奶，则此代码将包括除零，这是一个错误。为了处理我们缺奶的特殊情况，我们可以添加对这种异常情况的测试。显示 16.1 中显示了添加了对特殊情况的此测试的完整程序。显示 16.1 中的程序不使用异常处理。现在，让我们看看如何使用 C++ 异常处理设施重写此程序。

**DISPLAY 16.1 Handling a Special Case Without Exception Handling**

```cpp
1   #include <iostream>
2   using namespace std;
3
4   int main()
5   {
6       int donuts, milk;
7       double dpg;
8       cout << "Enter number of donuts:\n";
9       cin >> donuts;
10      cout << "Enter number of glasses of milk:\n";
11      cin >> milk;
12
13      if (milk <= 0)
14      {
15          cout << donuts << " donuts, and No Milk!\n" << "Go buy some milk.\n";
16      }
17      else
18      {
19          dpg = donuts/static_cast<double>(milk);
20          cout << donuts << " donuts.\n" << milk << " glasses of milk.\n" << "You have " << dpg << " donuts for each glass of milk.\n";
21      }
22
23      cout << "End of program.\n";
24      return 0;
25  }
```

**Sample Dialogue**

```text
Enter number of donuts:
12
Enter number of glasses of milk:
0
12 donuts, and No Milk!
Go buy some milk.
End of program.
```

在显示 16.2 中，我们使用异常重写了显示 16.1 中的程序。这只是一个玩具示例，你可能不会在这种情况下使用异常。但是它确实给我们一个简单的示例。尽管整个程序并不更简单，但 try 和 catch 之间的部分更干净，这暗示了使用异常的优势。

**DISPLAY 16.2 Same Thing Using Exception Handling**

```cpp
#include <iostream>
using namespace std;

int main()
{
    int donuts, milk;
    double dpg;

    try
    {
        cout << "Enter number of donuts:\n";
        cin >> donuts;
        cout << "Enter number of glasses of milk:\n";
        cin >> milk;

        if (milk <= 0)
            throw donuts;

        dpg = donuts/static_cast<double>(milk);
        cout << donuts << " donuts.\n"
             << milk << " glasses of milk.\n"
             << "You have " << dpg
             << " donuts for each glass of milk.\n";
    }
    catch(int e)
    {
        cout << e << " donuts, and No Milk!\n"
             << "Go buy some milk.\n";
    }

    cout << "End of program.\n";
    return 0;
}
```

**Sample Dialogue 1**

```text
Enter number of donuts:
12
Enter number of glasses of milk:
6
12 donuts.
6 glasses of milk.
You have 2 donuts for each glass of milk.
```

**Sample Dialogue 2**

```text
Enter number of donuts:
12
Enter number of glasses of milk:
0
12 donuts, and No Milk!
Go buy some milk.
End of program.
```

查看 try 和 catch 之间的代码。该代码基本上与显示 16.1 中的代码相同，但而不是大 if-else 语句（在显示 16.1 中以颜色显示），此新程序具有以下较小的 if 语句（加上一些简单的非分支语句）：

```cpp
if (milk <= 0)
    throw donuts;
```

此 if 语句表示如果没有牛奶，则执行异常操作。异常操作在 catch 之后给出。想法是正常情况由 try 后的代码处理，而 catch 后的代码仅在异常情况下使用。我们因此将正常情况与异常情况分开。在这个玩具示例中，这种分离并没有真正带来太多好处，但在其他情况下它将证明非常有帮助。让我们看一下细节。

在 C++ 中处理异常的基本方式由 try-throw-catch 三元组组成。try 块的语法为

```cpp
try
{
    Some_Code
}
```

此 try 块包含基本算法的代码，告诉计算机在一切顺利时做什么。它被称为 try 块，因为你不能 100% 确定一切都会顺利，但你想“试一试”。

现在如果出了问题，你想抛出异常，这是一种表示出了问题的方式。基本轮廓，在我们添加 throw 时如下：

```cpp
try
{
```

