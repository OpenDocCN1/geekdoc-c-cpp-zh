
## 短路求值

考虑下面的代码片段：

```cpp
int x = 2;
if (x < 0 && (x*x + 632*x == 1268))
{
    std::cout << "Congrats: " << x << " is the correct solution!" << std::endl;
}
```

快速判断一下，x = 2 是正确解吗？当然不是，2 并不小于 0！甚至 2*2 + 632*2 是否等于 1268 都无关紧要（实际上它确实等于……）。因为 AND 运算符的第一个操作数已经是 false，最终结果也会是 false。毕竟，false && true 仍然是 false；AND 运算符求值为 true 的唯一情况是 true && true。

同样，在下面的代码片段中，应该立刻就能看出 x = 2 是正确解：

```cpp
int x = 2;
if (x == 2 || (x*x + 632*x == 1268))
{
    std::cout << "Congrats: " << x << " is the correct solution!" << std::endl;
}
```

为什么？因为第一个操作数为 true，你立刻就知道整个 OR 表达式也会求值为 true。甚至不需要计算第二个操作数。

自然，C++ 编译器也知道这一点。因此，如果二元逻辑表达式的第一个操作数已经决定了结果，编译器就会确保不会浪费时间计算第二个操作数。逻辑运算符 && 和 || 的这种特性称为短路求值。另一方面，按位运算符 & 和 | 不会短路。对于这些运算符，两个操作数始终都会被求值。

C++ 程序员经常利用逻辑运算符的这种短路语义：

-   如果你需要测试由逻辑运算符连接起来的多个条件，那么应该把计算成本最低的条件放在最前面。本节中的两个例子已经在一定程度上说明了这一点，但当然，只有当其中一个操作数的计算确实很昂贵时，这种技巧才真正划算。
-   短路更常用于防止对右侧操作数求值，否则该求值可能会失败——例如导致致命崩溃。做法是把其他条件放在前面，以便在其余操作数会失败时发生短路。正如我们将在本书后面看到的，这种技术的一个常见应用是在解引用指针之前检查它是否为空。

我们将在后续章节中看到更多依赖短路求值的逻辑表达式示例。目前只需记住：&& 的第二个操作数仅在第一个操作数求值为 true 后才会求值，而 || 的第二个操作数仅在第一个操作数求值为 false 后才会求值。对于 & 和 |，两个操作数始终都会被求值。

另外，哦对了，如果你想知道的话，前面那个方程的正确解是 x = -634。

## 逻辑异或

逻辑运算符中没有与按位异或运算符 ^（XOR，Exclusive OR 的缩写）对应的运算符。毫无疑问，部分原因是：对这个运算符进行短路没有意义（必须始终计算两个操作数才能知道该运算符的正确结果；也许可以花点时间想想这一点）。幸运的是，XOR 运算符像任何按位运算符一样，也可以直接应用于布尔操作数。例如，下面的测试对大多数年轻人和百万富翁会通过。不过，银行余额正常的成年人不会通过，青少年百万富翁也不会通过：

```cpp
if ((age < 20) ^ (balance >= 1'000'000))
{
    ...
}
```

换句话说，这个测试等价于以下逻辑运算符组合中的任意一种：

```cpp
if ((age < 20 || balance >= 1'000'000) && !(age < 20 && balance >= 1'000'000))
{
    ...
}
```

```cpp
if ((age < 20 && balance < 1'000'000) || (age >= 20 && balance >= 1'000'000))
{
    ...
}
```

说服自己这三个 if 语句确实等价，是一个不错的布尔代数小练习。

## 条件运算符

*条件运算符*有时被称为*三元运算符*，因为它涉及三个操作数——也是唯一拥有三个操作数的运算符。它类似于 if-else 语句：不是根据条件选择执行两个语句块之一，而是选择两个表达式之一的值。因此，条件运算符使你能够在两个值之间进行选择。让我们考虑一个例子。

假设你有两个变量 a 和 b，并且你想把两者中较大的值赋给第三个变量 c。下面的语句可以做到这一点：

```cpp
c = a > b ? a : b;    // Set c to the higher of a and b
```

条件运算符的第一个操作数是一个逻辑表达式，在本例中是 a > b。如果这个表达式为 true，则选择第二个操作数——在本例中是 a——作为该运算的结果值。如果第一个操作数为 false，则选择第三个操作数——在本例中是 b——作为值。因此，条件表达式的结果在 a 大于 b 时为 a，否则为 b。这个值被存入 c。该赋值语句等价于下面的 if 语句：

```cpp
if (a > b)
{
    c = a;
}
```

每组 case 语句之后出现的 break 语句对这里的逻辑至关重要。执行 break 语句会跳出 switch，使执行继续到右花括号之后的语句。如果省略某个 case 的 break 语句，则后续 case 的语句也会执行。注意，最后一个 case（通常是 default case）之后不需要 break，因为此时执行无论如何都会离开 switch。不过，包含它仍然是一种良好的编程风格，因为它可以防止意外落入你以后可能添加到 switch 中的另一个 case。switch、case、default 和 break 都是关键字。

这个例子演示了 switch 语句：

```cpp
// Ex4_08.cpp
// Using the switch statement
import <iostream>;

int main()
{
    std::cout << "Your electronic recipe book is at your service.\n"
              << "You can choose from the following delicious dishes:\n"
              << "1. Boiled eggs\n"
              << "2. Fried eggs\n"
              << "3. Scrambled eggs\n"
              << "4. Coddled eggs\n\n"
              << "Enter your selection number: ";

    int choice {};  // Stores selection value
    std::cin >> choice;

    switch (choice)
    {
    case 1:
        std::cout << "Boil some eggs." << std::endl;
        break;
    case 2:
        std::cout << "Fry some eggs." << std::endl;
        break;
    case 3:
        std::cout << "Scramble some eggs." << std::endl;
        break;
    case 4:
        std::cout << "Coddle some eggs." << std::endl;
        break;
    default:
        std::cout << "You entered a wrong number - try raw eggs." << std::endl;
    }
}
```

在输出语句中定义选项并将选择编号读入变量 choice 后，switch 语句开始执行，其选择表达式就写在关键字 switch 后紧跟的圆括号中，即 choice。switch 中的可能选择位于花括号之间，每个选择都由一个 case 标签标识。如果 choice 的值与任一 case 值对应，则执行该 case 标签之后的语句。

如果 choice 的值不与任何 case 值对应，则执行 default 标签之后的语句。如果你在这里没有包含 default case，并且 choice 的值不同于所有 case 值，那么 switch 将什么都不做，程序将继续执行 switch 之后的下一语句——实际上就是执行 `return 0;`，因为已经到达 `main()` 的末尾。

在这个例子中，每个 case 只有一条语句加一条 break 语句，但一般来说，一个 case 标签之后可以有任意多条需要的语句，而且通常不需要把它们括在花括号中。确实需要添加花括号的情况将在后面的某一节中讨论。

正如我们之前所说，每个 case 值都必须是编译期常量，并且必须唯一。不能有两个 case 值相同的原因是，如果它们相同，编译器就无法知道当那个特定值出现时应该执行哪些语句。然而，不同的 case 值不需要有各自唯一的操作。多个 case 值可以共享同一个操作，如下例所示：

```cpp
// Ex4_09.cpp
// Multiple case actions
import <iostream>;
#include <cctype>

int main()
{
    char letter {};
    std::cout << "Enter a letter: ";
    std::cin >> letter;

    if (std::isalpha(letter))
    {
        switch (std::tolower(letter))
        {
        case 'a': case 'e': case 'i': case 'o': case 'u':
            std::cout << "You entered a vowel." << std::endl;
            break;
        default:
            std::cout << "You entered a consonant." << std::endl;
            break;
        }
    }
    else
    {
        std::cout << "You did not enter a letter." << std::endl;
    }
}
```

以下是一些输出示例：

```text
Enter a letter: E
You entered a vowel.
```

if 条件首先使用标准库中的 `std::isalpha()` 分类函数检查你输入的确实是字母，而不是其他字符。如果参数是字母，返回的整数将非零，并会被隐式转换为 true，从而使 switch 执行。switch 条件使用标准库字符将值转换为小写
