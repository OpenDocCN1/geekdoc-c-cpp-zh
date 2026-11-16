
所以在 `main():` 中的调用：

```
foo(&num);
```

我们将 num 的地址传递给函数 foo()。

现在查看函数头中 `foo()` 的形式参数声明。出现在 `num` 前面的 * 表示传递给 `foo()` 的值实际上是内存地址而非数据值。现在如果我们有一个内存地址，并想要实际访问该内存位置中存储的数据值，则必须使用 *间接运算符* (`*`) 来获取它。在函数中每次尝试访问形式参数时，* 都放在形式参数名称之前。

下面是一个通过引用交换两个整数值的程序：

```
// swap.c
#include <stdio.h>
void swap(int *x, int *y);
int main(void) {
    int a, b;
    a = 5;
    b = 9;
    printf("Before swap: a = %d b = %d\n", a, b);
    swap(&a, &b);
    printf("After swap: a = %d b = %d\n", a, b);
    return 0;
}
void swap(int *x, int *y) {
    int temp;
    temp = *x;
    *x = *y;
    *y = temp;
}
```

我们的程序输出如下：

```
Before swap: a = 5   b = 9
After swap: a = 9   b = 5
```

## 通过引用传递和 scanf() 函数

如前所述，scanf() 需要知道要读取的项目的地址。因此变量名前面加上地址运算符 &。但是，如果参数通过引用传递给函数，并且该变量在 scanf() 语句中使用，则无需在变量前面放置地址运算符。这是因为该变量已经表示一个地址，因为它是通过引用传递的。

```
// scanf.c

#include <stdio.h>

void getValue(int *num);

int main(void) {
   int num;

   getValue(&num);
   printf("The value input = %d\n", num);
   return 0;
}

void getValue(int *num) {
   printf("Enter a number: ");
   scanf("%d", num);   // No address-of (&) operator required
}
```

产生的输出如下：

```
Enter a number: 35
The value input = 35
```

## 函数回顾作业

- 编写一个函数 `timeUpdate()`，它接收三个 `int` 参数 `hour`、`min`、`sec`，表示当前时间，并返回更新一秒后的时间。该函数应使用 24 小时制，其中上午 4:30 表示为 4:30，下午 4:30 表示为 16:30。

- 解释以下程序的输出。交换最后 `printf()` 语句中的参数是否会有任何区别？

```
#include <stdio.h>

int main(void)
{
    char a = 127, b = 128;

    printf("%5d %5d %5d\n", a, a + 1, b);
    printf("%5d %5d %5d %5d\n", a, a += 1, b, a);

    return 0;
}
```

输出：
```
127 128 -128
127 -128 -128 -128
```

## 支票账户实验

构建一个 C 程序 check.c，它读取每月支票账户的详细信息并输出汇总这些交易的银行对账单。输入文件 account.txt 包含一个月支票账户的交易列表。输入文件的每一行包含一个单字符交易代码以及一个 double 类型的交易金额。有效的交易代码如下：

- I 从上个月结转的初始余额
- D 存款
- C 支票

输入每笔交易时，应在单行上输出交易类型、交易金额（存款和支票分列）以及处理交易后的余额：

| 交易 | 存款 | 支票 | 余额 |
|---|---|---|---|
| 初始余额 | | | 478.83 |
| 存款 | 127.45 | | 606.28 |
| 存款 | 619.84 | | 1226.12 |
| 支票 | | 945.12 | 281.00 |
| 支票 | | 4.76 | 276.24 |
| ... | | | |

银行的服务费（应在月底从余额中扣除）如下：

- 每月账户维护费 $3.00。
- 每张兑现的支票 $0.06。
- 每笔存款 $0.03。
- 每当兑现的支票使余额低于 $0.00 时，透支费 $5.00。

注意：当交易是存入透支账户但未使余额高于零时，不收取透支服务费。

银行对账单还应包含以下汇总信息：

- 存款总笔数：
- 存款总金额：
- 支票总笔数：
- 支票总金额：
- 服务费总额：
- 期初余额：
- 期末余额：

下面是你程序中应使用的 main() 函数。请勿修改 main() 函数。

```
int main(void) {
	char code;
	double amount, service, balance;
	double amtCheck, amtDeposit, openBalance, closeBalance;
	int numCheck, numDeposit;

	if (!(fpIn = fopen("account.txt", "r"))) {
		printf("account.txt could not be opened for input.");
		exit(1);
	}
	if (!(fpOut = fopen("csis.txt", "w"))) {
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
	while (!feof(fpIn)) {
		fscanf(fpIn, "%c %lf", &code, &amount);
		if (code == 'I') {
			initialBalance(amount, &balance, &service, &openBalance);
		} else if (code == 'D') {
			deposit(amount, &balance, &service, &numDeposit,
				&amtDeposit);
		} else {
			check(amount, &balance, &service, &numCheck, &amtCheck);
		}
	}
	closeBalance = balance - service;
	outputSummary(numDeposit, amtDeposit, numCheck, amtCheck,
		openBalance, service, closeBalance);
	fclose(fpIn);
	fclose(fpOut);
	return 0;
}
```

你需要为程序编写五个函数（及其原型）：

- outputHeaders()
- initialBalance()
- deposit()
- check()
- outputSummary()

这些函数将使用计数器和求和来跟踪支票账户的不同组成部分，并输出与银行对账单相关的特定信息。请注意，某些函数参数作为输入参数传递，某些作为输入-输出参数传递。请务必在函数中正确使用间接运算符 (*)。

请记住，main() 函数应作为程序中的第一个函数出现。请务必为程序中使用的每个函数使用函数原型。

account.txt 的内容如下：

| 类型 | 值 |
| :--- | :--- |
| I | 478.83 |
| D | 127.45 |
| D | 619.84 |
| C | 945.12 |
| C | 4.76 |
| D | 32.81 |
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

在程序中，除了文件指针的声明外，不应使用任何全局变量。全局变量是在 main() 之外声明的变量。

程序的输出应发送到终端窗口（您的屏幕）以及请求的 csis.txt 输出文件。请务必阅读关于捕获程序输出的文档。您的全名和 Palomar ID 号必须作为注释出现在包含 main() 的源文件中。请务必将 csis.txt 输出文件包含在 zip 压缩包中。

你应至少为程序创建以下函数：

## 日期实验

本次作业将重点介绍函数的使用和参数传递。你需要构建一个 C 程序 `date.c`，执行以下每项操作：

- 将日历日期转换为儒略日期
- 将儒略日期转换为日历日期。
- 计算任意两个日历日期之间的天数。

日历日期只是包含年、月、日的日期，而儒略日期是 1 到 366 之间（包含 1 和 366）的整数，表示从当年的 1 月 1 日起经过的天数（包括计算日期的那一天）。例如，日历日期 4/12/2008 相当于儒略日期 103，2008。

你的程序应包含一个选择菜单（_提示：考虑 do-while 循环_），允许用户选择一个选项。示例如下：

```
DATE SELECTION MENU

1) Convert calendar date into Julian date
2) Convert Julian date into calendar date
3) Compute days between two calendar dates
4) Exit program

ENTER SELECTION (1 - 4):
```

请确保你的程序为每个必需的操作包含单独的函数，并根据需要传递参数。请记住，除了文件指针外，程序中不允许使用全局变量。你应至少为程序创建以下函数：
