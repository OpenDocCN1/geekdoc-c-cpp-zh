
- 1. 这段代码执行的是升序排序还是降序排序？你怎么知道？
- 2. 对数组中的数据究竟进行了多少趟处理？请给出一个数字。
- 3. 进行了多少次比较？请给出一个数字。
- 4. 名为`numPasses`、`numCompares`和`numSwaps`的变量是否准确记录了此冒泡排序中进行的趟数、比较次数和交换次数？解释你的答案。

## 实验 9-2：使用冒泡排序

在本实验中，你将完成一个C++程序，该程序使用数组为一位计算机编程教师存储数据。该程序类似于*《编程逻辑与设计（第五版）》*第9章练习3中描述的程序。该程序应允许用户输入一名学生的姓名和10个测验成绩。程序应输出该学生的姓名及其八个最高测验成绩。本实验提供的文件包含必要的变量声明和输入语句。你需要编写代码，使用冒泡排序将成绩按升序排序，然后打印学生的姓名和八个最高测验成绩。代码中的注释会告诉你应在何处编写语句。

- 1. 使用记事本或你选择的文本编辑器打开名为`QuizScores.cpp`的源代码文件。
- 2. 编写冒泡排序和交换函数。
- 3. 输出学生的姓名和八个最高测验成绩。
- 4. 将此源代码文件保存到你选择的目录中，然后将该目录设为你的工作目录。
- 5. 编译源代码文件`QuizScores.cpp`。
- 6. 使用以下输入执行程序并记录输出：
  - 学生姓名：William Moriarty
  - 十个测验成绩：85, 42, 76, 95, 90, 85, 82, 92, 96, 88

## 文件输入与输出

你应在完成*《编程逻辑与设计（第五版）综合篇》*第10章后，再做本节的练习和实验。

商业应用程序通常必须处理大量数据。这些数据存储在一个或多个文件中。正如你在*《编程逻辑与设计（第五版）》*第1章中所学，数据按层次结构组织。层次结构的最低层是**字段**，它是一组字符。上一层是**记录**，它是一组相关字段。例如，你可以编写一个程序来处理员工记录，其中每条员工记录由三个字段组成：员工的名字、员工的姓氏和员工的部门编号。

在C++中，要使用文件中存储的数据，程序必须首先打开文件，然后从文件中读取数据。你可以使用C++库中预编写的类来完成此任务。接下来，你将学习如何使用这些类打开文件、关闭文件、从文件读取数据以及向文件写入数据。

### 使用输入和输出类

要使用执行文件输入（`ifstream`）和输出（`ofstream`）所需的类，你必须在C++程序的开头添加以下预处理指令：

```cpp
#include <fstream>
```

`fstream`类中包含的类是由C++开发团队为你预编写的，它们允许你通过使用这些类创建对象来简化编程任务。然后，你可以在C++程序中使用这些对象的属性和方法。

### 打开文件进行读取

要在C++中打开文件以便将数据读入程序，需要声明一个文件输入流对象（变量），如下所示：

```cpp
ifstream data_in;
```

然后使用open方法（函数）指定要打开的文件名。请看以下示例：

```cpp
data_in.open("inputFile.dat");
```

在示例中，你使用`ifstream`对象（`data_in`），后跟一个点（`.`），再后跟方法名（`open`）来打开文件进行输入。在括号内，你将想要打开的文件名用双引号括起来。这条语句打开名为`inputFile.dat`的文件进行读取。这意味着程序现在可以从该文件中读取数据。在此示例中，名为`inputFile.dat`的文件必须与使用该文件的C++程序保存在同一文件夹中。要打开保存在不同文件夹中的文件，必须指定路径，如下一个示例所示：

```cpp
data_in.open("C:\\myC++Programs\\Chapter9\\inputFile.dat");
```

> **注意**  
> 你可以将`ifstream`视为输入文件的数据类型。在下一章中，你将了解到`ifstream`实际上是一个类，而`data_in`是一个对象。

### 从输入文件读取数据

打开输入文件后，就可以读取文件中的数据了。你可以像使用`cin`时那样使用提取运算符`>>`。

在下一个示例中，我们将假设程序的输入文件按如下方式组织：员工的名字在一行，员工的姓氏在下一行，其薪水在第三行，如下所示：

```
Tim
Moriarty
2000.00
```

要让程序读取这些数据，你可以编写以下C++代码：

```cpp
ifstream data_in;
string firstName, lastName;
double salary;
data_in.open("inputFile.dat");
data_in >> firstName;
data_in >> lastName;
data_in >> salary;
```

示例中的第一行声明了data_in，这是一个ifstream对象。第二行声明了两个名为firstName和lastName的字符串变量。第三行声明了一个名为salary的double变量。接着，data_in与open方法一起使用，打开名为inputFile.dat的文件。然后，提取运算符（>>）被使用三次，从与data_in关联的文件（inputFile.dat）中读取三行输入。此代码执行后，名为firstName的变量包含值Tim，名为lastName的变量包含值Moriarty，名为salary的变量包含值2000.00。

### 使用循环和EOF读取数据

在必须读取大量数据的程序中，通常最好使用循环。在循环中，程序持续从文件读取，直到遇到EOF（文件结束）。在C++中，eof方法（函数）在到达EOF时返回true值，在尚未到达EOF时返回false值。eof方法可与cin一起用于键盘输入，也可与ifstream对象（如data_in）一起使用。

以下C++代码展示了如何将eof方法作为循环的一部分使用：

```cpp
ifstream data_in;
string firstName;
data_in.open("inputFile.dat");
data_in >> firstName;
while(!(data_in.eof()))
{
    cout << firstName;
    data_in >> firstName;
}
```

> **注意**  
> 对于键盘输入，你可以通过键入Ctrl + Z（Windows）或Ctrl + D（UNIX/Linux）来输入EOF字符。

在此示例中，第四行`data_in >> firstName;`使用了预读，然后使用`eof`方法作为`while`循环中要测试的表达式。只要`eof`返回的值不等于`true`，表达式就为`true`，并进入循环。注意，否定运算符（`!`）用于反转`eof`方法返回的值。一旦遇到EOF，测试就变为`false`，程序退出循环。包围`eof`方法调用的括号用于控制优先级。

### 打开文件进行写入

> **注意**  
> 你可以将`ofstream`视为输出文件的数据类型。在下一章中，你将了解到`ofstream`实际上是一个类，而`data_out`是一个对象。

要将C++程序中的数据写入输出文件，程序必须首先打开一个文件。与输入文件类似，你必须先声明一个文件流对象（变量）。对于输出文件，你需声明一个输出流对象，如下所示：

```cpp
ofstream data_out;
```

然后使用`open`方法（函数）指定要打开的文件名。请看以下示例：

```cpp
data_out.open("outputFile.dat");
```

在示例中，你使用`ofstream`对象（`data_out`），后跟一个点（.），再后跟方法名（`open`）来打开文件进行输出。在括号内，你将想要打开的文件名用双引号括起来。这条语句打开名为`outputFile.dat`的文件进行写入。这意味着程序现在可以将数据写入该文件。在此示例中，名为`outputFile.dat`的文件与使用该文件的C++程序保存在同一文件夹中。要打开保存在不同文件夹中的文件，必须指定路径，如下一个示例所示：

```cpp
data_out.open("C:\\myC++Programs\\Chapter9\\outputFile.dat");
```

### 将数据写入输出文件

打开输出文件后，就可以将数据写入文件了。你可以像使用`cout`时那样使用插入运算符`<<`。

例如，假设已像前一个示例那样从输入文件中读取了员工的`firstName`、`lastName`和`salary`，并且该员工将获得15%的加薪，其计算如下：

```cpp
const double INCREASE = 1.15;
double newSalary;
newSalary = salary * INCREASE;
```

现在你要将员工的`firstName`、`lastName`和`newSalary`写入名为`outputFile.dat`的输出文件。以下代码完成此任务：

```cpp
ofstream data_out;
data_out.open("outputFile.dat");
data_out << firstName << endl;
data_out << lastName << endl;
data_out << newSalary << endl;
data_out.close();
```

前一个示例的最后一行使用`data_out`和`close`方法关闭输出文件。在输入和输出文件……时关闭它们是一种良好的编程习惯。
