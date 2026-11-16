

银行对账单还应包含以下汇总信息：

- 存款总笔数：
- 存款总金额：
- 支票总笔数：
- 支票总金额：
- 服务费总额：
- 期初余额：
- 期末余额：

下面显示的是你程序中应使用的 main() 函数：

```c
int main(void) {
    char code;
    double amount, service, balance;
    double amtCheck, amtDeposit, openBalance, closeBalance;
    int numCheck, numDeposit;

    if (! (fp = fopen("account.txt", "r"))) {
        printf("account.txt could not be opened for input.");
        exit(1);
    }

    if (! (csis = fopen("csis.txt", "w"))) {
        printf("csis.txt could not be opened for output.");
        exit(1);
    }

    amount = 0.0;
    service = 0.0;
    balance = 0.0;
    amtCheck = 0.0;
    amtDeposit = 0.0;
    openBalance = 0.0;
    closeBalance = 0.0;
    numCheck = 0;
    numDeposit = 0;

    outputHeaders();

    while (!feof(fp)) {
        fscanf(fp, "%c %lf\n", &code, &amount);
        if (code == 'I') {
            initialBalance(amount, &balance, &service, &openBalance);
        }
        else if (code == 'D') {
            deposit(amount, &balance, &service, &numDeposit,
                    &amtDeposit);
        }
        else {
            check(amount, &balance, &service, &numCheck, &amtCheck);
        }
    }
    closeBalance = balance + service;
    outputSummary(numDeposit, amtDeposit, numCheck, amtCheck,
                  openBalance, service, closeBalance);
    fclose(csis);
    fclose(fp);
    return 0;
}
```

你需要为程序编写五个函数（及其原型）：

```
outputHeaders()
initialBalance()
deposit()
check()
outputSummary()
```

这些函数将使用计数器和求和来跟踪支票账户的不同组成部分，以及输出与银行对账单相关的特定信息。请注意，某些函数参数作为输入参数传递，某些作为输入-输出参数传递。请务必在函数中正确使用间接运算符 (*)。

## `account.txt` 的内容如下：

| 类型 | 金额 |
| :--- | :--- |
| I | 478.83 |
| D | 127.45 |
| D | 619.84 |
| C | 945.12 |
| C | 4.76 |
| D | 32.91 |
| C | 1.06 |
| D | 184.32 |
| C | 495.18 |
| C | 141.81 |
| C | 255.10 |
| D | 250.00 |
| D | 123.88 |
| D | 245.05 |
| D | 873.25 |
| C | 981.12 |
| D | 317.84 |
| C | 812.73 |
| D | 606.12 |

你的程序中不应使用任何全局变量，除了文件指针的声明之外（除了文件指针）。全局变量是在 `main()` 之外声明的变量。请勿修改我上面提供的 `main()` 函数。

程序输出应发送到终端窗口（您的屏幕）以及请求的 `csis.txt` 输出文件。请务必阅读关于捕获程序输出的文档。您的全名和 Palomar ID 号必须作为注释出现在包含 `main()` 的源文件中。请务必将 `csis.txt` 输出文件包含在 zip 压缩包中。

## 日期实验室

本次作业将侧重于函数的使用和参数传递。你需要构建一个 C 程序 date.c，执行以下每项操作：

```
Converts a calendar date into a Julian date
Converts a Julian date into a calendar date.
Computes the number of days between any two calendar dates.
```

日历日期只是包含年、月、日的日期，而儒略日是 1 到 366 之间（包含 1 和 366）的整数，表示自当年的 1 月 1 日以来已过去的天数（包括计算日期当天）。例如，日历日期 4/12/2008 相当于儒略日 103, 2008。

你的程序应包含一个选择菜单（提示：考虑 do-while 循环），允许用户选择其中一个选项。示例如下：

```
DATE SELECTION MENU
1) Convert calendar date into Julian date
2) Convert Julian date into calendar date
3) Compute days between two calendar dates
4) Exit program
ENTER SELECTION (1 - 4):
```

请确保你的程序为每个必需操作包含单独的函数，并根据需要传递参数。请记住，除了文件指针外，程序中不允许使用全局变量。你的程序至少应创建以下函数：

| 函数 | 描述 |
|---|---|
| displayMenu | 显示选择菜单并提示用户选择 |
| getCalendarDate | 提示并从用户处获取日历日期 |
| getJulianDate | 提示并从用户处获取儒略日 |
| toCalendar | 将儒略日转换为日历日期 |
| toJulian | 将日历日期转换为儒略日 |
| daysBetweenDates | 计算两个日历日期之间的天数 |

计算两个日历日期之间天数的提示：对于每个日期，计算自 1900 年 1 月 1 日以来的天数，然后相减。

本次作业中，我们将闰年定义为能被 4 整除但不能被 100 整除的任何年份，但能被 400 整除的年份是闰年。这是一个可用于计算闰年的函数。试着分析其细节。

```
int isLeapYear(int year) {
    return (((year % 4) && year % 100) || !(year % 400));
}
```

下面给出了实验的测试数据。请务必提交下面每组测试数据的输出。每组测试数据后括号中的信息是正确（希望如此）的解决方案。你可以使用这些解决方案在提供的测试数据上测试你的程序。最终，你的程序应该能够在任何有效数据上运行。

### 将日历日期转换为儒略日
11 15 1922 (319, 1922)
2 29 1984 ( 60, 1984)
7 7 2000 (189, 2000)

### 将儒略日转换为日历日期
53 1947 ( 2/22/1947)
211 1995 ( 7/30/1995)
360 2006 (12/26/2006)

### 计算两个日历日期之间的天数
5 12 1949 8 16 1900 (17801)
12 15 1985 3 1 1986 (76)
1 1 1900 7 7 1993 (34155)

## 额外加分

给定一个日历日期和距未来某个事件的天数，确定未来事件的日历日期。

给定任何日历日期，确定其对应的星期几。你可以假设 1900 年 1 月 1 日是星期一。（提示：考虑 mod 7）。

使用以下额外加分测试数据：

### 计算未来日期

| | | | | |
|---|---|---|---|---|
| 5 | 16 | 1947 | 2376 | (11/16/1953) |
| 2 | 12 | 1912 | 6000 | (7/17/1928) |
| 12 | 15 | 1933 | 2345 | (5/17/1940) |

### 计算星期几

| | | | |
|---|---|---|---|
| 12 | 31 | 1900 | (星期一) |
| 4 | 18 | 1977 | (星期一) |
| 8 | 1 | 1932 | (星期一) |
| 11 | 30 | 1947 | (星期日) |
| 12 | 31 | 1986 | (星期三) |
| 12 | 31 | 1988 | (星期六) |

程序输出应发送到终端窗口（您的屏幕）以及请求的 `csis.txt` 输出文件。请务必阅读关于捕获程序输出的文档。您的全名和 Palomar ID 号必须作为注释出现在包含 `main()` 的源文件中。请务必将 `csis.txt` 输出文件包含在 zip 压缩包中。

## 黑杰克实验室

本次作业将侧重于函数的使用和参数传递。你需要构建一个玩简化版黑杰克游戏的 C 程序。规则如下：

- 一局游戏由若干手牌组成，一直玩到牌用完为止。在每手牌中，庄家和玩家都试图累积点数尽可能接近 21 但不超过 21 的牌。

- 首先玩家发一张牌，然后庄家发一张牌，接着玩家发第二张牌，庄家发第二张牌。

- 然后玩家有机会索要更多牌。她的策略是当点数达到 16 点或以上时拒绝要牌（即，她在 15 点或以下时“要牌”）。如果她的点数超过 21，该手牌结束，庄家获胜。

- 如果玩家的点数没有超过 21，庄家索要更多牌。他必须在点数达到 17 或以上时拒绝要牌（即，他在 16 点或以下时“要牌”）。如果他超过 21，玩家赢得该手牌。否则，点数更接近 21 的手牌获胜。平局时，庄家获胜。

- 如果玩家头两张牌是 21 点，她拥有黑杰克并立即赢得该手牌。如果庄家头两张牌是 21 点，该手牌结束，庄家获胜。

- 2 到 10 的牌按面值计算；K、Q、J 计 10 点；A 如果手牌点数大于 10 则计 1 点，否则 A 计 11 点。

- 一副示例牌组可以在 cards.txt 中找到。

黑杰克程序应按以下方式组织：

程序应包含一个名为 playHand() 的函数，它有两个参数：dealerWin 和 ranOut（均为半布尔值）。playHand() 用于玩一手黑杰克，然后如果庄家获胜将 dealerWin 设置为 true (1)，否则设置为 false (0)。main() 函数应反复调用 playHand()，并使用两个变量 dealerTotal 和 playerTotal 跟踪游戏中的总获胜次数。但是，如果 playHand() 牌已用完，应将 ranOut 设置为 true (1)。在这种情况下，程序不应计算这手牌，打印玩家和庄家的总获胜次数，然后退出。

