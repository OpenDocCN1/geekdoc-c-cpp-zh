

```cpp
// termination phase
average = total / 10; // integer division

printf( "Class average is %d\n", average ); // display result
} // end function main
```

```text
Enter grade: 98
Enter grade: 76
Enter grade: 71
Enter grade: 87
Enter grade: 83
Enter grade: 90
Enter grade: 57
Enter grade: 79
Enter grade: 82
Enter grade: 94
Class average is 81
```

**图 3.6** | 使用计数器控制迭代的班级平均分问题。（第 2 部分，共 2 部分。）

该算法提到了一个总和和一个计数器。总和是一个用于累加一系列值之和的变量。计数器是一个变量（第 8 行），用于**计数**——在本例中，用于统计输入的成绩数量。由于本程序中的计数器变量用于从 1 计数到 10（所有值均为正数），我们将该变量声明为 unsigned int，它只能存储非负值（即 0 及更大的值）。用于存储总和的变量应在程序中使用**之前**初始化为零；否则，总和将包含该总和内存位置中先前存储的值。计数器变量通常初始化为零或一，具体取决于其用途——我们将分别给出示例。未初始化的变量包含一个“垃圾”值——即最后存储在为该变量保留的内存位置中的值。

### 常见编程错误 3.4

*如果计数器或总和未初始化，程序的结果很可能是错误的。*

*这是一个逻辑错误的示例。*

### 错误预防提示 3.4

*初始化所有计数器和总和。*

程序中的平均计算产生了整数结果 81。实际上，本例中成绩的总和是 817，除以 10 应得到 81.7，即一个带有**小数点**的数。我们将在下一节中了解如何处理这类数（称为*浮点数*）。

## 关于变量定义位置的重要说明

在第 2 章中，我们提到 C 标准允许将每个变量定义放在 main 中该变量在代码中首次使用之前的**任何位置**。在本章中，我们继续将变量定义集中放在 main 的开头，以强调简单程序的初始化阶段、处理阶段和终止阶段。从第 4 章开始，我们将把每个变量定义放在该变量首次使用之前。我们将看到

## 第二次细化

为了进入下一层细化，即第二次细化，我们确定具体的变量。我们需要一个数字的累计总和、一个已处理数字数量的计数、一个在输入时接收每个成绩值的变量，以及一个保存计算所得平均值的变量。伪代码语句

```
Initialize variables
```

可以细化为如下：

```
Initialize total to zero
Initialize counter to zero
```

只有 total 和 counter 需要初始化；变量 average 和 grade（分别用于计算所得的平均值和用户输入）不需要初始化，因为它们的值将分别由计算得到和由用户输入。伪代码语句

```
Input, sum, and count the quiz grades
```

需要一个迭代结构，依次输入每个成绩。由于我们事先不知道要处理多少个成绩，我们将使用哨兵控制迭代。用户将一次输入一个合法成绩。在输入最后一个合法成绩后，用户将输入哨兵值。程序将在每次输入成绩后测试该值，并在输入哨兵时终止循环。于是，前面伪代码语句的细化结果为

```
Input the first grade (possibly the sentinel)
While the user has not as yet entered the sentinel
    Add this grade into the running total
    Add one to the grade counter
    Input the next grade (possibly the sentinel)
```

请注意，在伪代码中，我们不用花括号括起构成 *while* 语句主体的语句集。我们只是将这些语句全部缩进到 *while* 之下，以表明它们都属于 *while*。再次说明，伪代码是一种非正式的程序开发辅助工具。

伪代码语句

```
Calculate and print the class average
```

可以细化为如下：

```
If the counter is not equal to zero
    Set the average to the total divided by the counter
    Print the average
else
    Print “No grades were entered”
```

请注意，我们在这里谨慎地测试除以零的可能性——这是一个致命错误，如果未被发现，将导致程序失败（通常称为“崩溃”）。完整的第二次细化如图 3.7 所示。

### 常见编程错误 3.5

*试图除以零会导致致命错误。*

### 良好编程实践 3.3

*当对一个值可能为零的表达式执行除法时，应显式测试这种情况并在程序中妥善处理（例如打印错误消息），而不是让致命错误发生。*

在图 3.5 和图 3.7 中，为了提高可读性，我们在伪代码中包含了一些完全空白的行。实际上，这些空白行将这些程序分隔成各个阶段。

```
1 Initialize total to zero
2 Initialize counter to zero
3
4 Input the first grade (possibly the sentinel)
5 While the user has not yet entered the sentinel
6 Add this grade into the running total
7 Add one to the grade counter
8 Input the next grade (possibly the sentinel)
9
10 If the counter is not equal to zero
11 Set the average to the total divided by the counter
12 Print the average
13 else
14 Print "No grades were entered"
```

**图 3.7** | 使用哨兵控制迭代解决班级平均分问题的伪代码算法。

### 软件工程观察 3.3

许多程序在逻辑上可以分为三个阶段：初始化阶段，用于初始化程序变量；处理阶段，用于输入数据值并相应地调整程序变量；以及终止阶段，用于计算并打印最终结果。

图 3.7 中的伪代码算法解决了更一般的班级平均分问题。该算法仅经过两层细化就开发出来了。有时需要更多层细化。

### 软件工程观察 3.4

当伪代码算法被详细到足以让你能够将伪代码转换为 C 程序时，你就终止自顶向下、逐步细化的过程。此后，实现 C 程序通常就很直接了。

C 程序和示例执行结果如图 3.8 所示。尽管只输入了整数成绩，但平均计算很可能产生带有小数点的数。int 类型不能表示这样的数。该程序引入了 float 数据类型来处理带有小数点的数（称为浮点数），并引入了一种称为强制类型转换运算符的特殊运算符来处理平均计算。这些特性将在展示程序之后进行解释。

```c
// Fig. 3.8: fig03_08.c
// Class-average program with sentinel-controlled iteration.
#include <stdio.h>

// function main begins program execution
int main( void )
{
    unsigned int counter; // number of grades entered
    int grade;            // grade value
    int total;            // sum of grades

    float average; // number with decimal point for average

    // initialization phase
    total = 0; // initialize total
    counter = 0; // initialize loop counter

    // processing phase
    // get first grade from user
    printf( "%s", "Enter grade, -1 to end: " ); // prompt for input
    scanf( "%d", &grade ); // read grade from user

    // loop while sentinel value not yet read from user
    while ( grade != -1 ) {
        total = total + grade; // add grade to total
        counter = counter + 1; // increment counter

        // get next grade from user
        printf( "%s", "Enter grade, -1 to end: " ); // prompt for input
        scanf( "%d", &grade ); // read next grade
    } // end while

    // termination phase
    // if user entered at least one grade
    if ( counter != 0 ) {

        // calculate average of all grades entered
        average = ( float ) total / counter; // avoid truncation

        // display average with two digits of precision
        printf( "Class average is %.2f\n", average );
    } // end if
    else { // if no grades were entered, output message
        puts( "No grades were entered" );
    } // end else
} // end function main
```

**图 3.8** | 使用哨兵控制迭代的班级平均分程序。（第 1 部分，共 2 部分。）

