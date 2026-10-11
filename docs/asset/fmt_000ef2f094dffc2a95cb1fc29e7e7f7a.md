
```
Enter grade: 88
Enter grade: 79
Enter grade: 95
Enter grade: 100
Enter grade: 48
Enter grade: 88
Enter grade: 92
Enter grade: 83
Enter grade: 90
Enter grade: 85
```

Total of all 10 grades is 848

Class average is 84

> 图 5.9 使用计数控制迭代解决班级平均分问题。（2部分/2部分）

### Main 中的局部变量

第 10、11、17 和 23 行分别声明了局部变量 `total`、`gradeCounter`、`grade` 和 `average`。在方法中声明的变量是局部变量，可以从其声明行一直到该变量所在块的结束右括号处使用。局部变量的声明必须在使用之前出现；否则会发生编译错误。变量 `grade`——在 `while` 循环体中声明——只能在该代码块内使用。

### 初始化阶段：初始化变量 `total` 和 `gradeCounter`

# 要求局部变量必须经过明确赋值——也就是说，在变量值在使用之前，每个局部变量都必须赋予一个值。第 10-11 行在使用这些值之前声明并初始化了 `total` 为 0，`gradeCounter` 为 1，因此这些变量是经过明确赋值的（分别如第 17 行和第 23 行中的 `grade` 和 `average` 直接）。

![](img/57baed2319be0bb1b5f98674846f2711_199_0.png)

#### 常见编程错误 5.3

所有局部变量在表达式中使用值之前必须进行赋值。

在局部变量明确赋值之前使用其值会导致编译错误。

## 200 第5章 算法开发与控制语句：第一部分

![](img/57baed2319be0bb1b5f98674846f2711_200_0.png)

### 错误预防提示 5.2

在声明时初始化局部变量可以帮助避免因尝试使用未初始化的数据而可能引起的编译错误。虽然 C# 不要求将局部变量初始化包含在声明中，但要求局部变量在表达式中使用值之前必须初始化。

![](img/57baed2319be0bb1b5f98674846f2711_200_1.png)

### 错误预防提示 5.3

在声明中或赋值语句中初始化每个计数器和总和。总和通常初始化为 0。计数器通常初始化为 0 或 1，取决于它们的用法（我们将展示这两种用法的示例）。

### 处理阶段：从用户处读取 10 个成绩

第 14 行表示，只要 `grade` 的值小于或等于 10，`while` 语句就继续循环（也称为迭代）。只要该条件为真，`while` 语句就会重复执行大括号内的限制其体的语句（第 15–20 行）。

第 16 行显示 `"Enter grade: "`。第 17 行输入用户输入的成绩并将其赋值给变量 `grade`。然后，第 18 行将用户输入的新成绩加到 `total` 中，并将结果赋值给 `total`，替换其原有值。

第 19 行给 `gradeCounter` 加1，表示程序已处理了一个成绩，并准备好从用户处输入下一个成绩。增加 `gradeCounter` 最终会导致其超过 10。然后循环终止，因为其条件（第 14 行）变为假。

### 终止阶段：计算并显示班级情况

当循环结束时，第 23 行在 `average` 变量的初始化器中执行平均值计算。第 26 行显示 `"Total of 10 grades is "` 后后接 `total` 的值。然后，第 27 行显示 `"Class average "` 后接 `average` 的值。当执行到第 28 行时，`Main` 方法执行了所有工作。注意，此示例只包含一个类；在本章和第3章中，你已经见过由两个类组成的示例：

- 一个包含实例变量、属性以及使用这些实例变量和属性执行任务的方法；
- 另一个包含 `Main` 方法，该方法创建另一个类的对象并调用其方法且访问其属性。

偶尔，如果创建一个单独的类来演示某个概念没有意义，我们将程序的语句完全放在单个类的 `Main` 方法中。

### 5.9.3 整数除与截断

第 23 行执行的平均值计算产生一个整数结果。应用程序的输出表明，在示例执行中，成绩值的总和为 848，除以 10 得到 84.8。然而，结果是 84。我们将在下一节查看如何获取浮点结果。

## 5.10 算法制定：计数控制迭代

## 201 算法制定：计数控制迭代

### 常见编程错误 5.4

假设整数除四舍五入（而不是截断）会导致结果错误。例如，`75/10` 得到 7。

![](img/57baed2319be0bb1b5f98674846f2711_201_0.png)

### 5.10 算法制定：计数控制迭代

让我们推广 5.9 中的班级平均分问题。考虑以下问题：开发一个处理任意数量学生成绩的班级平均分程序。在之前的示例中指定了学生人数，所以成绩数量（10）是已知的。在这个示例中，循环开始之前没有指示将输入多少成绩。我们如何确定停止？

解决方法是一种使用特殊的哨兵值（也称为信号值、虚拟值或标记值）来指示“数据结束”。用户一直输入直到所有成绩输入完毕。计数控制迭代通常被称为不定迭代，因为在循环开始之前不知道迭代次数。显然，必须选择一个不会与有效值混淆的哨兵值。成绩是正数，因此 `-1` 不是此问题的有效值。因此，该班级平均分程序的运行可能会处理如下输入序列：95, 96, 75, 74, 89 和 `-1`。然后程序将计算并打印 95, 96, 75, 74 和 89 的班级平均分；由于 `-1` 是哨兵值，它不应进入平均计算过程。

### 5.10.1 自顶向下的逐步细化：顶层与第一次细化

我们采用自顶向下的逐步细化技术来处理这个班级平均分程序，这对于开发结构良好的程序至关重要。我们从顶层的伪代码开始——一个传达程序总体目的语句：

> 确定测验的班级平均分

顶层实际上是程序的完整表示。遗憾的是，顶层很少传达关于编写 C# 应用程序的具体细节。因此，我们开始细化过程。我们将顶层分为更小的任务集，并按照执行顺序列出。这得到了如下第一次细化：

- 初始化变量
- 输入、求和并统计成绩
- 计算并打印班级平均分

这种细化只使用了顺序结构——列出的步骤应该按顺序一个接一个地执行。

# 第 5 章 算法开发与控制语句：第一部分

> 软件工程观察 5.2

每一次细化以及顶层本身，都是算法的完整规范——仅仅详细程度不同。

> 软件工程观察 5.3

许多程序在逻辑上可以分为三个阶段：初始化变量的初始化阶段；输入数据值并相应调整程序变量的处理阶段；以及计算并输出最终结果的终止阶段。

## 5.10.2 第二次细化

在自顶而下的过程中，上述软件工程观察通常就是第一次细化所需的全部内容。为了继续进行下一级细化——即第二次细化——我们了特定的变量。在这个示例中，我们需要一个数字的运行总和、一个处理数字数量的计数、一个用于接收用户输入的每个成绩值的变量，以及一个用于计算平均值的变量。伪代码语句

可以细化如下：

```
Initialize total to zero
Initialize counter to zero
```

只有 `total` 和 `counter` 两个变量在使用之前需要初始化。变量 `average` 和 `grade`（分别计算出的平均值和用户输入）不需要初始化，因为它们的值在计算或输入时会被覆盖。

伪代码语句

```
Input, sum and count the quiz grades
```

需要迭代来连续输入每个成绩。我们无法预知将输入多少个成绩，因此我们将使用哨兵值控制迭代。用户一次输入一个。在最后一个成绩之后，用户输入哨兵值。程序在每个成绩输入后测试哨兵值，并在用户输入哨兵值时终止循环。上述伪代码语句的第二次细化如下所示：

```
Prompt the user to enter the first grade
Input the first grade (possibly the sentinel)
While the user has not yet entered the sentinel
  Add this grade into the running total
  Add one to the grade counter
Prompt the user to enter the next grade
Input the next grade (possibly the sentinel)
```

我们对 `While` 下的语句进行缩进，以表示它们属于 `While`。再次强调，伪代码仅是非正式的程序开发辅助。

伪代码语句

```
Calculate and print the class average
```

## 5.10 制定算法：哨兵值控制迭代

可以细化如下：

```
If the counter is not equal to zero
  Set the average to the total divided by the counter
  Print the average
Else
  Print "No grades were entered"
```

我们仔细测试了除以零的可能性——这是一种逻辑错误，如果未检测到，会导致程序失败或产生无效输出。班级平均值问题伪代码的完整细化如图 5.10 所示。

## 错误预防提示 5.4

在对值可能为零的表达式进行除法时，请显式地测试这种可能性并在你的应用程序中妥善处理（例如显示错误消息），而不是让错误发生。

![](img/57baed2319be0bb1b5f98674846f2711_203_0.png)

```
Initialize total to zero
Initialize counter to zero
3
Prompt the user to enter the first grade
Input the first grade (possibly the sentinel)
6
While the user has not yet entered the sentinel
  Add this grade into the running total
  Add one to the grade counter
Prompt the user to enter the next grade
  Input the next grade (possibly the sentinel)
12
If the counter is not equal to zero
  Set the average to the total divided by the counter
  Print the average
15
Else
  Print "No grades were entered"
```

图 5.10 使用哨兵值控制迭代的班级平均值伪代码算法。

在图 5.8 和图 5.10 中，我们在伪代码中加入了空行和缩进，使其更具读性。空行分隔了算法的不同阶段并区分了控制语句；缩进强调了控制语句体。

图 5.10 中的伪代码算法解决了更一般的班级平均值问题。该算法是在两次细化后开发的。有时我们需要这样做。

![](img/57baed2319be0bb1b5f98674846f2711_203_1.png)

## 软件工程观察 5.4

当你指定的伪代码细节详细到足以让你将其转换为 C# 时，停止自顶而下的分步细化过程。

## 软件工程观察 5.5

有些程序员不使用伪代码等程序开发工具。他们认为最终目标是在计算机上解决问题，编写伪代码几乎会推迟最终输出的生成。虽然这对于简单且熟悉的问题可能有效，但在大型复杂的项目中会导致严重的错误和延迟。

![](img/57baed2319be0bb1b5f98674846f2711_204_0.png)

## 5.10.3 实现哨兵值控制迭代

在图 5.11 中，`Main` 方法实现了图 5.10 的伪代码算法。虽然用户输入的每个成绩都是整数，但平均值计算可能会产生带有小数点的数字——换句话说，实数或浮点数（例如 0.733、0.0975 或 100.12345）。`int` 类型无法表示此类数字，因此此示例必须使用 `float` 或 `double`。C# 提供了如 `float` 和 `double` 等数据类型在内存中存储浮点数。

```
// 5.11: ClassAverage.cs
// 使用哨兵值控制迭代解决班级平均值问题。
using System;
class ClassAverage
{
    static void Main()
    {
        // 初始化阶段
        int total = 0; // 初始化成绩总和
        int gradeCounter = 0; // 初始化已输入的成绩数量

        // 处理阶段
        Console.Write("Enter grade or -1 to quit: ");
        int grade = int.Parse(Console.ReadLine());

        // 循环直到从用户处读取哨兵值
        while (grade != -1)
        {
            total = total + grade; // 将成绩加到总和
            gradeCounter = gradeCounter + 1; // 计数器加1

            // 提示输入并从用户读取成绩
            Console.Write("Enter grade or -1 to quit: ");
            grade = int.Parse(Console.ReadLine());
        }

        // 终止阶段
        // 如果用户至少输入了一个成绩
        if (gradeCounter != 0) {
            // 使用浮点数计算平均值
            double average = (double) total / gradeCounter;

            // 显示总和平均值（两位精度）
            Console.WriteLine($"total of {gradeCounter} grades entered is {total}");
            Console.WriteLine($"Class average is {average:F2}");
        } else {
            // 没有输入成绩，所以输出错误消息
            Console.WriteLine("No grades entered");
        }
    }
}
```

图 5.11 使用哨兵值控制迭代解决班级平均值问题。（第一部分）。

## 5.10 制定算法：哨兵值控制迭代

```
// 终止阶段
// 如果用户至少输入了一个成绩
if (gradeCounter != 0) {
    // 使用浮点数计算平均值
    double average = (double) total / gradeCounter;

    // 显示总和平均值（两位精度）
    Console.WriteLine($"total of {gradeCounter} grades entered is {total}");
    Console.WriteLine($"Class average is {average:F2}");
} else {
    // 没有输入成绩，所以输出错误消息
    Console.WriteLine("No grades entered");
}
```

+   Enter grade or -1 to quit: 97

Enter grade or -1 to quit: 88

Enter grade or -1 to quit: 72

Enter grade or -1 to quit: -1

Total of the 3 grades entered is 257

Class average is 85.67

## 5.10.4 哨兵值控制迭代的程序逻辑

第 11 行将 `gradeCounter` 初始化为 0，因为还没有输入成绩。记住，此程序使用哨兵值控制迭代来输入成绩。只有当用户输入有效成绩时，程序才增加 `gradeCounter`。第 34 行声明 `double average`，它将班级平均值存储为浮点数。将哨兵值控制迭代的程序逻辑与图 5.9 中的计数迭代进行比较。在计数迭代中，`while` 语句的每次迭代都会从用户处读取一个值；在哨兵值控制迭代中，程序在到达 `while` 之前提示（图 5.11 第 15-16 行）。该值决定了程序的控制流是否应该进入 `while` 的体。如果 `while` 为假（第 19 行），用户输入了哨兵值，因此 `while` 的体不执行（即没有输入成绩）。反之，如果条件为真，则开始执行体，循环将成绩值加到总和

# 第5章 算法开发与控制语句：第一部分

增加 `gradeCounter`（第21–22 行）。然后循环体内的第 25–26 行从用户处输入下一个值。接下来，程序到达第 27 行循环体的右大括号，因此执行继续对 `while` 条件进行测试（第 19 行）。代码使用用户输入的最高分数来决定是否应再次执行循环。

变量 `grade` 的值在程序测试 `while` 条件之前立即从用户处输入。这允许程序在处理该值（即将其加到总和）之前，确定刚刚发送的值是否为哨兵值。如果输入了哨兵值，循环将终止，程序不会向总和中加 -1。

> 良好的编程实践 5.3

在哨兵值控制的循环中，提示信息应当提醒用户哨兵值。

循环结束后，执行第 31–44 行的 `if...else` 语句。第 31 行确定是否输入了分数。如果没有，则执行 `if...else` 语句的部分并显示消息“No grades were entered”（未输入分数）。

## 5.10.5 while 语句中的大括号

注意图 5.11 中的 `while` 语句块（第 20–27 行）。如果没有大括号，循环将被只认为第一条语句，即将分数加到总数的语句。块中的最后三个语句将落在循环体之外，导致计算机错误地解释代码为：
