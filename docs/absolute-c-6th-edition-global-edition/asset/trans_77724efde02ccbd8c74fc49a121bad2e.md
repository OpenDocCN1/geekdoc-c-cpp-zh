
namespaces? 这会导致错误（根据具体细节不同，可能是编译期错误或运行期错误）。你可以在两个不同的命名空间中定义相同的名称，但如果确实如此，那么你一次只能使用其中一个命名空间。然而，这并不意味着你不能在同一个程序中使用这两个命名空间。你可以在同一个程序中在不同的时间分别使用它们。

例如，假设 NS1 和 NS2 是两个命名空间，并且假设 myFunction 是一个在两个命名空间中都定义了的无参数 void 函数，但在两个命名空间中的定义方式不同。下面的代码就是合法的：

```
{
    using namespace NS1;
    myFunction( );
}
{
    using namespace NS2;
    myFunction( );
}
```

第一次调用将使用命名空间 NS1 中给出的 myFunction 的定义，而第二次调用将使用命名空间 NS2 中给出的 myFunction 的定义。

回想一下，块是一个用大括号 { } 括起来的语句、声明以及可能的其它代码的列表。块开始处的 using 指令仅适用于该块。因此，所示的第一个 using 指令仅适用于第一个块，而第二个 using 指令仅适用于第二个块。通常的说法是，NS1 using 指令的作用域是第一个块，而 NS2 using 指令的作用域是第二个块。请注意，由于这个作用域规则，我们能够在同一个程序中使用两个冲突的命名空间（例如在包含我们刚才讨论的两个块的程序中）。

通常，你会在块的开头放置 using 指令。然而，如果你将其放置在块的更下方，你就需要知道其精确的作用域。using 指令的作用域从其出现的位置运行到块的末尾。你可以在多个块中为同一个命名空间使用 using 指令，因此一个命名空间的整个作用域可能覆盖多个不相连的块。当你在块中使用 using 指令时，通常该块就是函数定义的函数体。

如果你将 using 指令放置在文件的开头（正如我们迄今为止通常所做的那样），那么 using 指令适用于整个文件。using 指令通常应放置在文件的开头附近（或块的开头），但精确的作用域规则是：位于所有块之外的 using 指令的作用域从 using 指令出现的位置到文件末尾。

## Scope Rule for using Directives

> The scope of a using directive is the block in which it appears (more precisely, from the location of the using directive to the end of the block). If the using directive is outside all blocks, then it applies to all of the file that follows the using directive.

## Creating a Namespace

要将一些代码放入命名空间中，你只需将其放在以下形式的命名空间分组中：

```
namespace Name_Space_Name
{
    Some_Code
}
```

当你在代码中包含其中一个分组时，就说你在 Name_Space_Name 命名空间中放置了 Some_Code 中定义的名称。这些名称（实际上是这些名称的定义）可以用 using 指令使之可用

```
using namespace Name_Space_Name;
```

例如，下面取自 Display 11.5 的代码将一个函数声明放在命名空间 Space1 中：

```
namespace Space1
{
    void greeting( );
}
```

如果你再次查看 Display 11.5，你会看到函数 greeting 的定义也被放在命名空间 Space1 中。这是通过以下额外的命名空间分组完成的：

```
namespace Space1
{
    void greeting( )
    {
        cout << "Hello from namespace Space1.\n";
    }
}
```

请注意，对于单个命名空间，你可以有任意数量的这些命名空间分组。在 Display 11.5 中，我们对命名空间 Space1 使用了两个命名空间分组，对命名空间 Space2 使用了另外两个分组。

在命名空间分组内部，每个在命名空间中定义的名称都可用，但这些名称也可以使之对命名空间分组之外的代码可用。例如，命名空间 Space1 中的函数声明和函数定义可以用 using 指令使之可用

```
using namespace Space1
```

正如 Display 11.5 所示。

## Display 11.5 Namespace Demonstration (part 1 of 2)

```
1
2 #include <iostream>
3 using namespace std;
4
4 namespace Space1
5 {
6     void greeting( );
7 }
8
8 namespace Space2
9 {
10     void greeting( );
11 }
12
12 void bigGreeting( );
13 int main()
14 {
15     {
16         using namespace Space2;
17         greeting( );
18     }
19
20     {
21         using namespace Space1;
22         greeting( );
23     }
24
25     bigGreeting( );
26
27     return 0;
28 }
29
29 namespace Space1
30 {
31     void greeting()
32     {
33         cout << "Hello from namespace Space1.\n";
34     }
35 }
36
37 namespace Space2
38 {
39     void greeting()
40     {
41         cout << "Greetings from namespace Space2.\n";
42     }
43 }
```

Names in this block use definitions in namespaces Space2, std, and the global namespace.

Names in this block use definitions in namespaces Space1, std, and the global namespace.

Names out here only use definitions in the namespace std and the global namespace.

## Display 11.5 Namespace Demonstration (part 2 of 2)

```
41 void bigGreeting()
42 {
43   cout << "A Big Global Hello!\n";
44 }
```

Sample Dialogue

> Greetings from namespace Space2.
> Hello from namespace Space1.
> A Big Global Hello!

## Putting a Definition in a Namespace

你通过将其放在命名空间分组中来将名称定义放入命名空间，其语法如下：

```
namespace Namespace_Name
{
    Definition_1
    Definition_2
    .
    .
    Definition_Last
}
```

你可以有多个命名空间分组（甚至在多个文件中），并且所有分组中的所有定义都将在同一个命名空间中。

## Self-Test Exercises

6. 考虑 Display 11.5 中显示的程序。我们能否用 greeting 代替 bigGreeting？

7.  在自测练习 6 中，我们看到你不能向全局命名空间添加以下函数的定义：

void greeting();

你能向全局命名空间添加以下函数声明的定义吗？

void greeting(int howMany);

## using Declarations

本小节描述了一种限定单个名称的方法，以便你只能使命名空间中的一个名称对你的程序可用，而不是使命名空间中的所有名称都可用。我们在第 1 章中见过这种技术，因此这是对我们在第 1 章中所说内容的回顾和扩展。

假设你面临以下情况。你有两个命名空间，NS1 和 NS2。你想使用在 NS1 中定义的函数 fun1 以及在命名空间 NS2 中定义的函数 fun2。问题是 NS1 和 NS2 都定义了一个函数 myFunction。（假设本讨论中的所有函数都不带参数，因此重载不适用。）你不能使用

```
using namespace NS1;
using namespace NS2;
```

这可能会为 myFunction 提供冲突的定义。（如果名称 myFunction 从未被使用，编译器将不会检测到问题并允许你的程序编译和运行。）

你需要一种方法来说明你正在使用 NS1 中的 fun1 和 NS2 中的 fun2，而在命名空间 NS1 和 NS2 中不使用其他任何东西。我们已经在使用一种可以处理这种情况的技术。以下就是你的解决方案：

```
using NS1::fun1;
using NS2::fun2;
```

形式为

```
using Name_Space::One_Name;
```

的限定使来自命名空间 Name_Space 的名称 One_Name（的定义）可用，但不会使 Name_Space 中的任何其他名称可用。这称为 using 声明。

请注意，我们在这些 using 声明中使用的作用域解析运算符 :: 与我们在定义成员函数时使用的作用域解析运算符相同。这两种使用作用域解析运算符的方式具有相似性。例如，Display 11.2 中有以下函数定义：

```
void DigitalTime::advance(int hoursAdded, int minutesAdded)
{
    hour = (hour + hoursAdded)%24;
    advance(minutesAdded);
}
```

在这种情况下，:: 的意思是我们正在为类 DigitalTime 定义函数 advance，而不是在任何其他类中名为 advance 的任何其他函数。类似地，

```
using NS1::fun1;
```

意味着我们正在使用在命名空间 NS1 中定义的名为 fun1 的函数，而不是在任何其他命名空间中对 fun1 的任何其他定义。
