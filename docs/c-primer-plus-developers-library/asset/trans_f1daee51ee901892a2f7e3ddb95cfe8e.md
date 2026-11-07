
假设你想添加第二个用户定义函数。就像使用库函数一样，你可以通过函数名调用用户定义函数。并且，就像使用库函数一样，你必须在使用该函数之前提供函数原型，通常的做法是将原型放在 `main()` 定义的上方。但现在，必须由你（而不是库供应商）提供新函数的源代码。最简单的方法是将代码放在同一文件中 `main()` 代码的后面。程序清单2.5说明了这些要素。

### 程序清单 2.5 `ourfunc.cpp`

```cpp
// ourfunc.cpp -- defining your own function
#include <iostream>
void simon(int);   // function prototype for simon()

int main()
{
    using namespace std;
    simon(3);       // call the simon() function
    cout << "Pick an integer: ";
    int count;
    cin >> count;
    simon(count);   // call it again
    cout << "Done!" << endl;
    return 0;
}

void simon(int n)  // define the simon() function
{
    using namespace std;
    cout << "Simon says touch your toes " << n << " times." << endl;
}                 // void functions don't need return statements
```

`main()` 函数调用 `simon()` 函数两次，一次以 3 为实参，一次以变量 count 为实参。在这两次调用之间，用户输入一个整数，用于设置 count 的值。该示例在 `cout` 提示消息中没有使用换行符。这使得用户输入与提示出现在同一行。下面是程序清单2.5中程序的一个示例运行：

```text
Simon says touch your toes 3 times.
Pick an integer: 512
Simon says touch your toes 512 times.
Done!
```

## 函数形式

程序清单2.5中 `simon()` 函数的定义遵循与 `main()` 定义相同的一般形式。首先是一个函数头。然后，用花括号括起来的是函数体。你可以将函数定义的形式概括如下：

```text
type functionname(argumentlist)
{
    statements
}
```

注意，定义 `simon()` 的源代码位于 `main()` 的右花括号之后。与 C 一样，也与 Pascal 不同，C++ 不允许将一个函数定义嵌入另一个函数定义中。每个函数定义都独立于所有其他函数定义；所有函数都是平等的（见图2.8）。

![](img/9afc44517b591d64e2e19f623c9308ef_69_0.png)

图2.8 函数定义在文件中按顺序出现。

## 函数头

程序清单2.5中的 `simon()` 函数具有如下函数头：

```cpp
void simon(int n)
```

开头的 `void` 表示 `simon()` 没有返回值。因此，调用 `simon()` 不会产生一个可以在 `main()` 中赋给变量的数。于是，第一次函数调用看起来像这样：

```cpp
simon(3);          // ok for void functions
```

由于可怜的 `simon()` 缺少返回值，你不能这样使用它：

```cpp
simple = simon(3);   // not allowed for void functions
```

括号中的 `int n` 表示你应当使用 `simon()` 时传入一个 `int` 类型的实参。`n` 是一个新变量，它被赋予函数调用期间传递的值。因此，下面的函数调用将值 3 赋给 `simon()` 函数头中定义的 n 变量：

```cpp
simon(3);
```

当函数体中的 `cout` 语句使用 n 时，它使用的是函数调用中传入的值。这就是为什么 `simon(3)` 在其输出中显示 3。示例运行中对 `simon(count)` 的调用使该函数显示 512，因为那是为 count 输入的值。简而言之，`simon()` 的函数头告诉你，该函数接受一个 int 类型的实参，并且没有返回值。

让我们回顾一下 `main()` 的函数头：

```cpp
int main()
```

开头的 int 表示 `main()` 返回一个整数值。空括号（其中可以选择包含 `void`）表示 `main()` 没有实参。有返回值的函数应使用关键字 return 提供返回值并终止函数。这就是为什么你一直使用下面的语句作为 `main()` 的结尾：

```cpp
return 0;
```

这在逻辑上是一致的：`main()` 应当返回一个 int 类型的值，而你让它返回整数 0。但是，你可能会想，你是在把值返回给什么？毕竟，在你的任何程序中，都没有看到任何东西调用 `main()`：

```cpp
squeeze = main();    // absent from our programs
```

答案是，你可以把计算机的操作系统（比如 Unix 或 Windows）看作在调用你的程序。因此，`main()` 的返回值不是返回给程序的其他部分，而是返回给操作系统。许多操作系统都可以使用程序的返回值。例如，Unix shell 脚本和 Windows 命令行界面批处理文件可以设计为运行程序并测试其返回值，这些返回值通常称为*退出值*。通常的约定是，退出值为零表示程序成功运行，而非零值表示出现了问题。因此，你可以设计一个 C++ 程序，在比如无法打开文件时返回非零值。然后，你可以设计一个 shell 脚本或批处理文件来运行该程序，并在程序发出失败信号时采取某些替代操作。

## 关键字

关键字是计算机语言的词汇。本章使用了四个 C++ 关键字：`int`、`void`、`return` 和 `double`。由于这些关键字对 C++ 来说很特殊，你不能将它们用于其他目的。也就是说，你不能把 `return` 用作变量名，也不能把 `double` 用作函数名。但你可以将它们用作名称的一部分，例如 `painter`（其中隐藏着 int）或 `return_aces`。附录B“C++保留字”提供了 C++ 关键字的完整列表。顺便提一下，`main` 不是关键字，因为它不是语言的一部分。相反，它是必需函数的名称。你可以将 `main` 用作变量名。（在过于深奥、这里无法描述的情况下，这可能会引发问题，而且无论如何都会令人困惑，所以你最好不要这样做。）同样，其他函数名和对象名也不是关键字。然而，在程序中将同一个名称（比如 `cout`）同时用于一个对象和一个变量会让编译器混淆。也就是说，你可以在一个不使用 `cout` 对象进行输出的函数中将 `cout` 用作变量名，但不能在同一个函数中以两种方式使用 `cout`。

## 使用有返回值的用户定义函数

让我们再进一步，编写一个使用 return 语句的函数。`main()` 函数已经展示了有返回值函数的方案：在函数头中给出返回类型，并在函数体末尾使用 `return`。你可以使用这种形式为前往英国的人解决一个重量级问题。在英国，许多浴室秤以*英石*为单位校准，而不是以美国磅或国际千克为单位。*英石*这个词在此语境中单复数同形。（英语确实缺乏比如 C++ 那样的内部一致性。）一英石是 14 磅，程序清单2.6使用一个函数进行这种转换。

### 程序清单 2.6 `convert.cpp`

```cpp
// convert.cpp -- converts stone to pounds
#include <iostream>
int stonetolb(int);      // function prototype
int main()
{
    using namespace std;
    int stone;
    cout << "Enter the weight in stone: ";
    cin >> stone;
    int pounds = stonetolb(stone);
    cout << stone << " stone = ";
    cout << pounds << " pounds." << endl;
    return 0;
}

int stonetolb(int sts)
{
    return 14 * sts;
}
```

下面是程序清单2.6中程序的一个示例运行：

```text
Enter the weight in stone: 15
15 stone = 210 pounds.
```

在 `main()` 中，程序使用 `cin` 为整数变量 `stone` 提供一个值。这个值作为实参传递给 `stonetolb()` 函数，并在该函数中赋给变量 `sts`。然后，`stonetolb()` 使用 `return` 关键字将 `14 * sts` 的值返回给 `main()`。这说明你并不局限于在 `return` 后面跟一个简单的数字。这里，通过使用更复杂的表达式，你避免了不得不
