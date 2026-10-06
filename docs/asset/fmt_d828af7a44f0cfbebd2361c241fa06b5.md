
`printf("nPlease enter your pin\n");`

`scanf("%d", &pin);`

`while (pin != 0) {`

`    printf("Incorrect pin entered. Re-enter pin\n");`

`    scanf("%d", &pin);`

`}`

要成功运行，需要在更早的地方声明 `pin`。

**Q5.8.** 修改上述程序，在 `while` 循环停止后产生所有数字的*总量*。

# 第五章 - 循环

## while 循环相对于 if 语句的优势

### 屏幕输入输出与程序

```c
1 #程序目标：显示错误使用 if 语句
2 #include <stdio.h>
3 main()
4 (
     int guess;
```
![](img/d66aad4cac4279bfe1f0f55cccf5946a_187_0.png)

代码

# 第五章 - 循环

## 注释

第 10 行包含不当的设计。运行程序时，用户会认为他们通过 7 第二次选择了正确数字。事实并非如此。正确数字是 9（第 5 行）。正确的设计意味着使用 `while` 循环而不是 `if` 条件（第 10 行）。本程序显示了 `while` 循环相对于 `if` 的优势。`while` 循环包含迭代控制流；`if` 则没有。使用 `if` 时，当第一次猜错数字时，会执行 `if` 语句的内容，即第 12 行和第 13 行。第二次猜测源于第 13 行的 `scanf`。这次猜测之后，无论是否猜中了正确数字，程序都会移动到第 17 行。如果使用了 `while` 循环而不是 `if` 条件，循环将返回第 8 行。

# 第五章 - 循环

## if 与 while 的比较总结

![](img/d66aad4cac4279bfe1f0f55cccf5946a_189_0.png)

![](img/d66aad4cac4279bfe1f0f55cccf5946a_189_1.png)

`while` 允许持续循环直到猜中正确数字。使用 `if`，当第二次猜错数字时，控制从第 13 行移动到第 16 行，而不是返回第 10 行。

# while 循环在猜数字游戏中继续嵌套的 if

### 屏幕输入与程序

`guessANoWithIf/ORKS22072017.c`

```c
1 /*程序目标：使用 while 循环进行猜数字游戏
2 包含两个嵌套的 if*/
3 #include <stdio.h>
4 main()
5 (
6 int noGuessed, winningNo = 9;
7 \n
8 printf("Guess a No: ");
9 scanf("%d", &noGuessed);
10
11 while (noGuessed != winningNo)
12 {
13 if (noGuessed < winningNo)
14 {
15 printf("Too low. Guess Again: ");
16 }
17
18 if (noGuessed > winningNo)
19 {
20 printf("Too high. Guess Again: ");
21 }
22 scanf("%d", &noGuessed);
23 }
24
25 printf("\nCorrect %d is the winning No \n", noGuessed);
26 printf("\n\nProgram End");
27 getch();
28 )
```

![](img/d66aad4cac4279bfe1f0f55cccf5946a_190_0.png)

# 第五章 - 循环

# 代码

```c
1: /*程序目标：使用 while 循环编写猜数字游戏
2:    包含两个嵌套的 if */
3: #include <stdio.h>
4: int main()
5: {
6: int noGuessed, winningNo = 9;
7: 
8:     printf("Guess a No: ");
9:     scanf("%d", &noGuessed);
10: 
11:     while (noGuessed != winningNo)
12:     {
13:         if (noGuessed < winningNo)
14:         {
15:             printf("太小了。再试一次: ");
16:         }
17: 
18:         if (noGuessed > winningNo)
19:         {
20:             printf("太高了。再试一次: ");
21:             scanf("%d", &noGuessed);
22:         }
23:     }
24: 
25:     printf("\n正确，%d 是中奖数字 ", noGuessed);
26:     printf("\n\n程序结束");
27:     getchar();
28: }
```

## 注释

猜数字游戏通过额外的代码进一步扩展。第 11 到 23 行的 `while` 循环包含两个嵌套的 `if`。这些判断告诉玩家猜的数字是太小还是太大。这些额外信息允许玩家更快地猜中目标数字。

## 使用 rand 函数生成随机数的屏幕输入输出

屏幕输入输出与程序
猜数字随机随机15082017.c |

```c
/*猜 1 到 10 之间的数字游戏。
中奖数字是随机生成的*/
#include <stdlib.h>
#include <stdio.h>
int main() {
  int randomNo
```
```

E:\Books\GuessANoRandomNoRandomWORKS15082017.exe

猜一个数字: 5

太高了。再试一次: 1

太小了。再试一次: 3

太高了。再试一次: 2

是的。你猜对了。

程序结束

```

# 代码

```c
1: /*猜 1 到 10 之间的数字游戏。
2: 中奖数字是随机生成的*/
3: #include <stdlib.h>
4: #include <stdio.h>
5: int main()
6: {
7:     int randomNo, winningNo, guessedNo;
8:
9:     randomNo = rand() % 10;
10:    winningNo = randomNo + 1;
11: 
12:     printf("猜一个数字: ");
13:     scanf("%d", &guessedNo);
14: 
15:     while (guessedNo != winningNo)
16:     {
17:         if (winningNo > guessedNo)
18: 
19:             printf("太小了。再试一次: ");
20:             scanf("%d", &guessedNo);
21:         }
22: 
23:         if (winningNo < guessedNo)
24:         {
25:             printf("太高了。再试一次: ");
26:             scanf("%d", &guessedNo);
27:         }
28: 
29:     printf("是的。你猜对了。 \n");
30: 
31:     printf("\n程序结束 ");
32:     getch();
33: }
34: }
```

## 注释

从 15 到 28 行的循环允许持续猜数字。这意味着通过第 9 行的 `rand()` 函数，中奖数字被随机设置为计算机处理器设置（而不是当前时间）。`%10` 意味着随机数范围是从 0 到 9，因为 `%10` 将计算机生成的随机数设置为小于 10 的余数。如果第 8 行的 `%10` 语句是 `%1000`，那么随机数范围将是 0 到 999。第 10 行的 `+1` 意味着中奖数字的范围是 1 到 10（包含边界值），而不是 0 到 9。

循环通过第 12 行的 `printf` 语句提示玩家输入一个数字。第 13 行的 `scanf` 允许玩家从计算机键盘输入数字。第 17 行和 27 行让玩家知道猜的数字太小还是太大。由于在此阶段还没有猜中目标数字，因此第 15 到 28 行的 `while` 循环不会退出。相反，玩家会被提示再次猜测。由于第 15 行的结果会扫描另一个猜测。玩家将一直猜，直到选中目标数字为止。然后第 15 到 28 行的 `while` 循环退出，控制流转到第 29 行，该行让玩家知道猜中了。

第 3 行添加了另一个库，包含：

```c
3: #include <stdlib.h>
```

这意味着包含了一个标准库头文件。这提供了额外的处理功能。

## 对随机数生成的批判

上述随机数生成器在每次打开和运行程序时都会产生相同的随机数。随机数是由计算机处理器决定的。因此，玩家一旦熟悉了这个程序，就会熟悉每次玩游戏时生成的数字。这意味着 `rand()` 函数需要修改。可以通过在每次玩游戏时将随机数设置为时间（而不是计算机确定的时间）来实现。

## 随机数设置为当前时间 屏幕输入输出与程序
猜数字随机随机设置时间12017WORKS.c

```c
1: //猜 1 到 10 之间的数字游戏。
2: 中奖数字随机设置为当前时间：
3: #include <stdio.h>
4: #include <stdlib.h>
5: main() {
6:     int randomNo, guessedNo;
7:     time_t t;
8: //随机数生成器初始化
9:     srand((unsigned)time(NULL));
10:    randomNo = rand() % 10;
11:    winningNo = randomNo + 1;
12:     printf("猜一个数字: ");
13:     scanf("%d", &guessedNo);
14: 
15:     while (guessedNo != winningNo)
16:     {
17:         if (winningNo > guessedNo)
18:         {
19:             printf("太小了。再试一次: ");
20:             scanf("%d", &guessedNo);
21:         }
22: 
23:         if (winningNo < guessedNo)
24:         {
25:             printf("太高了。再试一次: ");
26:             scanf("%d", &guessedNo);
27:         }
28:     }
29:     printf("\n正确，%d 是中奖数字 \n", winningNo);
30:     printf("\n程序结束");
31:     getchar();
32: }
```

# 代码

```c
1: /*猜 1 到 10 之间的数字游戏。
2: 中奖数字是随机生成的*/
3: #include <stdio.h>
4: #include <stdlib.h>
5: int main()
6: {
7:     int randomNo, winningNo, guessedNo;
8:     time_t tt;
9: 
10: //随机数生成器初始化
11:     srand((unsigned)time(NULL));
12:     randomNo = rand() % 10;
13:     winningNo = randomNo + 1;
14: 
15:     printf("猜一个数字: ");
16:     scanf("%d", &guessedNo);
17: 
18:     while (guessedNo != winningNo)
19:     {
20:         if (winningNo > guessedNo)
21:         {
22:             printf("太小了。再试一次: ");
23:             scanf("%d", &guessedNo);
24:         }
25: 
26:         if (winningNo < guessedNo)
27:         {
28:             printf("太高了。再试一次: ");
29:             scanf("%d", &guessedNo);
30:         }
31:     }
32:     printf("\n是的。你猜对了。 \n");
33:     printf("\n程序结束 ");
34:     getch();
35: }
```

## 注释

在上面的代码中，每次打开并运行程序，生成的随机数都是不同的。这是因为 `time_tt`（当前行，第8和11行）在每次打开程序时都是不同的。`srand` 替换了 `rand`（第11行）。这意味着随机数被“种子化”，这是随机数生成中的一个表达式。这确保了每次玩游戏时数字都是确定的。连续两次使用 `rand` 将看到相同的目标数字。使用 `srand` 后，每次目标数字都会不同。因此，玩家无法预测目标数字。

## 使用 while 循环进行多选题屏幕输入输出

```

E:\C\WhileLoopTwice147WORK505.c

选择以下数字之一：

历史上最大的 147 是：

1 John Parrot 在 1974 年对 Steve Davis。

2 Steve Davis 在 1982 年对 John Spencer。

3 Cliff Thorburn 在 1983 年对 Terry Griffiths。

4 Jimmy White 在 1947 年对 Jimmy White。

5 Jimmy White 完成 147 仅用 7 分 41 秒

6 在 2014 年7月14日凌晨 1:47 在 147 Club。

7 Steven Henry 在 1995 年对 Jimmy White。

8 John Higgins 在 2007 年对 Dennis Taylor。

9 Ding Junhui 在 2011 年 PFB 公开赛中的第二次 147。

10 Marco Fo 在 2015 年大师赛中的 147。

11 Ronnie O'Sullivan 在 147 Club 完成的 147。

12 美美的 Virgin's 147 路通过了

13 J S Bach 的 BMW 147，马力为 127。

```

# 第五章 - 循环

## 程序

```c
 //程序目标：在多选题中使用 while 循环。
#include <stdio.h>
int main() {
    int guess;
    printf("Choose one of the following numbers : \n\n");
    printf("The greatest 147 of all time is: \n\n");
    printf("John Parrot's 1974 against Steve Davis.\n");
    printf("Steve Davis's 1982 against John Spencer.\n");
    printf("Cliff Thorne's 1983 against Terry Griffiths.\n");
    printf("White's 147 in 1984 against Jimmy White.\n");
    printf("Jimmy White's 147 completed in 7 41 secs \n");
    printf("John Higgins's 2000 against Dennis Taylor.\n");
    printf("at 1.27am on 14 July 2014 at the 147 Club.\n");
    printf("Steve Henry's 1995 against Jimmy White.\n");
    printf("Ding Junhui's 147 at the 2015 FFB Open\n");
    printf("Marco O'Sullivan's 147 at the 147 Club.\n");
    printf("The R147 Dublin to Cavan Road that leads through:\n");
    printf("  the beautiful Virginia Lake district.\n");
    printf("J S Bach's BWV 147 of 1716.\n\n");
    int guess = 1;
    scanf("%d", &guess);
}
```

## 工资条单设计中的迭代流控制

关系运算符可以与循环结合使用。例如，在处理工资单时，当存在最低时费率（例如每小时 5 美元），且存在防止过度金额的保护措施（例如每小时 20 美元）。

## 工资程序

### 屏幕输入输出与程序

```c
1 /程序目标：展示两个等值运算符的作用"
2 #include <stdio.h>
3 main()
4 {
5     int ratePerHour, noOfHours, minimumRate = 5,
```
