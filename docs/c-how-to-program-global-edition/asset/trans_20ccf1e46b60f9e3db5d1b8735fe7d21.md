
开始比赛时打印

    BANG !!!!!
    AND THEY'RE OFF !!!!!

然后，对于时钟的每次滴答（即循环的每次迭代），打印一条 70 个位置的行，显示乌龟所在位置的字母 T 和兔子所在位置的字母 H。偶尔，竞争者会落在同一个格子上。在这种情况下，乌龟咬住兔子，你的程序应从该位置开始打印 OUCH!!!。除 T、H 或平局情况下的 OUCH!!! 之外的所有打印位置应为空白。

打印完每行后，检查是否有动物到达或超过第 70 格。如果是，则打印获胜者并终止模拟。如果乌龟获胜，打印 TORTOISE WINS!!! YAY!!! 如果兔子获胜，打印 Hare wins. Yuch. 如果两只动物在同一时钟滴答时获胜，你可能想偏爱乌龟（“弱者”），或者你可能想打印 It's a tie. 如果没有动物获胜，则再次执行循环以模拟下一个时钟滴答。当你准备好运行程序时，召集一群粉丝观看比赛。你会惊讶于观众的参与程度！

## 7.18（洗牌和发牌修改）
修改图 7.24 中的洗牌和发牌程序，使洗牌和发牌操作由同一个函数（shuffleAndDeal）执行。该函数应包含一个嵌套循环结构，其与图 7.24 中的函数 shuffle 相似。

## 7.19 假设用户输入两个长度相同的字符串，这个程序做什么？

```c
// ex07_19.c
// What does this program do?
#include <stdio.h>
#define SIZE 80

void mystery1(char *s1, const char *s2); // prototype

int main(void)
{
    char string1[SIZE]; // create char array
    char string2[SIZE]; // create char array

    puts("Enter two strings: ");
    scanf("%79s%79s", string1, string2);
    mystery1(string1, string2);
    printf("%s", string1);
}

// What does this function do?
void mystery1(char *s1, const char *s2)
{
    while (*s1 != '\0') {
        ++s1;
    }

    for (; *s1 = *s2; ++s1, ++s2) {
        ; // empty statement
    }
}
```

## 7.22（迷宫遍历）
以下网格是迷宫的二维数组表示。

![](img/bf54db922e6fa8319cba11069e785521_350_0.png)

# 符号代表迷宫的墙壁，而句点（.）代表迷宫中可能路径的格子。

有一个简单的走迷宫算法可以保证找到出口（假设存在出口）。如果没有出口，你将再次回到起始位置。将你的右手放在右侧的墙上并开始向前走。永远不要把手从墙上移开。如果迷宫向右转，你就跟随墙向右走。只要你不把手从墙上移开，最终你就会到达迷宫的出口。你所走的路可能不是最短的路径，但你保证能走出迷宫。

编写递归函数 mazeTraverse 来遍历迷宫。该函数应接收一个表示迷宫的 12×12 字符数组和迷宫的起始位置作为参数。在 mazeTraverse 尝试定位迷宫出口时，它应在路径中的每个格子放置字符 X。函数应在每次移动后显示迷宫，以便用户可以看到迷宫被解决的过程。

## 7.23（随机生成迷宫）
编写一个函数 mazeGenerator，它接收一个二维 12×12 字符数组作为参数并随机生成一个迷宫。该函数还应提供迷宫的起始和结束位置。使用练习 7.22 中的函数 mazeTraverse 尝试几个随机生成的迷宫。

## 7.24（任意大小的迷宫）
将练习 7.22–7.23 中的函数 mazeTraverse 和 mazeGenerator 推广，以处理任意宽度和高度的迷宫。

## 7.25（指向函数的指针数组）
重写图 6.22 的程序以使用菜单驱动界面。程序应向用户提供以下四个选项：

```
Enter a choice:
0 Print the array of grades
1 Find the minimum grade
2 Find the maximum grade
3 Print the average on all tests for each student
4 End program
```

使用函数指针数组的一个限制是所有指针必须具有相同的类型。指针必须指向具有相同返回类型且接收相同类型参数的函数。因此，图 6.22 中的函数必须修改，使它们各自返回相同的类型并接受相同的参数。修改函数 minimum 和 maximum，使其打印最小或最大值并返回 nothing。对于选项 3，修改图 6.22 中的函数 average，使其输出每个学生的平均值（而不是特定学生）。函数 average 应返回 nothing 并接受与 printArray、minimum 和 maximum 相同的参数。将指向四个函数的指针存储在数组 processGrades 中，并使用用户所做的选择作为索引来调用每个函数。

## 7.26 假设用户输入两个长度相同的字符串，这个程序做什么？

```
// ex07_36.c
// What does this program do?
#include <stdio.h>
#define SIZE 80

int mystery3(const char *s1, const char *s2); // prototype

int main(void)
{
    char string1[SIZE]; // create char array
    char string2[SIZE]; // create char array

    puts("Enter two strings: ");
    scanf("%79s%79s", string1, string2);
    printf("The result is %d\n", mystery3(string1, string2));
}

int mystery3(const char *s1, const char *s2)
{
    int result = 1;

    for (; *s1 != '\0' && *s2 != '\0'; ++s1, ++s2) {
        if (*s1 != *s2) {
            result = 0;
        }
    }

    return result;
}
```

## 特别章节：构建自己的计算机
在接下来的几个练习中，我们暂时从高级语言编程的世界中转移开来。我们“打开”一台计算机并查看其内部结构。我们介绍机器语言编程并编写几个机器语言程序。为了使这次体验特别有价值，我们随后构建一台计算机（通过基于软件的模拟技术），你可以在其上执行你的机器语言程序！

## 7.27（机器语言编程）
让我们创建一个我们称之为 Simpletron 的计算机。如其名所示，它是一个简单的机器，但正如我们很快会看到的，它也是一个强大的机器。Simpletron 运行用它唯一直接理解的语言编写的程序——即 Simpletron 机器语言，简称 SML。

Simpletron 包含一个累加器——一个“特殊寄存器”，信息在 Simpletron 在计算中使用该信息或以各种方式检查它之前被放入其中。Simpletron 中的所有信息都以字为单位处理。一个字是一个带符号的四位十进制数，例如 +3364、-1293、+0007、-0001 等等。Simpletron 配备了 100 字内存，这些字由其位置编号 00、01、...、99 引用。

在运行 SML 程序之前，我们必须加载或将程序放入内存中。每个 SML 程序的第一个指令（或语句）始终放置在位置 00。

SML 编写的每个指令占用 Simpletron 内存的一个字，因此指令是带符号的四位十进制数。我们假设 SML 指令的符号始终为正，但数据字的符号可以是正或负。Simpletron 内存中的每个位置可能包含指令、程序使用的数据值或未使用（因此未定义）的内存区域。每个 SML 指令的前两位数字是操作码，指定要执行的操作。SML 操作码总结在图 7.32 中。

| Operation code | Meaning |
|---|---|
| *输入/输出操作：* | |
| `#define READ 10` | 从终端读取一个字到内存中的特定位置。 |
| `#define WRITE 11` | 将内存中特定位置的一个字写入终端。 |
| *装载/存储操作：* | |
| `#define LOAD 20` | 从内存中特定位置加载一个字到累加器。 |
| `#define STORE 21` | 将累加器中的一个字存储到内存中的特定位置。 |
| *算术操作：* | |
| `#define ADD 30` | 将内存中特定位置的一个字加到累加器中的字上（结果留在累加器中）。 |
| `#define SUBTRACT 31` | 从累加器中的字减去内存中特定位置的一个字（结果留在累加器中）。 |
| `#define DIVIDE 32` | 用内存中特定位置的一个字除累加器中的字（结果留在累加器中）。 |
| `#define MULTIPLY 33` | 将内存中特定位置的一个字乘以累加器中的字（结果留在累加器中）。 |
| *转移控制操作：* | |
| `#define BRANCH 40` | 分支到内存中的特定位置。 |
| `#define BRANCHNEG 41` | 如果累加器为负，则分支到内存中的特定位置。 |
| `#define BRANCHZERO 42` | 如果累加器为零，则分支到内存中的特定位置。 |
| `#define HALT 43` | 停止——即程序已完成其任务。 |

Fig. 7.32 | Simpletron Machine Language (SML) operation codes.

SML 指令的最后两位数字是操作数，即包含要操作的字所在的内存位置的地址。现在让我们考虑几个简单的 SML 程序。以下 SML 程序从键盘读取两个数字，并计算并打印它们的和。指令 +1007 从键盘读取第一个数字并将其放入位置 07（已初始化为零）。然后 +1008 将下一个数字读入位置 08。加载指令 +2007 将第一个数字放入累加器，而加法指令 +3008 将第二个数字加到累加器中的数字上。所有 SML 算术指令都将其结果留在累加器中。存储指令 +2109 将结果放回内存位置 09，写指令 +1109 从中取出数字并打印它（作为带符号的四位十进制数）。停止指令 +4300 终止执行。

