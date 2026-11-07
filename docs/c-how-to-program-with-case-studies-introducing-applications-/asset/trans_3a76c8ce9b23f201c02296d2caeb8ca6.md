
答案：c）错误。实际上，经验表明，在计算机上解决问题最困难的部分是为解决方案开发算法。一旦指定了正确的算法，生成可运行的 C 程序的过程通常就很直接。

3（程序段）当以指定精度打印浮点值时，打印值会被舍入。编写语句分别以 1 位、4 位和 10 位精度显示值 98.5999473210643，并说明每种情况下显示的内容。

答案：见下文。

```c
printf("%.1f\n", 98.5999473210643); // displays 98.6
printf("%.4f\n", 98.5999473210643); // displays 98.5999
printf("%.10f\n", 98.5999473210643); // displays 98.5999473211
```

## 3.10 用自顶向下、逐步细化方法设计算法 案例研究 3：嵌套控制语句

让我们再处理一个完整问题。我们将使用伪代码以及自顶向下、逐步细化的方法来设计算法，并编写相应的 C 程序。我们已经看到，控制语句可以像孩子堆叠积木一样，一个叠一个地（按顺序）堆叠。在本案例研究中，我们将看到 C 中控制语句唯一另一种结构化连接方式，即把一个控制语句嵌套在另一个控制语句中。考虑以下问题陈述：

> > 一所大学开设了一门课程，为学生参加房地产经纪人的州执照考试做准备。去年，完成这门课程的 10 名学生参加了执照考试。自然，学院想知道它的学生在考试中表现如何。有人要求你编写一个程序来汇总结果。你已得到这 10 名学生的名单。每个名字旁边是 1（如果该学生通过考试）或 2（如果该学生未通过考试）。

你的程序应按如下方式分析考试结果：

- 1. 输入每个考试结果（即 1 或 2）。每次程序请求另一个考试结果时，显示提示消息“输入结果”。
- 2. 统计每种类型的考试结果数量。
- 3. 显示考试结果摘要，指出通过和未通过的学生人数。
- 4. 如果有超过八名学生通过考试，打印消息“给教师奖励！”

仔细阅读问题陈述后，我们作出以下观察：

- 1. 程序必须处理 10 个考试结果。我们将使用计数器控制的循环。
- 2. 每个考试结果都是一个数字——要么是 1，要么是 2。每次程序读取一个考试结果时，它必须确定该结果是 1 还是 2。我们将在算法中测试是否为 1。如果该数字不是 1，我们就假定它是 2。练习 3.27 要求你确保每个考试结果都是 1 或 2。
- 3. 使用两个计数器——一个统计通过考试的学生人数，另一个统计未通过考试的学生人数。
- 4. 程序处理完所有结果后，必须判断是否有超过 8 名学生通过考试，如果是，则打印“给教师奖励！”。

### 顶层的伪代码表示

我们继续采用自顶向下、逐步细化的方法。首先给出顶层的伪代码表示：

```
Analyze exam results and decide whether instructor should receive a bonus
```

再次强调，顶层表示是程序的完整表示，但在伪代码能够自然地演化为 C 程序之前，很可能需要进行多次细化。

### 第一次细化

我们的第一次细化是：

- 初始化变量
- 输入十个考试结果并统计通过和未通过人数
- 打印考试结果摘要并决定是否给教师奖励

同样，尽管我们已经有了整个程序的完整表示，仍需要进一步细化。

### 第二次细化

现在我们确定具体变量。我们需要计数器记录通过和未通过人数，一个计数器控制循环过程，以及一个变量存储用户输入。

伪代码语句“初始化变量”可以细化为：

```
Initialize passes to zero
Initialize failures to zero
Initialize student to one
```

只初始化计数器和总计。伪代码语句“输入十个考试结果并统计通过和未通过人数”需要一个循环，依次输入每个考试的结果。这里我们事先知道正好有十个考试结果，因此适合使用计数器控制的循环。在循环内部（即嵌套在循环中），双选择语句将确定每个考试结果是通过还是未通过，并递增相应的计数器。于是，前面伪代码语句的细化为：

```
While student counter is less than or equal to ten
    Input the next exam result
    If the student passed
        Add one to passes
    else
        Add one to failures
    Add one to student counter
```

伪代码语句“打印考试结果摘要并决定是否给教师奖励”可以细化为：

```
Print the number of passes
Print the number of failures
If more than eight students passed
    Print "Bonus to instructor!"
```

### 完整的第二次细化

图 3.5 包含完整的第二次细化。我们使用空行提高可读性。

```
1  Initialize passes to zero
2  Initialize failures to zero
3  Initialize student to one
4
5  While student counter is less than or equal to ten
6      Input the next exam result
7
8      If the student passed
9          Add one to passes
10     else
11         Add one to failures
12
13     Add one to student counter
14
15 Print the number of passes
16 Print the number of failures
17 If more than eight students passed
18     Print "Bonus to instructor!"
```

**图 3.5** | 考试结果问题的伪代码。

### 实现算法

这个伪代码现在已足够细化，可以转换为 C。图 3.6 显示了 C 程序和两个示例执行结果。

```c
// fig03_06.c
// Analysis of examination results.
#include <stdio.h>

// function main begins program execution
int main(void) {
    // initialize variables in definitions
    int passes = 0;
    int failures = 0;
    int student = 1;

    // process 10 students using counter-controlled loop
    while (student <= 10) {
        // prompt user for input and obtain value from user
        printf("%s", "Enter result (1=pass, 2=fail): ");
        int result = 0; // one exam result
        scanf("%d", &result);

        // if result 1, increment passes
        if (result == 1) {
            passes = passes + 1;
        } // end if
        else { // otherwise, increment failures
            failures = failures + 1;
        } // end else

        student = student + 1; // increment student counter
    } // end while

    // termination phase; display number of passes and failures
    printf("Passed %d\n", passes);
    printf("Failed %d\n", failures);

    // if more than eight students passed, print "Bonus to instructor!"
    if (passes > 8) {
        puts("Bonus to instructor!");
    } // end if
} // end function main
```

![](img/43d318ad505997c339a3ea78d716d162_164_0.png)

**图 3.6** | 考试结果分析。（第 1 部分，共 2 部分。）

```
    Enter Result (1=pass, 2=fail): 1
    Enter Result (1=pass, 2=fail): 1
    Enter Result (1=pass, 2=fail): 1
    Enter Result (1=pass, 2=fail): 2
    Enter Result (1=pass, 2=fail): 1
    Enter Result (1=pass, 2=fail): 1
    Enter Result (1=pass, 2=fail): 1
    Enter Result (1=pass, 2=fail): 1
    Enter Result (1=pass, 2=fail): 1
    Enter Result (1=pass, 2=fail): 1
    Passed 9
    Failed 1
    Bonus to instructor!
```

**图 3.6** | 考试结果分析。（第 2 部分，共 2 部分。）

### 自测

- 1（填空题）控制语句可以像孩子堆叠积木一样，一个叠一个地（按顺序）堆叠。在 C 中，控制语句唯一另一种结构化连接方式是 ________——也就是，将一个控制语句放在另一个控制语句内部。

答案：嵌套。

## 3.11 赋值运算符

C 提供了几个赋值运算符来缩写赋值表达式。例如，语句

```
c = c + 3;
```

可以用加法赋值运算符 `+=` 缩写为

```
c += 3;
```

`+=` 运算符将运算符右侧表达式的值加到运算符左侧变量的值上，然后将结果存入左侧变量。因此，赋值 `c += 3` 将 3 加到 `c` 的当前值上。下表列出了算术赋值运算符、使用这些运算符的示例表达式以及说明：

| 赋值运算符 | 示例表达式 | 说明 | 赋值结果 |
|---|---|---|---|
| *假设：int c = 3, d = 5, e = 4, f = 6, g = 12;* | | | |
| `+=` | `c += 7` | `c = c + 7` | 将 10 赋给 c |
| `-=` | `d -= 4` | `d = d - 4` | 将 1 赋给 d |
| `*=` | `e *= 5` | `e = e * 5` | 将 20 赋给 e |
| `/=` | `f /= 3` | `f = f / 3` | 将 2 赋给 f |
| `%=` | `g %= 9` | `g = g % 9` | 将 3 赋给 g |

