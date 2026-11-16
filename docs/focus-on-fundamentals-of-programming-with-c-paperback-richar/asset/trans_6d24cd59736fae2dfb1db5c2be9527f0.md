

模块之间的关系可以在结构图中以图形方式显示。例如，假设一家公共图书馆希望计算机化其运营——这是一个相当雄心勃勃的编程项目。将其分解为可管理规模的第一步是基本问题分解：

![](img/0603fdf2eefeabaf26542250cc2fb439_148_0.png)

如果我们有遗漏，随时可以回溯到改进的这一步。我们现在可以进一步深入，细化第一层级的每个子问题：

![](img/0603fdf2eefeabaf26542250cc2fb439_148_1.png)

这对程序员来说仍然太抽象，因此我们再次进行细化：

## 卡片目录

- 将书籍添加到目录
- 从目录中删除书籍
- 搜索书籍

## 图书预订

- 搜索书籍
- 通知借阅者
- 打印预留消息

## 创建新卡片

- 打印卡片表单
- 获取新卡片信息

## 移除过期卡片

- 从永久文件中移除卡片
- 检查未归还书籍
- 通知借阅者

## 替换丢失卡片

- 查找旧卡片信息
- 打印卡片表单

## 活动邮件

- 获取活动信息
- 通知借阅者

## 续借通知

- 获取旧卡片信息
- 通知借阅者

## 逾期图书

- 检查逾期图书
- 计算罚款
- 通知借阅者

请注意，随着问题的部分开始成型为输入/输出函数，细化开始见效。作为额外奖励，这一层级的一些细化（例如“通知借阅者”片段）足够相似，可以编写为单个函数。

整个程序仍然太复杂，无法用 C 语言编码，但部分内容已触手可及：

```c
// library.c
// Reads today's date and books due date. Both must be in the current
// month.

#define FinePerDay 0.25

void calculateFines() {
    float totalFine;
    int todaysDate, dueDate, daysLate;

    printf("Enter todays date and books due date.\n");
    scanf("%d %d", &todaysDate, &dueDate);
    daysLate = todaysDate - dueDate;
    totalFine = daysLate * FinePerDay;
    printf("The total fine is %5.2f", totalFine);
}
```

## 函数作业

1. 为以下每个函数给出函数头。

- a) 函数 areaTriangle 接受两个 double 参数，base 和 height，并返回一个 double 值。
- b) 函数 max 接受四个整数，w、x、y、z，并返回一个整数。
- c) 函数 outputHeaders 不接收任何参数且不返回值。
- d) 函数 getASCII 接受一个字符参数 ch，并返回一个 int。

2. 假设函数 foo() 具有以下定义：

```c
int foo ( int a, int b, int c ) {
... 
}
```

以下哪些语句是合法的？假设 i 的类型为 int，x 的类型为 double。

- a) i = foo (10, 20, 30);
- b) x = foo (10, 20, 30);
- c) i = foo (5.25, 3.45, 7.22);
- d) x = foo (5.25, 3.45, 7.22);
- e) foo (10, 20, 30);
- f) foo (10, 20);

3. 以下哪些是函数的有效原型，该函数不返回任何内容且具有一个 `double` 参数？

- a) `void foo (double x);`
- b) `void foo (double);`
- c) `void foo (x);`
- d) `foo (double x);`

4. 每张 CD 售价 2 美元，每张 DVD 售价 5 美元。编写一个函数，接受两个参数，分别表示 CD 和 DVD 的数量，并返回总美元成本。

## 第 7 章. 选择语句

- if 语句
- switch 语句
- 条件运算符
- 选择作业
- 身体质量指数实验
- 大 – 小实验

## If 语句

决策语句允许程序根据数据值遵循不同的行动方案或执行不同的任务。

### if 语句：单一备选决策语句

以下伪代码语句：

```
if x is not equal to zero then
    divide y by x and assign the result to num
```

可读作如下：

如果条件“x 不等于零”为真，则将 y 的值除以 x 的值，并将结果赋给变量 num。否则，条件“x 不等于零”为假。在这种情况下，不会采取备选操作，因为未指定语句为假时的备选操作。

if 语句的语法如下：

```
if (expression) {
    statement;
}
```

if 语句使用半布尔逻辑，即零表示假，非零表示真。以上述伪代码示例为例，C 代码可能如下所示：

```
if (x != 0) {
    num = y/x;
}
```

以下是一个打印数字绝对值的简短程序：

```c
//absoluteValue.c

int main(void) {
    int num;

    printf("Enter a value: ");
    scanf("%d", &num);
    if (num < 0) {
        num = -num;
    }
    printf("The absolute value is %d\n", num);
    return 0;
}
```

表达式内允许副作用。使用副作用是良好的 C 语言风格，可避免创建否则无用的“临时”变量。因此，

```
if (scanf("%d", &num) != 1) {
    printf("Bad value.\n");
}
```

优于

```
temp = scanf("%d", &num);
if (temp != 1) {
    printf("Bad value.\n");
}
```

由于表达式的结果将是零（假）或非零值，我们将使用：

```
if (expression)
```

而不是

```
if (expression != 0)
```

### if-else 语句：双备选决策语句

以下伪代码示例：

```
if x is not equal to zero then
    divide y by x and assign the result to num
else // otherwise
    display an error message
```

可读作如下：

如果条件“x 不等于零”为真，则将 y 的值除以 x 的值，并将结果赋给变量 num。否则，条件“x 不等于零”为假。在这种情况下，显示一条错误消息。

请注意，上述所示的条件是逻辑表达式。对其求值时，结果要么为真，要么为假。逻辑表达式只有这两个可能的值！

if-else 语句的语法如下：

```
if (expression) {
    statement1;
} else {
    statement2;
}
```

以上述伪代码示例为例，C 代码可能如下所示：

```
if (x != 0) {
    num = y / x;
} else {
    printf ("Divide by zero error condition.");
}
```

以下是一个判断数字是奇数还是偶数的简单程序：

```c
// oddEven1.c
int main(void) {
   int num;
   printf("Enter a number: ");
   scanf("%d", &num);
   if (num % 2 == 0) {
      printf("The number is even.\n");
   }
   else {
      printf("The number is odd.\n");
      return 0;
   }
}
```

请注意，在 C 语言中，控制结构允许的任何位置的语句，都可以是由花括号分隔的复合语句：

```c
// oddEven2.c
int main(void) {
   int num;
   printf("Enter a number: ");
   scanf("%d", &num);
   if (num % 2 == 0) {
      printf("The number entered is %d.\n", num);
      printf("The number is even.\n");
   }
   else {
      printf("The number entered is %d.\n");
      printf("The number is odd.\n");
   }
   return 0;
}
```

以下是一个使用 if-else 结构根据薪资和工作时数计算工资的程序：

```c
// calculateWages.c
// Program to Calculate Wages

#include <stdio.h>

int main (void) {
	float payRate, hours, wages;

	printf("Enter hourly salary: ");
	scanf("%f", &payRate);

	printf("Enter number of hours worked: ");
	scanf("%f", hours);

	if (hours <= 40)
		wages = hours * payRate;
	else
		wages = (40 * payRate) + (hours - 40) * 1.5 * payRate;

	printf("The employee's weekly wages are $%.2f\n", wages);
	return 0;
}
```

### 嵌套 if 语句

每当一个 if 语句嵌套在另一个 if 语句中时，请在嵌套的 if 语句周围加上花括号。此外，else 子句与同一作用域中最近的“未匹配” if 语句相关联：

```c
// nesting1.c

// incorrect nesting
if (num > 0)
	if (num % 2 == 0)
		printf("Positive and even.\n");
else
	printf("Not positive.\n");

// correct nesting
if (num > 0) {
	if (num % 2 == 0)
		printf("Positive and even.\n");
}
else
	printf("Not positive. ");
```

