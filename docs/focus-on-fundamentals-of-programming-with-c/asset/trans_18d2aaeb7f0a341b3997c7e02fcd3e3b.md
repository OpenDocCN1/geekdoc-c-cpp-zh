

## while 循环的语法如下：

```
// Before the loop construct, initialize any loop control variable,
// i.e., the variable appearing in the condition in the loop header.
while (condition) { // loop header - test the loop condition
    statement;
}
or
while (condition) { // loop header - test the loop condition
    statement;
    statement;
    ...
}
```

请记住，循环体必须包含一条用于更新循环条件中所用循环控制变量的语句。循环控制变量通常位于循环体的底部。

请注意，当 while 循环结构只有一条语句时，花括号 { } 是可选的。但是，即使不是必须的，使用花括号始终是个好主意。

## 示例：2 的幂

举个例子，假设有一个程序段旨在找出大于 100 的第一个 2 的幂。我们首先将整型变量 product 初始化为 2。当以下 while 重复语句执行完毕后，product 将包含所需的答案：

```
product = 2;
while (product <= 100) {
    product = product * 2; // or we can say: product *= 2;
}
```

进入 while 语句时，product 的值为 2。变量 product 反复乘以 2，依次取值 2、4、8、16、32、64 和 128。当 product 变为 128 时，while 语句中的条件：

```
product <= 100
```

变为假。这终止了重复，product 的最终值为 128。程序执行继续在 while 循环之后的下一条语句处进行。

我们可以将此示例推广，编写一个名为 findMax() 的函数，它将返回大于某个最大值的第一个 2 的幂：

```
#include <stdio.h>

int findMax(int value);

int main (void) {
    int value, max;

    value = 500;
    max = findMax(value); ...
    printf("The first power of 2 larger than %d is %d.", value, max);
    return 0;
}

int findMax(int value) {
    int product = 2;

    while (product <= value) {
        product *= 2;
    }
    return product;
}
```

其输出如下：

```
The first power of 2 larger than 500 is 512.
```

我们可以进一步推广此示例，使函数 findMax() 返回大于某个最大值的第一个 num 的幂：

```
#include <stdio.h>

int findMax(int product, int value);

int main (void) {
    int num, value, max;

    num = 5;
    value = 1000;

    max = findMax(num, value);
    printf("The first power of %d larger than %d is %d.", num,
           value, max);

    return 0;
}

int findMax(int product, int value) {
    while (product <= value) {
        product *= 2;
    }
    return product;
}
```

其输出如下：

```
The first power of 5 larger than 1000 is 1280.
```

## 计数器控制循环

计数器控制循环使用一个变量来统计已完成的循环迭代次数，从而重复执行一系列可执行语句指定的次数。

- 循环体重复的次数必须在第一次检查循环条件之前已知，且在循环体内不得更改。
- 计数变量必须在第一次检查循环条件之前初始化为已知值。
- 计数变量必须在循环体内更新，否则循环条件永远不会评估为假，从而创建一个永远不会停止的无限循环。
- 计数变量可以以任意量递增（值增加）或递减（值减少）。

## 示例：摄氏度到华氏度转换表

我们的转换表将使用一个计数器变量 ctemp 来控制 while 循环执行的次数。在此示例中，当 ctemp 变为 < 0 时，重复终止。

```c
#include <stdio.h>
int main (void) {
    int ctemp;
    float ftemp;
    printf("Celsius\t\tFahrenheit\n");
    ctemp = 100;
    while (ctemp >= 0) {
        ftemp = (9.0/5.0) * (float)ctemp + 32.0;
        printf ("%7d%15.1f\n", ctemp, ftemp);
        ctemp = ctemp - 10;
    }
    return 0;
}
```

程序输出如下：

| 摄氏度 | 华氏度 |
|---|---|
| 100 | 212.0 |
| 90 | 194.0 |
| 80 | 176.0 |
| 70 | 158.0 |
| 60 | 140.0 |
| 50 | 122.0 |
| 40 | 104.0 |
| 30 | 86.0 |
| 20 | 68.0 |
| 10 | 50.0 |
| 0 | 32.0 |

- 如果我们写 (9/5) 而不是 (9.0/5.0) 会发生什么？
- 如果我们去掉 (9.0/5.0) 两边的括号会发生什么？
- 为什么在上述表达式中写 `(float)ctemp` 而不是仅写 `ctemp` 是个好主意？

## 求和变量

假设我们希望求 1 到 1000 的数之和。我们不仅需要一个计数器变量来控制 while 循环执行的次数，还需要一个求和变量来累加目前为止所见数字的总和。

```
// summation.c

#include <stdio.h>

int main(void) {
    int count = 1;
    int sum = 0;

    while (count <= 1000) {
        sum += count;
        ++count;
    }

    printf("The sum = %d.\n", sum);
    return 0;
}
```

程序输出如下：

The sum = 500500.

请注意，用于存储求和或总计的变量通常应在程序中使用前初始化为零；否则，求和变量将包含其内存位置中先前存储的值。这是因为未初始化的变量通常包含“垃圾值”，即该变量保留内存位置中最后存储的值。

## 哨兵控制循环

有时我们事先不知道希望循环迭代多少次。例如，假设我们想要输出程序中输入数字的平方和立方。程序如何确定何时停止数字输入？解决此问题的一种方法是使用一个称为哨兵值的特殊值来指示“数据输入结束”。

用户输入数据值，程序将输出其平方和立方，直到输入哨兵值，这表示最后一个数据值已被输入。请注意，哨兵值的选择必须使其不会与可接受的输入值混淆。

```
// sentinel.c
#include <stdio.h>
int main(void) {
    int num;
    printf("Enter number, -999 to end: ");
    scanf("%d", &num);
    while (num != -999) {
        printf("%5d %5d %5d\n", num, num * num, num * num * num);
        printf("Enter number: ");
        scanf("%d", &num);
    }
    return 0;
}
```

程序输出如下：

```
Enter number, -999 to end: 2
2    4    8
Enter number, -999 to end: 5
5   25  125
Enter number, -999 to end: 8
8   64  512
Enter number, -999 to end: -999
```

## for 语句

for 语句适用于在进入循环之前已知循环迭代次数的情况。循环头由三个部分组成，用分号分隔：初始化、测试和更新。

```
for (i = 1; i <= 100; i++)
```

第一部分在进入循环之前运行。这通常是循环控制变量的初始化。

第二部分是对循环控制变量的测试。当此测试不再为真时，退出循环。

第三部分是循环控制变量的更新。这通常是在循环体完成后每次执行的语句。通常这是对循环控制变量的递增或递减。

以下是 for 语句的语法：

```
for (initialExpression; loopCondition; loopExpression) {
    statement;
}
```

- initialExpression 在循环开始前设置初始值。
- loopCondition 指定继续循环所需的条件。
- loopExpression 在循环体执行后每次执行。

## 示例：求 1 到 100 的整数和

```
int i, sum = 0;
for (i = 1; i <= 100; ++i) {
    sum += i;
}
```

