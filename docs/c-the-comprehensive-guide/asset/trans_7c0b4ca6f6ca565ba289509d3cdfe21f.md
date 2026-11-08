
## 8.1 语句块

在任何允许编写单条语句的地方，你也可以用花括号 `{...}` 将多条语句组合在一起。你可以看到图 8.1 中的示意流程图。这也称为复合语句。你不需要用分号结束这个块；这样做会创建一个空语句，而你应该避免这种情况（见第 9 章第 9.2 节）。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_204_0.png)

图 8.1 语句块的流程图。

在清单 8.1 中，我已将这些块附加到大多数 `if` 语句和 `for` 循环上。在这里一致地使用 `{...}` 可以为将来的扩展做准备，并提高可读性。在 `if(factor*factor > n)` 和 `if(n%factor==0)` 中，你会看到没有块花括号的 `if`。`for` 也是如此。

```cpp
for(int prime : primes)          // for followed by a single statement
    std::cout << prime << " ";
    std::cout << "\n";           // not part of for anymore
```

**清单 8.2** 这个“for”只引用一条语句。

这个 for 只与两个输出中的第一个相关联。第二行只输出一次。如果你想在循环内做更多事情，那么使用 `{...}`。这样，你就得到一个语句块，对于 `for` 来说它算作一条语句。

```cpp
for(int prime : primes) {        // Beginning of the block
    std::cout << prime;
    std::cout << " ";
}                               // End of the block
std::cout << " ";
```

**清单 8.3** 语句块由 { 和 } 包围。

现在，分开的 `cout` 输出都在循环内执行。

### 8.1.1 独立块与变量作用域

然而，你不必把块绑定到 `for` 或类似结构上；你可以在任何对你来说有意义的地方引入它们，以代替单条语句。下面的清单就是一个例子。

```cpp
if(number > 50) {                 // outer block
    {                              // 1st inner block
        int result = number*number;
        std::cout << "Square: " << result << std::endl;
    }
    {                              // 2nd inner block
        int result = number*number;
        std::cout << "Doubled: " << result << std::endl;
    }
}
```

**清单 8.4** 在允许语句的地方，你也可以创建块。

两个内部块都与 `if` 关联执行，因为它们都位于属于该 `if` 的外部块内。

你可以自由选择是否要以这种方式对语句进行分组。例如，如果你想在两个内部块中引入相同的变量名，这会很有用。在清单 8.4 中，`result` 在两个内部块中都作为新的 `int` 变量引入。变量只在其定义的块内有效。如果不划分成两个块，两个 `result` 定义会相互干扰。

```cpp
if(number > 50) {
    int result = number*number;          // Definition of result
    std::cout << "Square: " << result << std::endl;
    int result = number+number;          // ⚡ Error: result has already been defined
    std::cout << "Doubled: " << result << std::endl;
}
```

**清单 8.5** 不允许在一个块中两次将“result”用作新变量。

当然，你本可以在这里使用已经存在的 result 变量，而不必用 `int result = number+number` 重新声明它。然而，有时会有一些原因让你不想或不能这样做。

你也可以用 `int result2 = ...` 引入一个新变量。但也许你不希望周围有太多你实际上不再需要的变量。通过引入内部块，你清楚地表明了 `result` 从何处到何处需要，等等。后来的读者就不必再考虑这一点了。

```cpp
if(number > 50) {
    int result1 = number*number;        // a result
    std::cout << "Square: " << result1 << std::endl;
    int result2 = number+number;        // another result
    std::cout << "Doubled: " << result2 << std::endl;
    int result3 = number+number+number; // and another result
    // ... many lines of code in between ...
    // and here?
    // ... even more lines of code ...
}
```

**清单 8.6** 变量太多也不好。

在 `// and here?` 处想知道自己是否可以将任何 `resultN` 变量用于自己目的的人，只能困难地弄清楚——并且很可能出于绝望再引入另一个变量。

为每个单独的变量引入一个新块并每次都向左缩进，会使代码碎片化并毫无必要地加长它。这也不利于阅读时的理解。

在引入新的独立块时，请运用常识。

## 8.2 空语句

当你在期望出现语句的地方写一个分号时，那就是空语句。这条语句*什么都不做*。

```cpp
int main() { ;;;                 // 3 empty statements
    int number = 12 ; ;           // 1 empty statement
    if (int q = number*number ;   // 1 empty statement
    if(q>50) {
        q = q - 50;
    } ;                           // 1 empty statement
    std::cout << q << std::endl;
}
```

**清单 8.7** 到处都是空语句。

什么都不做通常完全没有问题。然而，在某些情况下，插入的空语句是危险的。你已从**第4章**中知道，*if* 后面跟着一条语句，该语句应在条件满足时执行。假设你在前面示例中的 `if(q>50)` 之后插入一个空语句：

```cpp
if(q>50) ; {              // empty statement with serious consequences
    q = q - 50;
}
```

那么，在 `q>50` 的情况下，被执行的就是空语句。减法 `q=q-50` 不再是 *if* 的一部分，而是现在*总是*执行。

> **避免空语句**
>
> 尽管空语句大多无害，但当它们确实引发问题时，追踪起来会非常麻烦。养成不要用分号结束语句块 `{...}` 的习惯。
>
> 对 `if`、`for` 和 `while` 结构要特别警惕，以免无意中插入空语句。

## 8.3 声明语句

我们已经多次看到引入了新变量。例如，在**清单 8.1**中，就是这一行：

```cpp
int upTo = 0;
```

这引入了一个新变量——它*声明*了这个变量。首先指定它的类型——这里是 `int`——然后指定变量将使用的名称——这里是 `upTo`。完成了。但是等号 `=` 以及它右边的内容呢？那是*初始化*，在这种声明形式中是可选的。我已经在**第4章第4.2节**中讨论了各种初始化形式。

所以，请注意以下内容。使用

```cpp
int upTo;
```

该变量被*声明*了。你不能按它现在的样子使用它（进行计算等），因为它还没有包含值。更准确地说，它的值是*未定义*的。这意味着，如果你使用该变量进行计算，它包含一个*任意*值——在大多数情况下，这会导致程序中出现不可预见的行为。关于这一点还有更多要说的，因为许多类型也会用这种声明形式*初始化*，但 `int` 不会。请在**第12章**中阅读更多相关内容。

同样重要的是，变量只在你声明它们的块内已知。一旦程序越过该块的右花括号，它们就不再可用。因此，这个声明不会与前一个声明重叠：

```cpp
int upTo = inputUpTo(argc, argv);
```

这声明了一个“不同的” `upTo`，它只在 `main()` 中可见。

你还可以在这里看到，初始化不仅可以用 0 或常量进行。这里，一个复杂的函数调用返回了用于初始化 `upTo` 的值。

你也可以组合用逗号分隔的声明。你可以像这样声明多个变量：

```cpp
int from, to, result;
```

这里，所有变量都将是 `int` 类型。如果你想同时初始化所有（或部分）变量，可以这样做：

```cpp
int from, to = 0, result;
```

这里你声明了三个变量，但只有 `to` 用 0 初始化。

### 8.3.1 结构化绑定

从 C++17 开始，也可以一次声明多个元素，并用单个等号 `=` 将它们全部初始化。为此，请在方括号 `[]` 前使用 `auto`，方括号中则包含要声明的变量。

有三种可能的变体：绑定 C 数组、绑定元组和绑定结构体。

```cpp
// https://godbolt.org/z/xWbqeeq3n
#include <iostream>
#include <tuple>
auto mkTpl() {
    return std::make_tuple(2, 'b', 3.14); // tuple<int,char,double>
}
struct Point {
    int x, y;
};
int main() {
    // Structured binding of a C-array
    int odd[5] = { 1,3,7,9,11 };
    auto [ one, two, three, four, five ] = odd;
    // Structured binding of a tuple
    auto [ zwei, be, pi ] = mkTpl();
```
