
运行此应用程序时，你会看到以下输出：

```
10.5
10.5
```

在这段代码中，你使用了一个名为 `fabs()` 的函数或机器（通常读作“ef-abs”，表示浮点绝对值）。此函数以数字作为输入，并返回该数字的绝对值作为输出。

![](img/128ab511de4e7360e167e3b15cdd5dd0_162_0.png)

一个数的绝对值就是该数的正值形式。例如，-5 的绝对值就是 5。12 的绝对值仍是 12。绝对值几乎总是正数，因为 0 的绝对值是 0，但 0 是原点，既不是正数也不是负数（详情见 http://www.math.com/school/subject1/lessons/S1U1L10DP.html）。名称 abs 前面的 f 是因为它使用浮点数，而浮点数就是带小数点的数。

因此，`main()` 中的第一行针对值 -10.5 调用 `fabs()`。然后 cout 获取此函数的输出（即结果），并将其打印到控制台。

接着，第二行再次执行相同的操作，只是它取数字 10.5 的绝对值。

那么这个函数的处理程序在哪里？它不在你的代码中；它在另一个文件里，而下面这一行确保你的应用程序可以使用此函数：

```
#include <math.h>
```

你在许多地方见过函数。如果你使用计算器，输入一个数字并按平方根按钮，计算器就会运行一个计算平方根的函数。

但函数可以比仅处理数字更复杂。仔细考虑这句话：当你使用文字处理器，高亮一个单词并检查该单词的拼写时，应用程序会调用一个处理拼写检查的函数。此函数执行类似以下操作：

```
This is a function to check the spelling of a single word.
Inputs: A single word.
Look up the word
If the word is not found
    Find some suggestions.
    Open a dialog box through which you (the user)
        can change the word by either typing a new word
or picking one of the selections, or just leaving
it the same.
If you made a change,
    Return the new spelling.
Otherwise
    Return nothing.
Otherwise
    Return nothing
```

## 用函数分工

注意 `if` 语句是如何通过缩进分组。最后的 `otherwise` 与第一个 `if` 语句配对，因为它的缩进与 `if` 语句的缩进相匹配。

所以那是一个执行拼写检查的函数。但请考虑这一点：当你不高亮任何单词而运行拼写检查器时，拼写检查器会针对整个文档运行。那是另一个函数。如下所示。

```
This function checks the spelling of the entire document
For each word in the document
    Check the spelling of the single word
```

计算机如何执行 `for` 循环中的步骤“检查单个单词的拼写？”它会调用前面描述的函数。此过程称为*代码复用*。如果整个函数已经在别处存在，你完全没有理由再重写一遍。这就是函数的妙处。

### 调用函数

当你运行函数中的代码时，计算机人士会说你在*调用*该函数。就像每个好人一样，好的函数也有名字。调用函数时，你通过名字来调用。

![](img/128ab511de4e7360e167e3b15cdd5dd0_163_0.png)

通常，在编写应用程序和开发调用函数的代码时，开发者会说他们在调用函数。这在一定程度上是计算机行话，也在一定程度上是一种奇怪的毛病，即开发者开始对计算机产生了一点过多的共鸣。

要调用函数，你需要键入它的名称，然后键入一对圆括号。在圆括号内，列出你想发送到函数输入中的项。这里使用的术语是*传递*，就像“你把值传递给函数”。

### 对函数使用 auto

一般来说，明确指定用于接收函数输出的变量类型会使代码更易读。然而，有些情况下你可能不知道精确的输出类型，或者函数的不同版本会输出不同的类型（这非常令人困惑）。在这种情况下，你首先按照第 1 册第 5 章“使用范围”一节所述，将 GCC 设置为使用 C++17。然后，你可以编写清单 6-2 中所示的 Fabs2 示例，如下面的 UsingAuto 示例所示：

```cpp
#include <iostream>
#include <math.h>

using namespace std;

int main()
{
    auto mynumber = fabs(-23.87);
    cout << mynumber << endl;
    return 0;
}
```

结果与 Fabs2 示例相同。区别在于，mynumber 现在的类型是 auto，C++ 会自动为你检测数据类型，而不是 double，后者需要你显式定义数据类型。

### 传递变量

你还可以将变量的值传递给函数。清单 6-3 中的 Fabs3 示例创建两个变量：一个传递给函数，另一个接收函数的结果。

- **清单 6-3：** 使用 fabs() 的另一种方式

```cpp
#include <iostream>
#include <math.h>

using namespace std;

int main()
{
    double start = -253.895;
    double finish = fabs(start);
    cout << finish << endl;
    return 0;
}
```

这段代码创建两个变量；第一个名为 `start`，第二个名为 `finish`。它将 `start` 初始化为值 -253.895。接下来，它调用 `fabs()`，并将 `start` 的值传递给它。它将返回值保存到 `finish`，并打印 `finish` 中的值。当 `fabs()` 运行时，你会看到控制台上出现以下内容：

```text
253.895
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_166_0.png)

如果你需要多次使用函数结果，将函数结果保存到变量中会很有用。例如，如果你出于某种原因需要 −253.895 的绝对值，然后几行之后又需要它，你有一个选择：你可以每次调用 `fabs(-253.895)`，也可以只调用一次，将结果保存到变量中，然后在每次需要时使用该变量。将其保存到变量中的好处是，你之后可能会说，例如：“哦，等等！我想要的不是绝对值！我想要绝对值的负值！”那么你只需修改一行代码——即调用 `fabs()` 的那一行。相反，如果你已经多次调用 `fabs()`，那么每次调用时都必须修改它。顺便说一句，如果你好奇如何取绝对值的负值并将其存储到变量中，只需在它前面加一个负号，如下所示：

```cpp
finish = -fabs(start);
```

### 传递多个变量

有些函数喜欢接收各种各样的好东西，例如多个参数。与接收单个值的函数一样，你把值放在一对圆括号内。由于有多个值，你用逗号分隔它们。清单 6-4 中所示的 `pow()` 示例使用一个名为 `pow()` 的函数计算 10 的三次幂。（也就是说，它计算 10 乘以 10 乘以 10。是的，就是 `pow()`。）请确保在 `#include` 部分包含 math.h 行，以便可以使用 `pow()` 函数。

### 定义 AddOne() 函数

清单 6-5 中所示的 AddOne 示例既提供了一个自定义函数，也提供了 main() 中调用该自定义函数的代码。（该函数放在 main() 外部——事实上，放在它前面。）

- **清单 6-5：** 编写你自己的函数

```cpp
#include <iostream>

using namespace std;

int AddOne(int start)
{
    int newnumber = start + 1;
    return newnumber;
}

int main()
{
    int testnumber = 20;
    int result = AddOne(testnumber);
    cout << result << endl;
    return 0;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_168_0.png)

注意，此示例缺少前面示例中出现的 `#include <math.h>` 条目。只有当你使用某个包含文件的特性时，才需要向代码的 include 部分添加条目。在此情况下，该示例依赖的是基本 C++ 语言组成部分的标准数学特性，因此不需要任何额外代码。

使用可下载的源代码会节省时间，并确保示例在你第一次尝试时就能运行。不过，你也可以选择手动键入它。由于代码量不少，你一开始可能会遇到一些编译器错误；仔细查看出错的代码行，找出你的代码与本书中此处代码之间的差异。运行该示例后，你会看到：

```
21
```
