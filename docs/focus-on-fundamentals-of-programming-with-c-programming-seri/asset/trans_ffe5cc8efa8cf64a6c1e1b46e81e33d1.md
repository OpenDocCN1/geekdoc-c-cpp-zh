

- 计数变量必须在循环体内更新，否则循环条件永远不会求值为 false，从而创建一个永远不会停止的无限循环。
- 计数变量可以以任意量递增（值增加）或以任意量递减（值减少）。

## 示例：摄氏度转华氏度转换表

我们的转换表将使用计数器变量 ctemp 来控制 while 循环执行的次数。在此示例中，当 ctemp 变为 < 0 时，重复终止。

```c
// tempConversion.c
#include <stdio.h>
int main(void) {
    int ctemp;
    float ftemp;
    printf("Celsius\tFahrenheit\n");
    ctemp = 100;
    while (ctemp >= 0) {
        ftemp = (9.0/5.0) * (float)ctemp + 32.0;
        printf ("%7d\t%10.1f\n", ctemp, ftemp);
        ctemp -= 10;
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
- 在上述表达式中写 (float)ctemp 而不是仅写 ctemp 是个好主意，这是为什么呢？

## 求和变量

假设我们希望求 1-1000 的数字之和。我们不仅需要一个计数器变量来控制 while 循环执行的次数，还需要一个求和变量来累加我们迄今所见数字的总和。

```c
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

总和 = 500500。

注意，用于存储求和或总计的变量，通常应在程序中使用前初始化为零；否则，求和变量将包含存储在求和变量内存位置中的先前值。这是因为未初始化的变量通常包含“垃圾值”，即最后存储在为该变量保留的内存位置中的值。

## 哨兵控制循环

有时我们事先不知道希望循环迭代多少次。例如，假设我们想要输出程序中输入的数字的平方和立方。程序如何确定何时停止数字输入？解决此问题的一种方法是使用一种称为哨兵值的特殊值来指示“数据输入结束”。

用户输入数据值，其平方和立方将被输出，直到输入哨兵值，这表示最后一个数据值已被输入。请注意，哨兵值的选择必须使其不会与可接受的输入值混淆。

```c
// sentinel.c

#include <stdio.h>

int main(void) {
    int num;

    printf("Enter number, -999 to end: ");
    scanf_s("%d", &num);
    while (num != -999) {
        printf("%5d %5d %5d\n", num, num * num, num * num * num);
        printf("Enter number: ");
        scanf_s("%d", &num);
    }
    return 0;
}
```

程序输出如下：

```
Enter number, -999 to end: 2
2 4 8
Enter number, -999 to end: 5
5 25 125
Enter number, -999 to end: 8
8 64 512
Enter number, -999 to end: -999
```

## for 语句

for 语句在进入循环之前已知循环迭代次数时效果很好。循环头由分号分隔的三部分组成：初始化、测试和更新。

```
for (i = 1; i <= 10; i++)
```

第一部分在进入循环之前运行。这通常是循环控制变量的 *初始化*。

第二部分是对循环控制变量的 *测试*。当此测试不再为真时，循环退出。

第三部分是循环控制变量的 *更新*。这通常是循环体完成后每次执行的语句。通常这是对循环控制变量的递增或递减。

以下是 *for* 语句的语法：

```c
for (initialExpression; loopCondition; loopExpression) {
    statement;
}
```

- initialExpression 在循环开始前设置初始值。
- loopCondition 指定继续循环所需的条件。
- loopExpression 在循环体执行后每次执行。

## 示例：求 1 到 100 的整数之和

```c
// sumIntegers1.c
int i, sum = 0;
for (i = 1; i <= 100; ++i) {
    sum += i;
}
```

在我们的示例中，变量 i 是循环控制变量，并初始化为 1。如果 loopCondition 为真，即 i <= 100，则循环体将执行一次。在循环体的最后一条语句执行后，将执行 loopExpression。在此示例中，i 的值将递增 1。如果 loopCondition 仍为真，则 for 循环体将再次执行，以此类推。

请注意，for 语句中的任何或所有表达式都可以缺失，但两个分号必须始终保留。例如，如果 initialExpression 缺失，则作为 for 循环的一部分不会执行任何初始化步骤：

```c
// sumIntegers2.c
// Compute the sum of integers from 1 - 10.
int i = 1, sum = 0;
for ( ; i <= 10; ++i) {
    sum += i;
}
```

当 loopCondition 缺失时，规则是测试始终为真。因此，下面的 for 循环是一个无限循环。

```c
// sumIntegers3.c
int i = 1, sum = 0;
for ( ; ; ) {
    sum += i++;
    printf("%d ", sum);
}
```

请注意，`for` 语句始终可以翻译为等效的 `while` 语句，反之亦然：

```c
// for loop
for (initialExpression; loopCondition; loopExpression) {
    statement;
}

// while loop
initialExpression;
while (loopCondition) {
    statement;
    loopExpression;
}
```

请务必不要在 for 循环标题末尾放置分号：

```c
// sumIntegers4.c
int i, sum = 0;
for (i = 1; i <= 100; ++i);
    sum += i;
```

这会造成问题，因为 `for` 循环将不再有循环体。在这种情况下，循环的控制方面将执行 100 次，但什么都不会做，因为循环体为空。

请注意，当 `for` 循环结构只有一条语句时，花括号 {} 是可选的。但是，即使不是必需的，使用花括号始终是个好主意。

## 嵌套 for 循环

有时我们需要将一个 `for` 循环放在另一个 `for` 循环的循环体中。这被称为嵌套 `for` 循环。你能跟踪下面嵌套 `for` 循环的控制流程吗：

```c
// nest.c
#include <stdio.h>
int main(void) {
    int i, j;
    for (i = 1; i <= 4; ++i) {
        for (j = 1; j <= 3; ++j) {
            printf("%d %d\n", i, j);
        }
    }
    return 0;
}
```

以下是生成的输出：

```
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
4 1
4 2
4 3
```

## 逗号运算符

偶尔，你会发现自己处于这样的情况：C 期望一个单一表达式，但你有两件事想要表达。最常见的（实际上也是唯一常见的）示例是在 `for` 循环中，具体来说是第一个和第三个控制表达式。例如，如果你希望有一个循环，其中 `i` 从 0 递增到 10，同时 `j` 从 10 递减到 0，你可以在循环标题中操纵 `i`，并“手动”处理 `j`：

```c
// comma1.c
...
j = 10;
for(i = 0; i < 10; i++) {
    ... rest of loop ...
    j--;
}
```

但在这里，更难看出 `i` 和 `j` 的并行性质，而且如果循环包含 `continue` 语句，这也无法正常工作。（`continue` 会跳回循环顶部，`i` 将被递增，但 `j` 将 _不会_ 被递减。）你可以根据 `i` 计算 `j`：

```c
// comma2.c
...
for(i = 0; i < 10; i++) {
    j = 10 - i;
    ... rest of loop ...
}
```

但这也使 `j` 不必要地从属。在 C 中编写此循环的通常方式是：

```c
// comma3.c
...
for(i = 0, j = 10; i < 10; i++, j--) {
    ... rest of loop ...
}
```

