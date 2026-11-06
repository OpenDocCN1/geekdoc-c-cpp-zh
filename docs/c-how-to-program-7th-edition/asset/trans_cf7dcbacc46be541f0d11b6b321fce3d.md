

```cpp
gradeCounter = 0; // initialize loop counter

// processing phase
// prompt for input and read grade from user
cout << "Enter grade or -1 to quit: ";
cin >> grade; // input grade or sentinel value

// loop until sentinel value read from user
while ( grade != -1 ) // while grade is not -1
{
   total = total + grade; // add grade to total
   gradeCounter = gradeCounter + 1; // increment counter

   // prompt for input and read next grade from user
   cout << "Enter grade or -1 to quit: ";
   cin >> grade; // input grade or sentinel value
} // end while

// termination phase
if ( gradeCounter != 0 ) // if user entered at least one grade...
{
   // calculate average of all grades entered
   average = static_cast< double >( total ) / gradeCounter;

   // display total and average (with two digits of precision)
   cout << "\nTotal of all " << gradeCounter << " grades entered is "
        << total << endl;
   cout << "Class average is " << setprecision( 2 ) << fixed << average
        << endl;
} // end if
else // no grades were entered, so output appropriate message
   cout << "No grades were entered" << endl;
} // end function determineClassAverage
```

**图 4.13** | 使用哨兵控制的重复实现班级平均成绩问题：GradeBook 源代码文件。（共 2 部分，第 2 部分。）

第 55 行将变量 `gradeCounter` 初始化为 0，因为此时还没有输入任何成绩。请记住，该程序使用哨兵控制的重复。为了准确记录输入的成绩数量，程序仅在用户输入有效的成绩值（即不是哨兵值）并且程序完成输入处理时，才递增变量 `gradeCounter`。请注意，两个输入语句（第 57 行和第 67 行）之前都有输出语句，用于提示用户输入。

![](img/023f159fdd47d944d48e08843cea732d_171_0.png)

## 良好的编程实践 4.8

对于每次键盘输入，都应提示用户。提示应说明输入的形式以及任何特殊的输入值。例如，在哨兵控制的循环中，请求输入数据的提示应明确提醒用户哨兵值是什么。

## 哨兵控制的重复与计数器控制的重复的程序逻辑

将本例中的哨兵控制重复的程序逻辑与图 4.9 中的计数器控制重复逻辑进行比较。在计数器控制的重复中，`while` 语句的每次迭代（图 4.9 的第 54～60 行）都会从用户处读取一个值，迭代次数由指定的次数决定。在哨兵控制的重复中，程序在执行到 `while` 之前读取第一个值（图 4.13 的第 56～57 行）。该值决定程序的控制流是否应进入 `while` 的循环体。如果 `while` 的条件为假，说明用户输入了哨兵值，因此 `while` 的循环体不会执行（即没有输入任何成绩）。另一方面，如果条件为真，循环体便开始执行，循环将成绩值加到总成绩中（第 62 行），并递增 `gradeCounter`（第 63 行）。随后，循环体中的第 66～67 行提示用户输入下一个值，并从用户处读取该值。接着，程序控制到达第 68 行循环体的右大括号（`}`），因此执行继续进行 `while` 条件的测试（第 60 行）。该条件使用用户最近输入的成绩来确定循环体是否应再次执行。变量 `grade` 的值总是在程序测试 `while` 条件之前立即从用户处读取。这样，程序就能在处理刚输入的值之前（即将其加到总成绩并递增 `gradeCounter` 之前）判断该值是否为哨兵值。如果输入的是哨兵值，循环终止，程序不会将 `-1` 加到总成绩中。

```cpp
// Fig. 4.14: fig04_14.cpp
// Create GradeBook object and invoke its determineClassAverage function.
#include "GradeBook.h" // include definition of class GradeBook

int main()
{
   // create GradeBook object myGradeBook and
   // pass course name to constructor
   GradeBook myGradeBook( "CS101 C++ Programming" );

   myGradeBook.displayMessage(); // display welcome message
   myGradeBook.determineClassAverage(); // find average of 10 grades
} // end main
```

```text
Welcome to the grade book for
CS101 C++ Programming

Enter grade or -1 to quit: 97
Enter grade or -1 to quit: 88
Enter grade or -1 to quit: 72
Enter grade or -1 to quit: -1

Total of all 3 grades entered is 257
Class average is 85.67
```

**图 4.14** | 使用哨兵控制的重复实现班级平均成绩问题：创建 `GradeBook` 对象并调用其 `determineClassAverage` 成员函数。

循环终止后，第 71～83 行的 `if...else` 语句会执行。第 71 行的条件用于判断是否输入了任何成绩。如果没有输入成绩，`if...else` 语句的 `else` 部分（第 82～83 行）会执行，显示消息 `"No grades were entered"`，然后成员函数将控制权返回给调用函数。

请注意图 4.13 中 `while` 循环里的代码块。如果没有大括号，循环体中的最后三条语句就会位于循环之外，导致计算机错误地解释这段代码，如下所示：

```cpp
// loop until sentinel value read from user
while ( grade != -1 )
    total = total + grade; // add grade to total
    gradeCounter = gradeCounter + 1; // increment counter

// prompt for input and read next grade from user
cout << "Enter grade or -1 to quit: ";
cin >> grade;
```

如果用户没有在第一次输入成绩时（第 57 行）输入 `-1`，这将导致程序进入无限循环。

## 常见编程错误 4.11

省略用于界定代码块的大括号可能导致逻辑错误，例如无限循环。为了避免此问题，一些程序员会将每条控制语句的循环体都放在大括号中，即使循环体只包含一条语句。

### 浮点数精度和内存需求

`float` 类型的变量表示单精度浮点数，在大多数 32 位系统上具有 7 位有效数字。`double` 类型的变量表示双精度浮点数。这类变量所需的内存是 `float` 变量的两倍，并且在大多数 32 位系统上可提供 15 位有效数字——精度大约是 `float` 变量的两倍。对于大多数程序所需的数值范围，`float` 类型的变量应该足够使用，但你也可以使用 `double` 来“确保万无一失”。在某些程序中，即使 `double` 类型的变量也不够用——这类程序超出了本书的范围。大多数程序员使用 `double` 类型表示浮点数。事实上，默认情况下，C++ 会将你在程序源代码中输入的所有浮点数（例如 7.33 和 0.0975）视为 `double` 值。源代码中的这类值称为浮点常量。有关 `float` 和 `double` 的取值范围，请参阅附录 C“基本类型”。

浮点数通常是除法运算的结果。在常规算术中，将 10 除以 3，结果为 3.3333333……，其中 3 的序列会无限重复。计算机只能分配固定大小的空间来存储这样的值，因此显然，存储的浮点值只能是一个近似值。

## 常见编程错误 4.12

以假设浮点数能够被精确表示的方式使用浮点数（例如，在相等性比较中使用浮点数），可能导致错误结果。浮点数只能以近似值表示。

尽管浮点数并不总能达到 100% 的精确度，但它们有许多应用场景。例如，当我们说“正常”的体温是 98.6 时，并不需要精确到很多位数字。当我们从温度计上读到 98.6 时，它实际的值可能是 98.5999473210643。在大多数涉及体温的应用中，将这个数简单地称为 98.6 是没有问题的。由于浮点数具有不精确的特性，因此相比 `float` 类型，更推荐使用 `double` 类型，因为 `double` 变量能够更准确地表示浮点数。基于这一原因，本书始终使用 `double` 类型。

