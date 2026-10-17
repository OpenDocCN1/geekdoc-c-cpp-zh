
| Face | Frequency |
| :--- | :--- |
| 1 | 9999294 |
| 2 | 10002994 |
| 3 | 9995360 |
| 4 | 10000409 |
| 5 | 10005206 |
| 6 | 9996802 |

> 图 5.12 | 掷 60,000,000 次六面骰子。（部分 2。）

如程序输出所示，通过缩放和偏移，我们使用 `rand` 函数真实地模拟了六面骰子的投掷过程。注意使用 `%s` 转换说明符来打印 "Face" 和 "Frequency" 字符串作为列标题（第 49 行）。在我们学习第 6 章的数组后，我们将展示如何用一行语句优雅地替换这 26 行 `switch` 语句。

## 随机化随机数生成器

再次执行图 5.11 的程序会产生：

| 6 | 5 | 5 | 6 |
| 5 | 1 | 1 | 5 | 3 |
| 6 | 6 | 2 | 4 | 2 |
| 6 | 2 | 3 | 4 | 1 |

注意打印的是*完全相同的数值序列*。这些怎么能是随机数呢？讽刺的是，*这种重复性*是函数 `rand` 的一个重要特性。在*调试程序*时，这种可重复性对于对程序提供修正至关重要。

`rand` 函数通常生成伪随机数。反复调用 `rand` 会产生一个*看起来*是随机的数字序列。然而，序列本身在每次程序执行时都是相同的。一旦程序经过彻底调试，就可以对其进行配置，以便每次执行产生不同的随机数序列。这被称为*随机化*（randomizing），通过标准库函数 `srand` 实现。`srand` 接受一个 `unsigned int` 参数，并为 `rand` 函数设置种子，以便在每次程序运行时产生不同的随机数序列。

我们在 5.13 中演示了 `srand` 函数。格式符 `%u` 用于通过 `scanf` 读取 `unsigned int` 值。`srand` 函数的原型可以在 `<stdlib.h>` 中。

```c
// 图 5.13: fig05_13.c
// 随机化掷骰子程序。
#include <stdlib.h>
#include <stdio.h>
int main(void) {
    unsigned int seed; // 用于初始化随机数生成器的数字
    printf("%s", "Enter seed: ");
    scanf("%u", &seed); // 注意 unsigned int 使用 u
    srand(seed); // 设置随机数生成器的种子
    // 循环 10 次
    for (int i = 1; i <= 10; ++i) {
        // 选取 1 到 6 的随机数并输出
        printf("%10d", 1 + (rand() % 6));
        // 如果计数器能被 5 整除，开始新的一行输出
        if (i % 5 == 0) {
            printf("\n");
        }
    }
}
```

// 当游戏未完成时
```c
while (CONTINUE == gameStatus) { // 玩家继续掷
    sum = rollDice(); // 再次掷骰
    if (sum == myPoint) { // 通过点数赢得
        gameStatus = WON;
    } else
        if (7 == sum) { // 掷出7输了
            gameStatus = LOST;
        }
    }
    // 显示胜利或失败的消息
if (WON == gameStatus) { // 玩家赢了吗？
    puts("Player wins");
} else { // 玩家输了
    puts("Player loses");
}
```

// 掷骰子，计算和并显示结果
```c
int die1 = 1 + (rand() % 6); // 随机选择 die1 值
int die2 = 1 + (rand() % 6); // 随机选择 die2 值
```

// 显示本次掷骰的结果
```c
printf("Player rolled %d + %d = %d\n", die1, die2, die1 + die2);
return die1 + die2;
```

图 5.14 模拟骰子游戏。（部分 2/2。）

| 玩家在第一次掷中获胜 |
| :--- |
| 玩家掷出 5 + 6 = 11 |
| 玩家胜利 |

| 玩家在后续掷中获胜 |
| :--- |
| 玩家掷出 4 + 1 = 5 |
| 点数是 5 |
| 玩家掷出 6 + 2 = 8 |
| 玩家掷出 2 + 1 = 3 |
| 玩家掷出 3 + 2 = 5 |
| 玩家胜利 |

图 5.15 骰子游戏的示例运行。（部分 1/2。）

# 5.11 示例：一种机会游戏：引入 enum

玩家在第一次掷中输了

| :--- |
| 玩家掷出 1 + 1 = 2 |
| 玩家输了 |

玩家在后续掷中输了

| :--- |
| 玩家掷出 6 + 4 = 10 |
| 点数是 10 |
| 玩家掷出 3 + 4 = 7 |
| 玩家输了 |

**图 5.15** 骰子游戏的示例运行。（部分 2/2。）

在游戏规则中，注意玩家在第一次掷时必须掷两个骰子，并且在后续所有的掷中都可以这样做。我们定义了一个函数 `rollDice` 来掷骰子并计算它们的和。`gameStatus` 被定义为新类型 `enumStatus`，存储当前状态。第 8 行创建了一个程序员定义的类型 `enumeration`（枚举）。枚举是由关键字 `enum` 引入的，是一组由标识符表示的整数常量集合。枚举常量使程序更具可读性且易于维护。枚举中的值从 0 开始，并每次递增 1。在第 8 行中，常量 `CONTINUE` 的值为 0，`WON` 的值为 1，`LOST` 的值为 2。也可以为枚举中的每个标识符分配一个整数值（参见第 10 章）。枚举中的标识符必须是唯一的，但值可以重复。

> 常见编程错误 5.7
> 在定义一个枚举常量后对其赋值是一个语法错误。

> 良好编程实践 5.6
> 在枚举常量名中仅使用大写字母，使这些常量在程序中脱颖而出，并指示常量不是变量。

当游戏赢得时，无论是在第一次掷还是后续掷，`gameStatus` 被设置为 `WON`。当游戏失败时，无论是在第一次掷还是后续掷，`gameStatus` 被设置为 `LOST`。否则，`gameStatus` 被设置为 `CONTINUE` 游戏继续。

## 游戏在第一次掷时结束

在第一次掷之后，如果赢了游戏，`while` 语句（第 46–58 行）将被跳过，因为 `gameStatus` 不是 `CONTINUE`。程序继续执行第 61–66 行的 `if...else` 语句，如果 `gameStatus` 为 `WON` 则打印 "Player wins"，否则打印 "Player loses"。

## 第 5 章 C 函数

### 在后续掷中结束

在第一次掷之后，如果游戏没有结束，则 `sum` 被保存在 `myPoint` 中。由于 `gameStatus` 是 `CONTINUE`，执行继续进入 `while` 语句。每次通过 `while` 时，都会调用 `rollDice` 来产生一个新的和。`gamePoint` 被设置为 `WON` 以表示玩家胜利，`while` 测试失败，`if...else` 语句打印 "Players" 并终止执行。如果 `sum` 为 7（第 54 行），`gameStatus` 被设置为 `LOST` 以表示玩家输了，`while` 测试失败，`if...else` 语句打印 "Player loses" 并终止执行。

### 控制架构

注意程序中有趣的控制架构。我们使用了两个函数——`main` 和 `rollDice`——以及 `switch`、嵌套的 `if...else` 和嵌套语句。在本章的练习中，我们将研究骰子游戏有趣的特性。

## 5.12 存储存储类

在第 2–4 章中，我们使用标识符作为变量名。变量的属性包括名称、类型和值。在本章中，我们使用标识符作为变量名。变量的属性包括包括存储类、作用域和值。标识符的存储类决定了标识符的生存周期和作用域。作用域决定了标识符在程序中可以被引用的区域。5.13 节将讨论作用域和生存周期。标识符的存储类决定了标识符的生存周期和作用域。

在本章中，我们使用标识符作为用户定义的类型。标识符的存储类决定了标识符的生存周期和作用域。局部变量通常具有自动存储期。默认情况下，`auto` 关键字很少使用。对于本文，我们将具有自动存储期的变量统称为自动变量。

- `register` 关键字已过时，不应使用。
- C11 标准增加了线程局部存储类。

### 性能提示 5

自动存储是一种内存手段，因为自动变量只在需要时存在。它们在进入函数时创建

## 静态存储类

`extern` 和 `static` 关键字用于静态存储期的变量和函数。静态存储期的标识符从程序开始到程序终止。对于静态变量，存储在程序开始前分配并初始化一次。然而，即使函数在程序开始时存在，也不意味着这些标识符可以在整个程序中访问。生存周期和作用域是独立的问题，正如我们在 5.13 节中看到的。静态存储期的标识符有几种类型：外部标识符（如全局变量和函数名）以及带有 `static` 类的局部变量。全局变量和函数名默认的存储类为 `extern`。全局变量通过在程序执行之外放置声明来创建。全局变量和函数可以被其声明之后的任何函数引用。这是使用函数类型的一个例子——当我们为程序包含 `std.h` 时，函数原型被放置在我们的文件开头。

> 软件工程观察 5.1
> 将变量定义为全局变量而不是局部变量，可以避免在函数不需要访问或恶意修改变量时发生副作用。通常情况下，应避免全局变量，除非有某些特殊的性能需求（如第 14 章所述）。

> 软件工程观察 5.11
> 仅在特定函数使用的变量应该定义为函数的局部变量而不是全局变量。使用 `static` 关键字定义的局部变量仍然仅在其定义的函数已知，但与自动变量不同，静态局部变量在函数退出时会保留其值。下次调用函数时，静态局部变量包含其上次函数退出时的值。以下语句将局部 `count` 声明为静态并初始化为 1。

```c
static int count = 1;
```

所有静态存储期的数值变量在没有显式初始化时，默认初始化为 0。

## 5.13 作用域规则

标识符的作用域是程序中该标识符可以被用的部分。例如，当我们在块中定义一个局部变量时，它只能在该块中的定义之后或在该块嵌套的块中被引用。四种标识符分别是函数作用域、文件作用域、块作用域和原型类型作用域。

标签（以冒号标识，如 `start:`）是唯一具有函数作用域的标识符。标签可以使用它们所在的函数的任何地方，但不能在函数体之外引用。标签用于 `switch` 语句（作为 `case` 标签）和 `go` 语句（参见第 14 章）。标签在定义它们的函数内部是隐藏的。这种隐藏性——更正式地称为**最小特权原则**——信息隐藏——是软件工程的一项基本原则。在应用程序的上下文中，代码应该被授予完成其设计任务所需的权限和访问权限，而不更多。

在任何函数之外声明的标识符具有文件作用域。这种标识符从声明处开始到文件结束，在所有函数中都是已知的（即可访问的）。放在所有函数之外的全局变量、函数定义和原型具有文件作用域。

在块内部定义的标识符具有块作用域。块作用域结束于块的终止右括号 `}` 处。在函数开始定义的局部变量具有块作用域，函数参数也是如此，它们被函数视为局部变量。任何块都可以包含变量定义。当块嵌套时，如果外部块中的标识符与内部块中的标识符同名，则外部块会被隐藏，直到内部块结束。这意味着在内部块中执行时，内部块看到的是它自己的局部标识符的值，而不是包围它的外部块中同名标识符的值。声明为静态的局部变量仍然具有块作用域，尽管它们在程序启动之前就已经存在了。存储期不影响标识符的作用域。

唯一具有原型类型作用域的标识符是那些在函数原型参数列表中使用的标识符。如前所述，函数原型在参数列表中不需要名称——只需要类型。如果在函数原型的参数列表中使用了名称，编译器将忽略该名称。在函数原型中使用的标识符可以在程序的其他地方重用而不会产生歧义。

> ### 常见编程错误 5.8
> 不经意为内部块中的标识符使用了与外部块标识符相同的名称，而实际上你希望外部块中的标识符在内部块持续期间保持激活。

> ### 错误预防提示 5.4
> 避免使用隐藏外部作用域名称的变量名。

图 5.16 展示了全局变量、自动局部变量和静态局部变量的作用域问题。定义了一个全局变量 `x` 并初始化为 1（第 9 行）。该全局变量在任何定义了名为 `x` 变量的块（或函数）中都被隐藏。在 `main` 中，定义了一个局部变量 `x` 并初始化为 5（第 13 行）。打印该变量显示全局 `x` 在 `main` 中被隐藏。接下来在 `main` 中定义了一个新块，其中另一个初始化为 7 的局部变量 `x`（第 18 行）。打印该变量显示它隐藏了 `main` 外部块中的 `x`。值为 7 的变量 `x` 在退出块时自动销毁，然后再次打印 `main` 外部块中的局部 `x`，显示它不再被隐藏。

```c
// Fig 5.16: fig05_16.c
// Scoping.
#include <stdio.h>
void useLocal(void); // function prototype
void useStaticLocal(void); // function prototype
void useGlobal(void); // function prototype
int x = 1; // global variable
int main() {
    int x = 5; // local variable to main
    printf("x in outer scope of main is %d\n", x);
    { // start new scope
        int x = 7; // local variable to new scope
        printf("local in inner scope of main is %d\n", x);
    } // end new scope
    printf("x in outer scope of main is %d\n", x);
    useLocal(); // use automatic local x
    useStaticLocal(); // useStatic has static local x
    useGlobal(); // useGlobal global x
    useLocal(); // use reinitializes automatic local x
    useStaticLocal(); // static x retains its prior value
    useGlobal(); // global x also retains its value
    printf("\nlocal in main is %d\n", x);
}
// useLocal reinitializes local variable x during each call
void useLocal(void) {
    int x = 25; // initialized each time useLocal is called
    printf("\nlocal in useLocal is %d after entering useLocal\n", x);
    x++;
    printf("local in useLocal is %d before exiting useLocal\n", x);
}
```

**图 5.16** 作用域。（2 部分的第 1 部分。）

```c
// useStaticLocal initializes static variable x only the first time
// the function is called; value of x is saved between calls to the
// function
void useStaticLocal(void)
{
    // initialized once
    static int x = 50;
    printf("\n static x is %d on entering useStaticLocal\n", x);
    ++x;
    printf("local static x is %d on exiting useStaticLocal\n", x);
}
// functionGlobal modifies variable x during each call
void useGlobal(void)
{
    printf("\n x is %d on entering useGlobal\n", x);
    x = 10;
    printf("local x is %d on exiting useGlobal\n", x);
}
```
