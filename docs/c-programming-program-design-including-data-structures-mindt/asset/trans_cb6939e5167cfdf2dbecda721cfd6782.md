

- 4. 获取 `totalSales`。
- 5. 使用以下公式计算 `additionalBonus`：

```text
if (totalSales is less than 5000)
    additionalBonus = 0
otherwise
    if (totalSales is greater than or equal to 5000 and
        totalSales is less than 10000)
        additionalBonus = totalSales * (0.03)
    otherwise
        additionalBonus = totalSales * (0.06)
```

- 6. 使用以下等式计算 `payCheck`：

```text
payCheck = baseSalary + bonus + additionalBonus
```

### 示例 1-4

在这个示例中，我们设计了一个玩猜数字游戏的算法。目标是随机生成一个大于等于 0 且小于 100 的整数。然后提示玩家（用户）猜这个数字。如果玩家猜对了数字，输出相应的消息；否则，检查猜的数字是否小于随机数。如果猜的数字小于生成的随机数，输出消息“你的猜测低于该数字。再猜一次！”；否则输出消息“你的猜测高于该数字。再猜一次！”然后提示玩家输入另一个数字。系统会不断提示玩家猜测随机数，直到玩家输入正确的数字。

第一步是如上所述生成一个随机数。C++ 提供了实现这一功能的方法，这将在第 5 章中讨论。假设 `num` 表示随机数，`guess` 表示玩家猜测的数字。

玩家输入猜测的数字后，你可以按照以下方式将猜测值与随机数进行比较：

```text
if (guess is equal to num)
    Print "You guessed the correct number."
otherwise
    if (guess is less than num)
        Print "Your guess is lower than the number. Guess again!"
    otherwise
        Print "Your guess is higher than the number. Guess again!"
```

现在你可以设计一个算法，如下所示：

- 1. 生成一个随机数，并将其命名为 `num`。
- 2. *重复*以下步骤，直到玩家猜中正确的数字：
  - a. 提示玩家输入 `guess`。
  - b. 检查 `guess` 的值。

    ```text
    if (guess is equal to num)
        Print "You guessed the correct number."
    otherwise
        if (guess is less than num)
            Print "Your guess is lower than the number. Guess again!"
        otherwise
            Print "Your guess is higher than the number. Guess again!"
    ```

在第 5 章中，我们将使用该算法编写一个 C++ 程序来实现猜数字游戏。

### 示例 1-5

一个班有 10 名学生。每名学生参加了五次测试，每次测试满分为 100 分。我们希望设计一个算法来计算每名学生的成绩以及班级平均分。成绩分配规则如下：如果平均测试成绩大于等于 90，则成绩为 A；如果平均测试成绩大于等于 80 且小于 90，则成绩为 B；如果平均测试成绩大于等于 70 且小于 80，则成绩为 C；如果平均测试成绩大于等于 60 且小于 70，则成绩为 D；否则成绩为 F。请注意，数据包括学生的姓名及其测试成绩。

这是一个可以分解为以下子问题的问题：一共有五次测试，因此你可以设计一个算法来计算平均测试成绩。接下来，再设计一个算法来确定成绩。这两个子问题分别是计算平均测试成绩和确定成绩。

首先让我们设计一个计算平均测试成绩的算法。要求平均测试成绩，需要先将五次测试成绩相加，然后用总和除以 5。因此，算法如下：

- 1. 获取五次测试成绩。
- 2. 将五次测试成绩相加。假设 *sum* 表示测试成绩的总和。
- 3. 假设 *average* 表示平均测试成绩。然后

  `average = sum / 5;`

接下来，设计一个算法来确定成绩。假设 *grade* 表示分配给学生的成绩。以下算法确定成绩：

```text
if average is greater than or equal to 90
    grade = A
otherwise
    if average is greater than or equal to 80
        grade = B
    otherwise
        if average is greater than or equal to 70
            grade = C
        otherwise
            if average is greater than or equal to 60
                grade = D
            otherwise
                grade = F
```

你可以使用这些子问题的解决方案来设计主算法，如下所示：
（假设 **totalAverage** 表示每名学生测试平均成绩的总和。）

- 1. **totalAverage = 0;**
- 2. *重复*以下步骤，对班里的每名学生：
  - a. 获取学生的姓名。
  - b. 使用上述算法计算平均测试成绩。
  - c. 使用上述算法确定成绩。
- 3. 将当前学生的平均测试成绩加到 **totalAverage** 上，更新 **totalAverage**。
- 4. 按如下方式计算班级平均成绩：

  **classAverage = totalAverage / 10**

第 8 章中的一个编程练习要求你编写一个 C++ 程序，计算一个班中每名学生的平均测试成绩和成绩。

> **注意**
>
> 在本章前面，我们描述了问题分析、编码和执行周期。在本节中，我们给出了各种示例来演示问题分析和编码周期。必须指出的是，问题分析是编程中最重要的部分。一旦你分析了问题，并用你的母语写出了解决方案的必要步骤，那么，正如你将在全书中看到的那样，编写 C++ 代码来实现你的解决方案就相对容易了。此外，你很快就会认识到，你的解决方案的步骤可以有效地转化为 C++ 代码。而且，一个好的问题分析将产生一个更好、更干净的程序。虽然我们还没有介绍 C++ 的语法，但为了说明如何编写与解决方案步骤相对应的 C++ 代码，让我们考虑示例 1-1 中设计的算法。假设 *length*、*width*、*perimeter* 和 *area* 分别表示矩形的长度、宽度、周长和面积。下面是算法的四个步骤及其对应的 C++ 语句：
>
> | 算法步骤 | C++ 指令（代码） |
> |---|---|
> | 1. 获取矩形的长度。 | `cin >> length;` |
> | 2. 获取矩形的宽度。 | `cin >> width;` |
> | 3. 计算周长。 | `perimeter = 2 * (length + width);` |
> | 4. 计算面积。 | `area = length * width;` |
>
> 考虑第一条语句。在 C++ 中，`cin` 代表通用输入（common input）。在程序执行期间，与其关联的代码指示用户输入数据，如果用户输入了有效数据，则该数据将被存储在内存中，也就是说，内存成为 **length** 的值。第 3 步中的 C++ 代码使用 **length** 和 **width** 的值来计算 **perimeter**，然后将其赋给 **perimeter**。
>
> 为了编写一个完整的 C++ 程序来计算面积和周长，你需要了解 C++ 程序的基本结构，这将在下一章中介绍。但是，如果你好奇完整的 C++ 程序是什么样子，可以访问本书附带的网站，查看存储在文件 `Ch1_Example_1-1_Code.cpp` 中的程序代码。

## 编程方法论

两种流行的编程设计方法是结构化方法和面向对象方法，下面分别进行概述。

### 结构化编程

将一个问题分解为更小的子问题称为**结构化设计**。然后对每个子问题进行分析，并得出解决该子问题的方案。然后将所有子问题的解决方案组合起来解决整体问题。实现结构化设计的过程称为**结构化编程**。结构化设计方法也称为**自顶向下设计**、**自底向上设计**、**逐步求精**和**模块化编程**。

### 面向对象编程

**面向对象设计（OOD）**是一种广泛使用的编程方法。在 OOD 中，解决问题过程的第一步是识别称为对象的组件，这些对象构成了解决方案的基础，并确定这些对象如何相互交互。例如，假设你想编写一个程序，使本地 DVD 商店的 DVD 出租流程自动化。这个问题中的两个主要对象是 DVD 和顾客。

识别出对象后，下一步是为每个对象指定相关数据以及可对该数据执行的操作。例如，对于 DVD 对象，*数据*可能包括：

- 电影名称
- 发行年份
- 制片人
- 制作公司
- 库存副本数量

DVD 对象上的部分*操作*可能包括：

- 查看电影名称
- 出租一份副本后，将库存副本数量减一
- 当顾客归还某张 DVD 后，将库存副本数量加一

