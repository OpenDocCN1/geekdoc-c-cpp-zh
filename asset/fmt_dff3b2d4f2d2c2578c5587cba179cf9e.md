
上述的讨论和图表存在一个缺陷。我们展示了 `main` 调用 `square` 以及 `square` 返回到 `main`，但实际上，`printf` 也是一个函数。当你学习图 5.3 中的代码时，可能会倾向于认为 `main` 调用 `printf`，那么在调用 `printf` 之前必须完全知道 `printf` 的参数值。因此执行过程如下：

- 1. 操作系统调用 `main`，因此 `main` 的栈帧被推入栈中。
- 2. `main` 调用 `square`，因此 `square` 的栈帧被推入栈中。
- 3. `square` 计算并向 `main` 返回一个值，用于 `printf` 的参数列表，因此 `square` 的栈帧从栈中弹出。
- 4. `main` 调用 `printf`，因此 `printf` 的栈帧被推入栈中。
- 5. `printf` 显示其参数，然后返回到 `main`，因此 `printf` 的栈帧从栈中弹出。
- 6. `main` 终止，因此 `main` 的栈帧从栈中弹出。

# 数据结构

你已经看到栈数据结构在实现支持程序执行的机制方面有多有价值。数据结构在计算机科学中有许多重要应用。我们将在第 12 章讨论栈、队列、列表和树。

## 自测

（填空）每当一个函数调用另一个函数时，一个条目就会推入栈中。这个条目被称为 ________，它包含了函数返回到调用函数时所需的返回地址。

答案：栈 (`stack`)。

（对/错）函数的栈帧是预留局部变量内存的理想位置。该栈帧仅在函数激活状态时存在。当函数返回——并且不再需要其局部变量时——栈帧会从栈中弹出。此时，程序将不再能感知到局部变量。

答案：对 (`True`)。

# 5.8 头文件

每个标准库都有一个相应的头文件，包含该库中所有函数的原型，以及这些函数所需的各种数据类型和常量定义。下表按字母顺序列出了程序中可能包含的标准库头文件。C 标准还包含了额外的头文件。表中多次使用的“宏”一词将在第 14 章中详细讨论。

# 第 5 章 函数

| 头文件 | 说明 |
| --- | --- |

我们在书中使用或讨论的头文件：

- `<assert.h>` 包含用于辅助程序调试调试的信息。
- `<ctype.h>` 包含测试字符特定属性的函数原型，以及可用于大和小写字母相互转换的函数原型。
- `<float.h>` 包含系统的浮点数大小限制。
- `<limits.h>` 包含系统的整数大小限制。
- `<math.h>` 包含数学库函数的原型。
- `<signal.h>` 包含处理程序执行期间可能出现的各种条件的函数原型和宏。
- `<stdarg.h>` 定义了处理数量和类型未知的函数参数列表的宏。
- `<stdio.h>` 包含标准输入输出库函数的原型以及它们使用的信息。
- `<stdlib.h>` 包含数字到文本、文本到数字转换的函数原型，内存分配、随机数以及其他实用函数原型。
- `<string.h>` 包含字符串处理函数的函数原型。
- `<time.h>` 包含时间函数的原型和时间类型。

其他头文件：

- `<errno.h>` 定义了用于报告错误的有用宏。
- `<locale.h>` 包含关于当前区域设置的信息。
- `<setjmp.h>` 包含允许系统跳转的函数原型。
- `<stdlib.h>` 包含常用类型定义。

你可以创建自定义头文件。程序员定义的头文件可以使用以下方式包含，例如，`square` 位于：

```c
#include "square.h"
```

第 14.2 节提供了关于包含头文件的额外信息，例如引号 (`"`) 而不是角括号 (`<`)。

## 自测

- _______ 头文件包含字符串处理函数的原型。

答案：`<string.h>`

# 5.9 按值和按引用传递参数

在编程语言中，传递参数有两种方式——按值传递和按引用传递。按值传递时，参数的值会被复制并传递给函数。改变不会影响原始变量。按引用传递时，调用者允许函数修改原始变量。

每当调用函数不需要修改调用者的原始值时，应使用按值传递。这可以防止阻碍正确可靠软件系统的副作用（变量修改）。只有在需要修改原始变量时才使用按引用传递。

在 C 中，所有参数都是按值传递的。在第 7 章指针中，我们将展示如何实现引用传递。在第 6 章，我们将看到数组是如何按引用传递的。我们将在第 7 章看到这并不矛盾。现在，我们关注按值传递。

## 自测

- （对/错）当按值传递时，参数的值会被复制并传递给函数。对副本的也会应用于原始变量：错 (`False`)。按值传递时，副本的变化不会影响原始变量。
- （对/错）只有在需要修改原始变量时才使用按引用传递：对 (`True`)。

# 5.10 随机数生成

我们现在对模拟和游戏进行简短（且希望是有趣的）的探索。在本节和下一节中，我们将开发一个结构良好的游戏程序。该程序使用了函数以及我们学习过的几种控制语句。可以使用 `<stdlib.h>` 头文件中的 C 标准库函数 `rand` 在计算机应用程序中引入随机元素。

- C 标准库函数 `rand` 已知是“可预测的”，这可能会产生安全漏洞。我们首选的每个平台都提供了非标准的安全的随机数生成器。我们将在第 5.17 节安全 C 编程——安全随机数生成中提到这一点。

## 获取随机整数值

考虑以下语句：

```c
int value = rand();
```

`rand` 函数生成一个在 0 到 `RAND_MAX` 之间的整数（在 `<stdlib.h>` 头文件中定义的符号常量）。C 标准规定，`RAND_MAX` 的值至少必须为 32,767，这是双字节（即 16 位）整数的最大值。本节中的程序已在 Microsoft Visual C++ 上进行过测试，其最大 `RAND_MAX` 值为 32,767；在 GNU gcc 和 Xcode Clang 上进行过测试，其最大 `RAND_MAX` 值为 2,147,483,647。如果 `rand` 随机产生整数，那么在每次调用 `rand` 时，0 到 `RAND_MAX` 之间的每个数字都有相等的几（或概率）被选中。

`rand` 直接产生的数值范围可能与特定应用程序所需的范围不同。例如，一个模拟掷硬币的程序可能只需要 `0` 表示“正面”，`1` 表示“反面”。一个模拟六面骰子的掷骰子程序则需要 1 到 6 之间的随机整数。

## 掷六面骰子

为了演示 `rand`，让我们编写一个程序（图 5.4）来模拟掷 10 次六面骰子，并打印每次掷的值。

```c
// fig5_04.c
// Shifted
```

| 6 | 6 | 5 | 5 | 6 | 5 | 1 | 1 | 5 | 3 |

**图 5.4** 由 `1 + rand() % 6` 产生的经过偏移和缩放的随机整数。

`rand` 函数的原型定义在 `<stdlib.h>` 中。在第 9 行中，我们将取数运算符（`%`）配合 `rand` 如下使用：

```c
rand() % 6
```

以产生 0 到 5 范围内的整数。这被称为**缩放（scaling）**。数字 6 被称为**缩放因子（scaling factor）**。然后我们通过在之前的结果上加 1 来**偏移（shift）**产生的数字范围。输出结果证实了结果在 1 到 6 的范围内——这些随机值的变化顺序因编译器而异。

## 掷 60,000,000 次六面骰子

为了证明这些数字出现的概率大致相等，让我们用图 5.5 中的程序模拟掷 60,000,000 次骰子。从 1 到 6 的每个整数都应该大约出现 10,000,000 次。

```c
// fig05.c
// Rolling a six-sided die 60,000,000 times.
#include <stdio.h>
#include <stdlib.h>

int main() {
    int frequency1 = 0; // 点 1 计数器
    int frequency2 = 0; // 点 2 计数器
    int frequency3 = 0; // 点 3 计数器
    int frequency4 = 0; // 点 4 计数器
    int frequency5 = 0; // 点 5 计数器
    int frequency6 = 0; // 点 6 计数器

    // 循环 60000000 次并汇总结果
    for (int roll = 1; roll < 60000000; ++roll) {
        int face = 1 + rand() % 6; // 1 到 6 的随机数

        // 确定点数并增加相应的计数器
        switch (face) {
            case 1: // 掷出 1
                ++frequency1;
                break;
            case 2: // 掷出 2
                ++frequency2;
                break;
            case 3: // 掷出 3
                ++frequency3;
                break;
            case 4: // 掷出 4
                ++frequency4;
                break;
            case 5: // 掷出 5
                ++frequency5;
                break;
            case 6: // 掷出 6
                ++frequency6;
                break; // 可选
        }
    }

    // 以表格格式显示结果
    printf("%s: %s\n", "Face", "Frequency");
    printf("%1d: %d\n", frequency1);
    printf("%2d: %d\n", frequency2);
    printf("%3d: %d\n", frequency3);
    printf("%4d: %d\n", frequency4);
    printf("%5d: %d\n", frequency5);
    printf("%6d: %d\n", frequency6);
}
```

**图 5.5** 掷 60,000,000 次六面骰子。（第一部分，共 2 部分）

| 点数 (Face) | 频率 (Frequency) |
| :--- | :--- |
| 1 | 9999294 |
| 2 | 10002929 |
| 3 | 9999294 |
| 4 | 10004090 |
| 5 | 10005296 |
| 6 | 9996802 |

输出证实了结果在 1 到 6 的范围内——这些随机值的变化顺序随编译器有很大不同。

## 5.11 游戏模拟案例研究：剪刀石头石头布

```c
// fig05_07.c
// 模拟剪刀石头石头布游戏
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h> // 包含 time 函数原型
```

```c
enum GameStatus {CONTINUE, GAME_WON, GAME_LOST}; // 常量表示游戏状态
enum RoundStatus {DRAW, WON, LOST}; // 常量表示局数状态
enum Shape {ROCK, PAPER, SCISSORS}; // 表示可能的形状常量
```

```c
enum Shape computerRandomShape(void); // playRandomShape 函数原型
enum GameStatus getRoundStatus(enum Shape, enum Shape);
enum Shape intToInt(int);
char* getStringFromShape(enum Shape);
```

```c
int main(void) {
    rand(NULL); // 根据当前时间随机化
    enum GameStatus gameStatus = CONTINUE; // 可能是 CONTINUE, GAME_WON 或 GAME_LOST
    int bestOfN = 3; // 三局两胜制
    int winThreshold = (bestOfN + 2) / 1;
    int playerWinCount = 0;
    int computerWinCount = 0;
    int roundNum = 0;
```

```c
// 当游戏未完成时
while (CONTINUE == gameStatus) { // 应继续游戏
    printf("\n%d\n===\n", roundNum++);
    printf("Enter 0 (ROCK), or 1 (PAPER), or 2 (SCISSORS): \n");
```

```c
    int playerShapeInt = -1;
    scanf("%d", &playerShapeInt);
    enum Shape playerShape = intToInt(playerShapeInt); // 玩家形状
    enum Shape computerShape = computerRandomShape(); // 电脑随机出一个形状
    enum RoundStatus roundStatus = getRoundStatus(playerShape, computerShape); // 当前局胜者
```

```c
    switch (roundStatus) {
    case DRAW:
        printf("It's a DRAW!\n");
        break;
```

图 5.7 模拟剪刀石头石头布游戏。（4 部分中的第 1 部分）。

## 第 5 章 函数

```c
case WON:
    printf("Player WON!\n");
    if (++playerWinCount == winThreshold) {
        // 计数，如果胜利次数达到阈值，
        // 玩家赢得游戏
        gameStatus = GAME_WON;
    }
    break;
case LOST:
    printf("Player LOST!\n");
    if (++computerWinCount == winThreshold) {
        // 计数，如果胜利次数达到阈值，
        // 电脑赢得游戏
        gameStatus = GAME_LOST;
    }
    break;
}
switch (gameStatus) {
    case WON:
        printf("**Best of %d game is WON by player!**\n", bestOfN);
        break;
    case LOST:
        printf("Best of %d game is WON by computer!**\n", bestOfN);
        break;
    case CONTINUE:
        printf("**Error! Should not reach here!**\n");
}

// 玩一局并显示结果
enum Shape computerPlayShape(void) {
    enum Shape randomShape = convertToShape(rand() % 3);
    printf("Computer played %s\n", getStringFromShape(randomShape));
    return randomShape;
}

enum RoundStatus getRoundStatus(enum Shape playerShape, enum computerShape) {
    if (playerShape == computerShape) {
        return DRAW;
    } else if (playerShape == ROCK && computerShape == SCISSORS)
    || (playerShape == SCISSORS && computerShape == PAPER)
    || (playerShape == PAPER && computerShape == ROCK)) {
        return WON;
    } else {
        return LOST;
    }
}
```

图 5.7 | 模拟剪刀石头石头布游戏。（4 部分中的第 2 部分）

```c
enum Shape intToShape(int shapeValue) {
    return (enum Shape) shapeValue;
}

char * getStringFromShape(enum Shape shape) {
    switch (shape) {
        case ROCK:
            return "ROCK";
        case PAPER:
            return "PAPER";
        case SCISSORS:
            return "SCISSORS";
    }
    return "";
}
```

玩家在几轮后胜利：
