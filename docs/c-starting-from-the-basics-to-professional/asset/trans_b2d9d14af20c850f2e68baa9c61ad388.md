
转换例程 `tolower()`，并使用结果来选择 case。转换为小写避免了需要同时为大写和小写字母设置 case 标签。所有标识元音字母的 case 都会执行相同的语句。可以看到，你只需把这些 case 依次写出来，后面跟上其中任一 case 选中时要执行的语句。如果输入不是元音字母，那它一定是辅音字母，默认 case 会处理这种情况。

如果 `isalpha()` 返回 0，这会被转换为 false，则不会执行 switch，因为会选择 else 子句；这会输出一条消息，指出输入的字符不是字母。

在 Ex4_09.cpp 中，我们把所有值为元音字母的 case 标签放在同一行。这并不是必需的。你也可以在 case 标签之间添加一个换行（或任何形式的空白）。下面是一个示例：

```cpp
switch (std::tolower(letter))
{
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        std::cout << "You entered a vowel." << std::endl;
        break;
    ...
}
```

break 语句并不是将控制权移出 switch 语句的唯一方式。如果某个 case 标签后面的代码包含 return 语句，控制权会立即退出 switch 语句，同时也会退出外围函数。因此，原则上你可以把 Ex4_09 中的 switch 语句重写如下：

```cpp
switch (std::tolower(letter))
{
case 'a': case 'e': case 'i': case 'o': case 'u':
    std::cout << "You entered a vowel." << std::endl;
    return 0;                         // Ends the program
}

// We did not exit main() in the above switch, so letter is not a vowel:
std::cout << "You entered a consonant" << std::endl;
```

在这个特定变体中，我们还可以看到默认 case 是可选的。如果你输入元音字母，输出会反映这一点，而 switch 语句中的 return 语句会终止程序。注意，在 return 语句之后绝不应再放 break 语句。如果你输入辅音字母，switch 语句什么也不做。这些 case 都不适用，而且没有默认 case。因此执行会继续执行 switch 语句之后的代码，并输出你实际上输入的是辅音字母——记住，如果你输入的是元音字母，程序早已因为 return 语句而终止了。

这个变体的代码以 Ex4_09A 的形式提供。不过，我们创建它是为了说明几个要点，而不是因为它必然体现了良好的编程风格。与在所有 case 都没有执行 return 后继续执行 switch 语句之后的代码相比，当然更推荐使用默认 case。

**提示** 你经常会使用 switch 语句来根据某个枚举值决定采取哪个操作（参见第 3 章）。对于基于枚举值的 switch，应避免使用默认 case。换句话说：通常应包含与相应枚举类型可能取值数量一样多的 case。这样，如果你以后给枚举类型添加新值，大多数编译器会为每个因此不再穷尽的 switch 语句发出警告。

## 贯穿（Fallthrough）

每组 case 语句末尾的 break 语句会把执行转移到 switch 之后的语句。你可以通过从前面示例 Ex4_08 或 Ex4_09 的 switch 语句中删掉 break 语句并观察会发生什么，来演示 break 语句的本质作用。你会发现，没有 break 语句的 case 后面紧邻的 case 标签下方的代码也会被执行。这种现象称为贯穿（fallthrough），因为从某种意义上说，我们“贯穿”到了下一个 case。

缺失 break 语句往往表明存在疏忽，因此是一个 bug。为了说明这一点，让我们回到前面的一个例子——那个关于彩票号码的例子：

```cpp
switch (ticket_number)
{
  case 147:
    std::cout << "You win first prize!" << std::endl;
  case 387:
    std::cout << "You win second prize!" << std::endl;
    break;
  case 29:
    std::cout << "You win third prize!" << std::endl;
    break;
  default:
    std::cout << "Sorry, you lose." << std::endl;
    break;
}
```

你会注意到，这一次我们“不小心”省略了第一个 case 后面的 break 语句。如果你现在执行这个 switch 语句，且 ticket_number 等于 147，输出将如下：

```
You win first prize!
You win second prize!
```

因为 ticket_number 等于 147，switch 语句会跳到对应的 case，你赢得一等奖。但由于没有 break 语句，执行会直接继续执行下一个 case 标签下方的代码，于是你也赢得二等奖——好耶！显然，这个 break 的遗漏一定是个意外疏忽。事实上，因为贯穿往往表示存在 bug，所以如果非空 switch case 后面没有 break 或 return 语句，许多编译器会发出警告。空 switch case，例如 Ex4_09 中使用的那些（用于检查元音字母），很常见，因此不会触发编译器警告。

不过，贯穿并不总是意味着犯了错误。有时故意编写使用贯穿的 switch 语句会非常有用。假设在我们的彩票中，有多个号码赢得二等奖和三等奖（分别有两个和三个号码），并且其中一个赢得三等奖的号码还会获得特别奖励奖。那么我们可以如下编写这个逻辑：

```
switch (ticket_number)
{
case 147:
    std::cout << "You win first prize!" << std::endl;
    break;
case 387:
case 123:
    std::cout << "You win second prize!" << std::endl;
    break;
case 929:
    std::cout << "You win a special bonus prize!" << std::endl;
case 29:
case 78:
    std::cout << "You win third prize!" << std::endl;
    break;
default:
    std::cout << "Sorry, you lose." << std::endl;
    break;
}
```

其思路是，如果你的 ticket_number 等于 929，结果应为：

```
You win a special bonus prize!
You win third prize!
```

然而，如果你的号码是 29 或 78，你只会赢得三等奖。这些非典型 case（双关语）带来的一点小烦恼是，编译器可能会发出贯穿警告，即使你确知这一次并不是错误。当然，作为一个自重的程序员，你希望编译所有程序时都没有警告。你总是可以重写代码并复制语句来输出你赢得三等奖。但一般来说，重复代码也是你想避免的。那么，该怎么办？

幸运的是，C++17 增加了一项语言特性，可以向编译器和阅读你代码的人表明你是在有意使用贯穿：你可以在原本要添加 break 语句的同一位置添加 `[[fallthrough]]` 语句：

```
switch (ticket_number)
{
...
case 929:
    std::cout << "You win a special bonus prize!" << std::endl;
    [[fallthrough]];
case 29:
case 78:
    std::cout << "You win third prize!" << std::endl;
    break;
...
}
```

对于空 case，例如号码 29 对应的那个，允许使用 `[[fallthrough]]` 语句，但不是必需的。编译器本来就不会为此发出警告。

## 语句块与变量作用域

switch 语句在花括号之间有它自己的块，其中包含 case 语句。if 语句也经常用花括号包围条件为真时要执行的语句，else 部分也可能有这样的花括号。就变量作用域而言，这些语句块与其他任何块没有区别。在块内声明的任何变量都会在块结束时消失，因此你不能在块外引用它。

这里，考虑下面这个相当随意的计算：

```cpp
if (value > 0)
{
  int savit {value - 1};    // This only exists in this block
  value += 10;
}
else
{
  int savit {value + 1};    // This only exists in this block
  value -= 10;
}
std::cout << savit;         // This will not compile! savit does not exist
```

末尾的输出语句会导致编译器错误消息，因为此时 savit 变量未定义。在块内定义的任何变量只能在该块内使用，因此如果你想从块外访问源自块内的数据，就必须在外部块中定义存储该信息的变量。

switch 语句块内的变量定义必须在执行过程中可达，并且不能通过跳到声明之后且在同一作用域内的某个 case 来绕过这些定义；否则代码将无法编译。你很可能还完全不理解我们的意思。不过，通过一个例子来解释会容易得多。下面的代码说明了 switch 中如何出现非法声明：

```cpp
int test {3};
switch (test)
{
  int i {1};          // ILLEGAL - cannot be reached

  case 1:
    int j {2};        // ILLEGAL - can be reached but can be bypassed
    std::cout << test + j << std::endl;
    break;

  int k {3};          // ILLEGAL - cannot be reached

  case 3:
  {
    int m {4};        // OK - can be reached and cannot be bypassed
    std::cout << test + m << std::endl;
    break;
  }
}
```
