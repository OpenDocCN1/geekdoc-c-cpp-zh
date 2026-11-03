
```
#define LAMDA 0.001
main()
{
    double t;
    float r;
    int i, R;
    for (i = 1; i<=27; ++i)
    {
        printf("---");
    }
    printf("\n");
    for (t=0; t<=3000; t +=150)
    {
        r = exp(-LAMDA*t);
        R = (int)(50*r+0.5);
        printf("|");
        for (i=1; i<=R; ++i)
        {
            printf("*");
        }
        printf("#\n");
    }
    for (i = 1; i<3; ++i)
    {
        printf("\n");
    }
}
```

# 输出

![](img/65953ea584e494f3d396b2252cb5ea53_136_0.png)

## 图 5.13 绘制可靠性图的程序

程序：图 5.13 给出的程序生成一个阴影图。t 的值由 for 语句自行生成

for (t=0; t<=3000; t +=150)

以 150 为步长。语句中整数 50

```
R = (int)(50*r+0.5)
```

是比例因子，它将 r 转换为用于绘制曲线时使用整数的大值。请记住 r 始终小于 1。

## 复习题和练习

对于问题 5.1 至 5.5 假设程序中已做出以下声明：

```
int    year, count;
float  amount, price;
char   code, city[10];
double root;
```

- **5.1** 说明以下输入语句中是否存在错误。
  - (a) scanf("%c%d%d", city, &price, &year);
  - (b) scanf("%s%d", city, amount);
  - (c) scanf("%f, %d, &amount, &year);
  - (d) scanf("\n%f", root);
  - (e) scanf("%c %d %ld", &code, &count, &root);

- **5.2** 当数据
  1988, x
  作为对以下语句的响应输入时，变量 **year** 和 **code** 中存储的值将是什么：
  - (a) scanf("%d %c", &year, &code);
  - (b) scanf("%c %d", &year, &code);
  - (c) scanf("%d %c", &code, &year);
  - (d) scanf("%s %c", &year, &code);

**5.3** 变量 **count**、**price** 和 **city** 具有以下值：

```
count  ←  1275
price  ← -235.74
city   ← Cambridge
```

显示以下输出语句将产生的确切输出：

- (a) printf("%d %f", count, price);
- (b) printf("%2d\n%f", count, price);
- (c) printf("%d %f", price, count);
- (d) printf("%10dxxxx%5.2f", count, price);
- (e) printf("%s", city);
- (f) printf("%-10d%-15s", count, city);

- **5.4** 说明以下每个输出语句有什么（如果有的话）错误：
  - (a) printf("%d 7.2%f", year, amount);
  - (b) printf("%-s, %c\n", city, code);
  - (c) printf("%f, %d, %s, price, count, city);
  - (d) printf("%c%d%f\n", amount, code, year);

## 5.5

作为对输入语句的响应

```
scanf("%4d %4d", &year, &code, &count);
```

输入以下数据：

19883745

计算机将为变量 year、code 和 count 分配什么值？

## 5.6

给定字符串 "WORDPROCESSING"，编写一个程序从终端读取该字符串并以以下格式显示：

- (a) WORD PROCESSING
- (b) WORD
      PROCESSING
- (c) W.P.

## 5.7

编写一个程序读取 x 和 y 的值并在一行中打印以下表达式的结果：

- (a) (x + y)/(x - y)
- (b) (x + y)/2
- (c) (x + y)(x - y)

## 5.8

编写一个程序读取以下数字，将其四舍五入到最接近的整数并以整数形式打印结果：

35.7   50.21   -23.73   -46.45

## 第 6 章

## 决策与分支

### 6.1 引言

我们已经看到 C 程序是一组语句，通常按其出现的顺序依次执行。这发生在不需要选项或不需要重复某些计算时。然而，在实践中，我们有许多情况可能需要根据某些条件改变语句的执行顺序，或重复一组语句直到满足某些指定条件。这涉及一种决策，以查看特定条件是否已发生，然后指示计算机相应地执行某些语句。

C 语言具有这种决策能力，并支持以下称为 *控制* 或 *决策* 语句的语句。

- 1. if 语句
- 2. switch 语句
- 3. 条件运算符语句
- 4. goto 语句

我们已经在之前的示例中使用了一些这些语句。在这里我们将更详细地讨论它们的功能、能力和应用。

### 6.2 使用 if 语句进行决策

if 语句是一个强大的决策语句，用于控制语句的执行流程。它基本上是一个双向决策语句，并与一个表达式一起使用。其形式如下：

```
if (test expression)
```

它允许计算机首先计算表达式，然后根据表达式（关系或条件）的值是‘真’（非零）还是‘假’（零），将控制转移到特定语句。程序的这一点有两个路径可供选择，一个用于真条件，另一个用于假条件，如图 6.1 所示。

![](img/65953ea584e494f3d396b2252cb5ea53_140_0.png)

图 6.1 双向分支

使用 if 语句进行决策的一些示例是：

- 1. if (银行余额为零)
      借钱
- 2. if (房间黑暗)
      打开灯
- 3. if (代码为 1)
      人是男性
- 4. if (年龄超过 55)
      人已退休

if 语句可以根据要测试的条件复杂程度以不同的形式实现。

- 1. 简单 if 语句
- 2. if .... else 语句
- 3. 嵌套 if .... else 语句
- 4. else if 梯形。

### 6.3 简单 if 语句

简单 if 语句的一般形式是

```
if(test expression)
{
    statement-block;
}
statement-x;
```

'statement-block' 可能是单个语句或一组语句。如果测试表达式为真，则 statement-block 将被执行；否则 statement-block 将被跳过，执行将跳转到 statement-x。请记住，当条件为真时，statement-block 和 statement-x 都将按顺序执行。这在图 6.2 中有所说明。

![](img/65953ea584e494f3d396b2252cb5ea53_141_0.png)

图 6.2 简单 if 控制的流程图

考虑以下用于处理入学考试成绩的程序段。

```
........
if (category == SPORTS)
{
    mark = marks + bonus_marks;
}
printf("%f", marks);
........
```

程序测试学生的类别类型。如果学生属于 SPORTS 类别，则在打印成绩之前会额外加上 bonus_marks。对其他人，不加 bonus_marks。

## 示例 6.1

图 6.3 中的程序从终端读取四个值 a、b、c 和 d，并计算 (a + b) 与 (c − d) 的比率，并在 c − d 不等于零时打印结果。

图 6.3 给出的程序已针对两组数据运行，以查看路径是否正常工作。

第一次运行的结果打印为

Ratio = -3.181818

第二次运行既没有产生任何结果也没有任何消息。在第二次运行期间，(c − d) 的值等于零，因此 statement-block 中包含的语句被跳过。由于 statement-block 后没有其他语句，程序在不产生任何输出的情况下停止。请注意在计算比率的语句中使用 float 转换。这是为了避免由于整数除法而导致的截断。

```
Program
/***********************************************************/
/* ILLUSTRATION OF IF STATEMENT */
/**********************************************************/

main()
{
    int a, b, c, d;
    float ratio;

    printf("Enter four integer values\n");
    scanf("%d %d %d %d", &a, &b, &c, &d);

    if (c-d != 0)
    {
        ratio = (float) (a+b) / (float) (c-d);
        printf("Ratio = %f\n", ratio);
    }
}

Output

Enter four integer values
12  23  34  45
Ratio = -3.181818

Enter four integer values
12  23  34  34
```

图 6.3 简单 if 语句的说明

简单 if 通常用于计数目的。示例 6.2 说明了这一点。

## 示例 6.2

图 6.4 中的程序计算体重小于 50 kg 且身高大于 170 cm 的男孩数量。

程序必须测试两个条件，一个用于体重，另一个用于身高。这是通过复合关系完成的

```
if (weight < 50 && height > 170)
```

这也可以等效地使用两个 if 语句完成，如下所示：

```
if (weight < 50)
    if (height > 170)
        count = count +1;
```

如果体重值小于 50，则执行以下语句，而该语句又是另一个 if 语句。此 if 语句测试身高，如果身高大于 170，则计数加 1。
