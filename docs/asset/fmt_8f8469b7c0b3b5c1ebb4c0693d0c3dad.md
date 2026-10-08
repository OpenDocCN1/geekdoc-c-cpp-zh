
```
$b \times (1 + \frac{r}{100})^n$
```

变为

```
b * Math.pow(1 + r / 100, n)
```

图 3 显示了如何分析一个表达式。表 6 显示了额外的数学方法。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_78_0.png)

图 3

分析表达式

| 表 6 数学方法 |  |
| --- | --- |
| `Math.sqrt(x)` | $x$ 的平方根 ($x \ge 0$) |
| `Math.pow(x, y)` | $x^y$ ($x>0$，或 $x=0$ 且 $y>0$，或 $x<0$ 且 $y$ 为整数） |
| `Math.sin(x)` | $x$ 的正弦（x 为弧度） |
| `Math.cos(x)` | $x$ 的余弦 |
| `Math.tan(x)` | $x$ 的正切 |
| `Math.toRadians(x)` | 将角度转换为弧度（即返回 $x \cdot \pi/180$） |
| `Math.toDegrees(x)` | 将弧度转换为角度（即返回 $x \cdot 180/\pi$） |
| `Math.exp(x)` | $e^x$ |
| `Math.log(x)` | 自然对数 (ln(x)$,$x>0$) |
| `Math.log10(x)` | 十对数 (log10(x), x > 0) |
| `Math.round(x)` | 接近 x 的整数（作为 long） |
| `Math.abs(x)` | 绝对值 $|x|$ |
| `Math.max(x, y)` | $x$ 和 $y$ 中的较大值 |
| `Math.min(x, y)` | $x$ 和 $y$ 中的较小值 |

### 2.2.5 将浮点数转换为整数

偶尔，你有一个 `double` 类型的值，并需要将其转换为 `int` 类型。将浮点值赋值给整数是错误的：

```
double balance = total + tax;
int dollars = balance; // 错误：无法将 double 赋值给 int
```

编译器不允许这种赋值，因为它是潜在危险的：

- 小数部分会丢失。
- 数量级可能太大。（最大的整数大约是 20 亿，但浮点数可以大得多。）

你必须使用强制转换运算符 `(int)` 将浮点值转换为整数。在你想要转换的表达式之前写上转换运算符：

```
double balance = total + tax;
int dollars = (int) balance;
```

强制转换 `(int)` 通过丢弃小数部分将浮点值 `balance` 转换为整数。例如，如果 `balance` 是 13.75，那么 `dollars` 被设置为 13。对算术表达式应用强制转换运算符，需要将表达式放在括号内：

```
dollars = (int) (total + tax);
```

#### 语法 2.4 强制转换

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_79_0.png)

丢弃小数部分并不总是合适的。如果你想将浮点数四舍五入到最近整数，请使用 `Math.round` 方法。该方法返回一个 `long` 整数，因为大的浮点数无法存储在 `int` 中。

- `long rounded = Math.round(balance);`
- 如果 `balance` 是 13.75，则 `rounded` 被设置为 14。
- 如果你知道结果可以存储在 `int` 中而不需要 `long`，可以使用：
  `int rounded = (int) Math.round(balance);`

### 表 7 算术表达式

| 数学表达式 | Java 表达式 | 注 |
| --- | --- | --- |
| $x + y$ | `(x + y) / 2` | 必须使用括号；$x+y/2$ |
| $xy$ | `x * y / 2` | 不需要括号；相同优先级的运算符从左到右求值 |
| $(x+r)^n$ | `Math.pow(x + r, n)` | 使用 `Math.pow(x, n)` 计算 $x^n$ |
| $\sqrt{a^2+b^2}$ | `Math.sqrt(a * a + b)` | $a * a$ 比 `Math.pow(a, 2)` 更简单 |
| $i + j + k$ | `(i + j + k) / 3.0` | 如果 $i, j,$ 和 $k$ 是整数，使用 3.0 作为分母将强制进行浮点除法 |
| $\pi$ | `Math.PI` | Math.PI 是 Math 类中的常量 |

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_80_0.png)

10. 一个银行账户每年产生利息。在 Java 中，如何计算第一年的利息？假设已声明 `double` 类型变量 `balance`。

11. 在 Java 中，如何计算存储在变量 `area` 中的正方形边长？

12. 球的体积由 $V = \frac{4}{3}\pi r^3$给出。如果半径由 `double` 类型变量给出，写出体积的 Java 表达式。

13. $1729 / 10$ 的值是多少？

14. 如果 $n$ 是正数，$n / 10$ 是多少？

现在你可以在章节末尝试这些练习：R2.3, R2.5, P2.4, P2.2。

#### 意外整数除法

遗憾的是，Java 使用相同的符号 `/` 同时用于整数除法和浮点除法。这些是两种完全不同的操作。误用整数除法是一个常见错误。考虑以下计算三个整数平均值的代码段：

```
int score1 = 10;
int score2 = 4;
int score3 = 9;

double average = (score1 + score2 + score3) / 3;
System.out.println("Average: " + average); // 输出 7.0，而不是 7.6666666666667
```

这有什么问题？当然，`score1, score2` 和 `score3` 的平均值应该是：

```
(score1+score2+score3)/3
```

在这里，由于 `score1 + score2 + score3` 都是整数且和为 23，23 除以 3 的结果是 7。然后这个整数 7 被移动到浮点变量 `average` 中。解决方法是让分子或分母变为浮点数：

```
double total = score1 + score2 + score3;
double average = total / 3;
```

或者

```
double average = (score1 + score2 + score3) / 3.0;
```

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_81_0.png)

#### 括号不匹配

考虑表达式

```
(a + b) / 2 * (1 - t)
```

它有什么问题？数一下括号。有三个 `(` 和两个 `)`。括号不匹配。这种写法在复杂的表达式中很常见。现在这个表达式：

```
(a + b) * (2 * (1 - t))
```

这个表达式有三个 `(` 和两个 `)`，但它是错误的。在表达式中间，`(` 的计数只有一个两个 `)`，这是错误的。`(` 的计数必须大于等于 `)` 的计数，在表达式结束时两个计数必须相等。

这里有一个不用纸笔计数的简单技巧。大脑很难同时保持两个计数。扫描表达式时只保留一个计数。从第一个左括号开始为 1，每遇到一个左括号加 1，每遇到一个右括号减 1。当你扫描表达式：

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_81_1.png)

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_81_2.png)

时，如果计数降降为零，或者在结束时不为零，则括号不匹配。例如，当扫描表达式时，你会念道：

```
(a + b) / 2 * (1 - t))
     1      -1
```

#### 编程提示 2.3

##### 表达式中的空格

以下代码比以下代码更容易读：

```
x1 = (-b + Math.sqrt(b*b - 4*c)) / (2 * a);
```

```
x1=(-b+Math.sqrt(b*b-4*c))/(2*a);
```

在所有运算符 `+ - * %` 周围加上空格即可。但是，不要在一元减号后加空格：用于否定单个数量，例如 `-b`。这样就可以很容易区别于二元减号，如 `-a - b`。习惯上不在方法名后加空格。即使用 `Math.sqrt(x)` 而不是 `Math.sqrt (x)`。

#### 特殊主题 2.3

##### 赋值与算术结合

在 Java 中，你可以结合算术和赋值。例如，指令

```
total += cans;
```

是 `total = total + cans;` 的简写。

同样，

```
total *= 2;
```

是编写 `total = total * 2;` 的另一种方式。

许多程序员发现这是一个方便的简写。如果你喜欢它，尽管在你的代码中使用它吧。尽管为了简单起见，我们在本书中不会使用它。

#### 视频示例 2.1

##### 使用整数除法

果汁配方需要一定量的橙子汽。在视频示例中，你将看到如何使用整数除法计算所需的 12 盎司罐数。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_82_1.png)

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_82_2.png)

在线可在 WileyPLUS 和 www.wiley.com/college/horstmann 获取。

如果你要求程序提供输入而不是使用固定值，就可以让你的程序更具活性。例如，考虑一个处理苏打水容器价格和数量的程序。价格和数量可能会波动。程序用户应该将它们作为输入。

## 2.3 输入与输出

当程序请求输入时，它应该首先打印一条消息，告诉用户期望输入什么内容。这样的消息被称为提示（prompt）。

```
System.out.print("Please enter the number of bottles:"); // 显示提示
```

使用 `print` 方法来显示输入。你希望输入出现在冒号后面，而不是在下一行。还要记住在冒号后留一个空格。

由于输出被发送到 `System.out`，你可能会认为你使用 `System.in` 进行输入。遗憾的是，情况并非完全如此。在 Java 最初设计时，人们并没有很关注读取键盘输入。他们假设所有程序员都会生成带有文本字段和菜单的图形用户界面。`System` 设计时包含了一组最少的功能，必须与其他类结合才能有用。

要读取输入，你使用 `Scanner` 类。你通过以下语句获取一个 `Scanner` 对象：

```
Scanner in = new Scanner(System.in);
```

你将在第 8 章中学习更多关于对象和类的知识。现在当你需要读取键盘输入时，只需包含该语句即可。

使用 scanner 时，你需要执行另一个步骤：从它的包（package）导入该类。包是具有相关用途的类的集合。Java 库中的所有类都包含包中。`System` 属于 `java.lang` 包。`Scanner` 属于 `java.util` 包。

只有 `java.lang` 包中的类在程序中是自动可用的。否则，请在程序文件的顶部放置以下声明：

```
import java.util.Scanner;
```

一旦你有了 scanner，你就可以使用它的 `nextInt` 方法来读取一个整数值：

```
System.out.print("Please enter the number of bottles:");
int bottles = in.nextInt();
```

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_84_0.png)

Java 类被分组在包中。使用 `import` 语句来使用包中的类。

## 2.5 输入语句

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_84_1.png)

当调用 `nextMethod` 时，程序会等待用户输入一个数字并按下回车键。在用户提供输入后，该数字被放入 `bottle` 变量中，程序继续执行。

要读取浮点数，请使用 `nextDouble` 代替：

使用 `Scanner` 类在控制台窗口中读取键盘输入。

```
System.out.print("Enter price: ");
double price = in.nextDouble();
```

### 2.3.2 格式化输出

当你打印计算结果时，你通常希望控制它的外观。例如，当你打印以美元和分数的金额时，你通常希望它保留两位有效数字。也就是说，当你希望输出看起来像这样：

Price per liter: 1.22

Price per liter: 1.2159624131455

以下命令显示小数点后两位数字的价格：

使用 `printf` 方法来指定应该如何格式化值。

```
System.out.printf("%.2f", price);
```

你也可以指定字段宽度：

```
System.out.printf("%-10.2f", price);
```

价格使用十个字符打印：六个空格，后跟四个字符 `1.22`。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_85_0.png)

`%10.2f` 被称为格式说明符（format specifier）：它描述了如何格式化值。格式说明符末的字母 `f` 表示我们正在显示一个浮点数。使用 `d` 表示整数，使用 `s` 表示字符串；示例见表 8。

## 表 8 格式说明符示例

| 格式字符串 | 示例输出 | 注释 |
|---|---|---|
| "%d" | 24 | 配合整数使用 `d`。 |
| "%5d" | 24 | 添加空格使字段宽度为 5。 |
| "Quantity:%5d" | 24 | 格式字符串内部但格式说明符外部的字符会出现在输出中。 |
| "%f" | 1.21997 | 配合浮点数使用 `f`。 |
| "%.2f" | 1.22 | 打印小数点后两位数字。 |
| "%7.2f" | 1.22 | 添加空格使字段宽度为 7。 |
| "%s" | Hello | 配合字符串使用 `s`。 |
| "%d %.2f" | 24 1.22 | 你可以同时格式化多个值。 |

你使用 `printf` 方法将输出对齐成整齐的列。

| 命令 | 月 | 几 | 年 | 总计 |
|---|---|---|---|---|
| %s | June 4 | 10 | 2005 | $100 |
| %s | July 21 | 12 | 2004 | $214 |
| %s | Aug 14 | 15 | 2003 | $225 |
| %s | Oct 20 | 25 | 2002 | $500 |
| %s | Nov 15 | 14 | 2001 | $210 |
| %s | May 22 | 14 | 2000 | $294 |
| %s | Mar 31 | 25 | 1999 | $625 |
| %s | Jan 18 | 28 | 1998 | $784 |

格式字符串包含格式说明符和字面字符。任何不是格式说明符的字符都会被原样打印。例如：

```
System.out.printf("Price per liter:%10.2f", price);
```

Price per liter: 1.22

你可以通过单次调用 `printf` 方法打印多个值。这里有一个典型的示例：

```
System.out.printf("Quantity: %d Total:%10.2f", quantity, total);
```

| Quantity: | 24 | Total: | 17 |
|---|---|---|---|

一个格式字符串包含格式说明符和字面字符。任何不是格式说明符的字符都会被原样打印。例如，这个

```
System.out.printf("Price per liter:%10.2f", price);
```

Price per liter: 1.22

你可以通过单次调用 `printf` 方法打印多个值。这里有一个典型的示例：

```
System.out.printf("Quantity: %d Total:%10.2f", quantity, total);
```

| Quantity: | 24 | Total: | 17 |
|---|---|---|---|

一个格式字符串包含格式说明符和字面字符。任何不是格式说明符的字符都会被原样打印。例如，这个

```
System.out.printf("Price per liter:%10.2f", price);
```

Price per liter: 1.22

你可以通过单次调用 `printf` 方法打印多个值。这里有一个典型的示例：

```
System.out.printf("Quantity: %d Total:%10.2f", quantity, total);
```

| Quantity: | 24 | Total: | 17 |
|---|---|---|---|

一个格式字符串包含格式说明符和字面字符。任何不是格式说明符的字符都会被原样打印。例如，这个

```
System.out.printf("Price per liter:%10.2f", price);
```

Price per liter: 1.22

你可以通过单次调用 `printf` 方法打印多个值。这里有一个典型的示例：

```
System.out.printf("Quantity: %d Total:%10.2f", quantity, total);
```
