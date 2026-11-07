
- c) 当 do...while 终止时，执行继续进行 while 子句之后的语句。
- d) 以上所有陈述都是正确的。

Answer: a) 是错误的。实际上，如果 while 语句的循环继续测试在进入循环时失败，循环的主体将不会执行。

2 (True/False) 假设 counter 初始化为 1，以下循环显示数字 1 到 10：

```
do {
    printf("%d ", counter);
} while (++counter < 10);
```

Answer: False. 该循环显示数字 1 到 9。要显示数字 1 到 10，请将循环继续条件中的 < 更改为 <=。

## 4.8 break 和 continue 语句

break 和 continue 语句用于改变控制流。第 4.6 节展示了在 switch 语句中遇到的 break 会终止 switch 的执行。本节讨论如何在迭代语句中使用 break。

### break 语句

break 语句在 while、for、do...while 或 switch 语句中执行时，会导致立即退出该语句。程序执行继续执行该 while、for、do...while 或 switch 之后的那条语句。break 的常见用途是提前从循环中退出或跳过 switch 的剩余部分（如图 4.5 所示）。图 4.7 演示了 for 迭代语句中第 12 行的 break 语句。

```
1  // fig04_07.c
2  // Using the break statement in a for statement.
3  #include <stdio.h>
4
5  int main(void) {
6      int x = 1;  // declared here so it can be used after loop
7
8      // loop 10 times
9      for (; x <= 10; ++x) {
10         // if x is 5, terminate loop
11         if (x == 5) {
12             break; // break loop only if x is 5
13         }
14
15         printf("%d ", x);
16     }
17
18     printf("\nBroke out of loop at x == %d\n", x);
19 }
```

Fig. 4.7 | 在 for 语句中使用 break 语句。(第 1 部分，共 2 部分。)

```
1 2 3 4
Broke out of loop at x == 5
```

**Fig. 4.7** | 使用 `break` 语句在 `for` 语句中。(第 2 部分，共 2 部分。)

当 `if` 语句检测到 x 变为 5 时，`break` 执行。这终止了 `for` 语句，程序继续执行 `for` 之后的 `printf`。循环仅完全执行四次。请记住，当你在 `for` 循环的 *初始化表达式* 中声明控制变量时，循环终止后该变量不再存在。我们在本例中在循环之前声明并初始化了 x，以便在循环终止后使用其最终值。因此，`for` 头部的初始化部分（第一个分号之前）为空。

### continue 语句

`continue` 语句在 `while`、`for` 或 `do...while` 语句中执行时，会跳过该控制语句主体中的剩余语句并执行循环的下一次迭代。在 `while` 和 `do...while` 语句中，循环继续条件会在 `continue` 语句执行后立即求值。在 `for` 语句中，先执行增量表达式，然后求值循环继续条件。图 4.8 在 `for` 语句中使用 `continue`（第 10 行）在 x 为 5 时跳过 `printf` 语句并开始循环的下一次迭代。

```
1  // fig04_08.c
2  // Using the continue statement in a for statement.
3  #include <stdio.h>
4
5  int main(void) {
6     // loop 10 times
7     for (int x = 1; x <= 10; ++x) {
8        // if x is 5, continue with next iteration of loop
9        if (x == 5) {
10          continue; // skip remaining code in loop body
11       }
12
13       printf("%d ", x);
14    }
15
16    puts("\nUsed continue to skip printing the value 5");
17 }
```

```
1 2 3 4 6 7 8 9 10
Used continue to skip printing the value 5
```

**Fig. 4.8** | 在 `for` 语句中使用 `continue` 语句。

### break 和 continue 注释

一些程序员认为 `break` 和 `continue` 违反了结构化编程的规范，因此不使用它们。这些语句的效果可以通过我们即将讨论的结构化编程技术来实现，但 break 和 continue 语句执行速度更快。

在实现高质量软件工程和实现性能最佳的软件之间存在矛盾——一个是以另一个为代价实现的。对于除最注重性能的情况以外的所有情况，请遵循以下准则：首先使代码简单且正确，然后再使其快速且精简，但仅在必要时。

### 自检

- 1. *(Multiple Choice)* 以下 a)、b) 或 c) 语句中哪一个是 **false**？
  a) break 语句终止 switch 语句的执行。
  b) break 语句在 while、for 或 do…while 语句中执行时，会导致立即退出该语句。
  c) break 的常见用途是提前从循环中退出或跳过 if…else 的剩余部分。
  d) 以上所有语句都是 *true*。

  **Answer:** c) 是 *false*。实际上，break 跳过的是 switch 的剩余部分，而不是 if…else。

- 2. *(Multiple Choice)* 以下 a)、b) 或 c) 语句中哪一个是 **false**？
  a) continue 语句在 while、for 或 do…while 语句中执行时，会跳过该控制语句主体中的剩余语句并执行循环的下一次迭代。
  b) 在 while 和 do…while 语句中，循环继续条件会在 continue 语句执行后立即求值。
  c) 在 for 语句中，continue 语句执行后，循环继续条件会被求值，然后增量表达式执行。
  d) 以上所有语句都是 *true*。

  **Answer:** c) 是 *false*。实际上，在 for 语句中，continue 语句执行后，增量表达式执行，然后循环继续条件会被求值。

## 4.9 逻辑运算符

到目前为止，我们使用过简单的条件，例如 counter <= 10、total > 1000 和 grade != −1。我们用关系运算符（>、<、>= 和 <=）和相等运算符（== 和 !=）来表达这些条件。每个决策精确测试一个条件。为了在决策过程中测试多个条件，我们必须在单独的语句中执行这些测试，或在嵌套的 if 或 if…else 语句中执行。C 提供了逻辑运算符，可通过组合简单条件来形成更复杂的条件。逻辑运算符是 &&（逻辑与）、||（逻辑或）和 !（逻辑非，也称为逻辑否定）。我们将考虑这些运算符的每个示例。

### 逻辑与 (&&) 运算符

假设我们希望在选择某个执行路径之前确保两个条件都为真。在这种情况下，我们可以按如下方式使用逻辑运算符 &&：

```c
if (gender == 1 && age >= 65) {
    ++seniorFemales;
}
```

这个 if 语句包含两个简单条件。例如，条件 gender == 1 可能会确定某人是否为女性。条件 age >= 65 确定某人是否为老年人。这两个简单条件首先被求值，因为 == 和 >= 的优先级均高于 &&。然后 if 语句考虑组合条件 gender == 1 && age >= 65，该条件在且仅在两个简单条件都为 *true* 时为 *true*。最后，如果此组合条件为 *true*，则前面的 if 语句将 seniorFemales 增加 1。如果一个或两个简单条件为 *false*，程序将跳过 if 的主体并继续执行下一个语句。

下表总结了 && 运算符：

| expression1 | expression2 | expression1 && expression2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | nonzero | 0 |
| nonzero | 0 | 0 |
| nonzero | nonzero | 1 |

该表显示了 *expression1* 和 *expression2* 的零（*false*）和非零（*true*）值的全部四种可能组合。这类表格通常称为真值表。C 将包含关系运算符、相等运算符和/或逻辑运算符的所有表达式求值为 0 或 1。尽管 C 将 *true* 值设为 1，但它接受任何非零值作为 *true*。

### 逻辑或 (||) 运算符

现在让我们考虑 ||（逻辑或）运算符。假设我们在程序的某一点希望在选择某个执行路径之前确保两个条件中一个或两个都为 *true*。在这种情况下，我们使用 || 运算符，如以下程序段所示：

```c
if (semesterAverage >= 90 || finalExam >= 90) {
    puts("Student grade is A");
}
```

该语句包含两个简单条件。条件 semesterAverage >= 90 确定学生是否因整个学期表现稳定而应得“A”。条件 finalExam >= 90 确定学生是否因期末考试表现优异而应得“A”。然后 if 语句考虑组合条件，如果一个或两个简单条件为 *true*，则给学生“A”。消息 "Student grade is A" 会在两个简单条件都为 *false*（零）时才不打印。以下是逻辑或运算符（||）的真值表：
