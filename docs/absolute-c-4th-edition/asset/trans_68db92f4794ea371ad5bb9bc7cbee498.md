

5. 假设你想更改在第 11.1 和 11.2 节中给出的类 DigitalTime 的实现。具体来说，你想更改记录时间的方式。不是使用两个私有变量 hour 和 minute，你想使用一个单一的（私有）int 变量，将其命名为 minutes。在这个新的实现中，私有变量 minutes 将把时间记录为自 0:00 时间（即自午夜）以来的分钟数。例如，1:30 记录为 90 分钟，因为它是午夜后的 90 分钟。描述你需要如何更改第 11.1 和 11.2 节中显示的接口和实现文件。你不必完整写出文件；只需以非常概括的方式指出你需要更改哪些项目以及如何更改它们。

## 11.2 命名空间

> 人名有什么意义？我们称之为玫瑰
> 换个名字也会一样芬芳。
> 
> 威廉·莎士比亚，《罗密欧与朱丽叶》

当一个程序使用由不同程序员编写的不同类和函数时，就有可能两个程序员会为两个不同的事物使用相同的名称。命名空间是处理此问题的一种方法。命名空间是一组名称定义，例如类定义和变量声明。可以说命名空间可以被打开和关闭，这样当其某些名称否则会与另一个命名空间中的名称冲突时，它可以被关闭。

## 命名空间和 using 指令

我们已经在使用名为 std 的命名空间。std 命名空间包含许多标准 C++ 库文件（例如 iostream）中定义的所有名称。例如，当你在文件开头放置以下行时，

```
#include <iostream>
```

它会将所有名称定义（如 cin 和 cout）放入 std 命名空间。你的程序除非指定它正在使用 std 命名空间，否则不知道 std 命名空间中的名称。要使 std 命名空间中的所有定义对你的代码可用，插入以下 using 指令：

```
using namespace std;
```

了解为什么你可能想要包含此 using 指令的一个好方法是思考为什么你可能不想要包含它。如果你不为命名空间 std 包含此 using 指令，那么你可以将 cin 和 cout 定义为具有除其标准含义之外的其他含义。（也许你想重新定义 cin 和 cout，因为你希望它们的行为与标准版本略有不同。）它们的标准含义在 std 命名空间中；如果没有 using 指令（或类似的东西），你的代码对 std 命名空间一无所知，因此就你的代码而言，它所知道的 cin 和 cout 的唯一定义就是你给它们的定义。

你编写的每一块代码都在某个命名空间中。如果你没有将代码放在某个特定命名空间中，那么代码就在一个被称为全局命名空间的命名空间中。到目前为止，我们没有将我们编写的任何代码放在任何命名空间中，因此我们所有的代码都在全局命名空间中。全局命名空间没有 using 指令，因为你始终在使用全局命名空间。你可以说总有一个隐式的自动 using 指令表示你正在使用全局命名空间。

请注意，你可以在同一个程序中使用多个命名空间。例如，我们始终在使用全局命名空间，我们通常也在使用 std 命名空间。如果一个名称在两个命名空间中都被定义，并且你同时使用这两个命名空间，会怎样？这会导致错误（根据具体细节，可能是编译器错误或运行时错误）。你可以在两个不同的命名空间中定义相同的名称，但如果是这样，那么你一次只能使用其中一个命名空间。然而，这并不意味着你不能在同一个程序中使用这两个命名空间。你可以在同一个程序中在不同时间使用它们。

例如，假设 NS1 和 NS2 是两个命名空间，并且假设 myFunction 是一个在两个命名空间中都定义但在两个命名空间中定义方式不同的无参数 void 函数。以下内容就是合法的：

```
{
    using namespace NS1;
    myFunction();
}
{
    using namespace NS2;
    myFunction();
}
```

第一次调用将使用命名空间 NS1 中给出的 myFunction 的定义，而第二次调用将使用命名空间 NS2 中给出的 myFunction 的定义。

回想一下，块是一组用大括号 {} 括起来的语句、声明以及可能的其它代码。块开头的 using 指令仅适用于该块。因此上面的第一个 using 指令仅适用于第一个块，第二个 using 指令仅适用于第二个块。通常的说法是 NS1 using 指令的作用域是第一个块，而 NS2 using 指令的作用域是第二个块。请注意，由于此作用域规则，我们能够在同一个程序中使用两个冲突的命名空间（例如在包含我们刚才讨论的两个块的程序中）。

再次查看第 11.5 节的显示，你会看到函数 greeting 的定义也放在命名空间 Space1 中。这是通过以下额外的命名空间分组完成的：

```
namespace Space1
{
    void greeting()
    {
        cout << "Hello from namespace Space1.\n";
    }
}
```

## 显示 11.5 命名空间演示（第 1 部分，共 2 部分）

```
1
2 #include <iostream>
3 using namespace std;
4
5 namespace Space1
6 {
7     void greeting();
8 }
9
10 namespace Space2
11 {
12     void greeting();
13 }
14
15 void bigGreeting();
16
17 int main()
18 {
19     {
20         using namespace Space2;
21         greeting();
22     }
23     {
24         using namespace Space1;
25         greeting();
26     }
27     bigGreeting();
28     return 0;
29 }
```

此块中的名称使用命名空间 Space2、std 和全局命名空间中的定义。

此块中的名称使用命名空间 Space1、std 和全局命名空间中的定义。

此处的名称仅使用命名空间 std 和全局命名空间中的定义。

## 显示 11.5 命名空间演示（第 2 部分，共 2 部分）

```
namespace Space1
{
    void greeting()
    {
        cout << "Hello from namespace Space1.\n";
    }
}
```

```
namespace Space2
{
    void greeting()
    {
        cout << "Greetings from namespace Space2.\n";
    }
}

void bigGreeting()
{
    cout << "A Big Global Hello!\n";
}
```

## 示例对话

> Greetings from namespace Space2.
> Hello from namespace Space1.
> A Big Global Hello!

请注意，对于单个命名空间，你可以有任意数量的这些命名空间分组。在显示 11.5 中，我们对命名空间 Space1 使用了两个命名空间分组，对命名空间 Space2 使用了另外两个分组。

在命名空间中定义的每个名称都在命名空间分组内部可用，但名称也可以使代码在命名空间分组之外可用。例如，命名空间 Space1 中的函数声明和函数定义可以通过 using 指令

```
using namespace Space1
```

使之可用，如显示 11.5 所示。

## 2024年6月全国大学英语四级考试真题（第1套）

Part I Writing (30 minutes)

Directions: Suppose your university is seeking students to volunteer for the upcoming international conference on AI and education. You are to write an essay to express your willingness to participate and describe what you can do for the conference. You will have 30 minutes for this task. You should write at least 120 words but no more than 180 words.

Part II Listening Comprehension (25 minutes)

Section A

Directions: In this section, you will hear three news reports. At the end of each news report, you will hear two or three questions. Both the news report and the questions will be spoken only once. After you hear a question, you must choose the best answer from the four choices marked A), B), C) and D). Then mark the corresponding letter on Answer Sheet 1 with a single line through the centre.

Questions 1 and 2 are based on the following news report.

1. A) A fire broke out in a downtown building.  B) A severe storm hit a coastal town.  C) A major traffic accident occurred on a highway.  D) A chemical plant exploded in an industrial area.

2. A) It caused widespread power outages.  B) It resulted in several injuries.  C) It led to the evacuation of residents.  D) It damaged many local businesses.

Questions 3 and 4 are based on the following news report.

3. A) A new species of fish was discovered.  B) A rare bird was spotted in the wild.  C) An ancient artifact was found underwater.  D) A new volcano was detected on the ocean floor.

4. A) It is the largest ever recorded.  B) It is over 1,000 years old.  C) It is made of gold and silver.  D) It is believed to be from a sunken ship.

