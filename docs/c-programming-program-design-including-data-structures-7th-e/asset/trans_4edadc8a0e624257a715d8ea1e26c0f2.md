

```text
Account Balance: $892.85
Eighth (from the end) customer's data:
    ID: 11111
    First Name: Rita
    Last Name: Gupta
    Account Balance: $14863.50
```

示例E-6中的程序演示了seekg函数的工作原理。使用seekg函数，可以将文件中的读取位置移动到文件的任意位置。类似地，seekp函数可用于将文件中的写入位置移动到任意位置。此外，这些函数可用于创建二进制文件，其中数据按某个变量或结构体的特定成员的值来组织。例如，假设一个班级中最多有100名学生。每名学生都有一个范围在1到100之间的唯一ID。利用学生ID，我们可以创建一个随机访问二进制文件，使得文件中学生的数据写入到由其ID指定的位置。这就像把文件当作数组来对待。优点是，一旦创建了该文件，就可以直接使用学生ID从文件中读取某位学生的数据。另一个优点是，在文件中，数据是按ID排序的。

这里，我们假设学生ID在1到100之间。然而，如果你使用，比如，三位、四位或五位数字作为学生ID，而班级里只有少数学生，那么文件中的数据可能会分散。换句话说，大量空间可能仅用于存储少数学生的数据。在这种情况下，需要使用更高级的技术来组织数据，以便能够高效地访问这些数据。

示例E-7中的程序说明了如何使用学生ID来组织二进制文件中的数据。该程序还演示了如何输出该文件。

### 示例 E-7

```cpp
//Creating and reading a random access file.

#include <iostream>
#include <fstream>
#include <iomanip>

using namespace std;

struct studentType
{
    char firstName[15];
    char lastName[15];
    int ID;
    double GPA;
};

void printStudentData(const studentType& student);

int main()
{
    studentType st;
    ifstream inFile;                     //Line 1
    ofstream outFile;                    //Line 3

    long studentSize = sizeof(st);       //Line 4

    //open the input file, which is a text file
    inFile.open("studentData.txt");      //Line 5

    if (!inFile)                         //Line 6
    {
        cout << "The input file does not exist. "
             << "The program terminates!!!" << endl; //Line 7
        return 1;                        //Line 8
    }

    //open a binary output file
    outFile.open("student.dat", ios::binary); //Line 9

    inFile >> st.ID >> st.firstName      //Line 10
           >> st.lastName >> st.GPA;

    while (inFile)                       //Line 11
    {
        outFile.seekp((st.ID - 1) * studentSize,
                      ios::beg);         //Line 12
        outFile.write(reinterpret_cast<const char *>(&st),
                      sizeof(st));       //Line 13
        inFile >> st.ID >> st.firstName  //Line 14
               >> st.lastName >> st.GPA;
    }

    inFile.close();                      //Line 15
    inFile.clear();                      //Line 16
    outFile.close();                     //Line 17

    cout << left << setw(3) << "ID"
         << setw(16) << "First Name"
         << setw(16) << "Last Name"
         << setw(12) << "Current GPA" << endl; //Line 18
    cout << fixed << showpoint << setprecision(2); //Line 19

    //open the input file, which is a binary file
    inFile.open("student.dat", ios::binary); //Line 20

    if (!inFile)                         //Line 21
    {
        cout << "The input file does not exist. "
             << "The program terminates!!!" << endl; //Line 22
        return 1;                        //Line 23
    }

    //read the data at location 0 in the file
    inFile.read(reinterpret_cast<char *>(&st),
                sizeof(st));             //Line 24
    while (inFile)                       //Line 25
    {
        if (st.ID != 0)                  //Line 26
            printStudentData(st);        //Line 27

        //read the data at the current reading position
        inFile.read(reinterpret_cast<char *>(&st),
                    sizeof(st));         //Line 28
    }

    return 0;                            //Line 29
}

void printStudentData(const studentType& student)
{
    cout << left << setw(3) << student.ID
         << setw(16) << student.firstName
         << setw(16) << student.lastName
         << right << setw(10) << student.GPA
         << endl;
}
```

### 示例运行

| ID | 名字 | 姓氏 | 当前GPA |
|---:|---|---|---:|
| 2 | Sheila | Duffy | 4.00 |
| 10 | Ajay | Kumar | 3.60 |
| 12 | Ashley | White | 3.90 |
| 16 | Tommy | Pitts | 2.40 |
| 23 | Rita | Gupta | 3.40 |
| 34 | Brad | Smith | 3.50 |
| 36 | Salma | Quade | 3.90 |
| 41 | Steve | Sharma | 3.50 |
| 45 | Sheila | Robinson | 2.50 |
| 56 | Lisa | Johnson | 2.90 |
| 67 | Jose | Ramey | 3.80 |
| 75 | Jennifer | Ackerman | 4.00 |

文件studentData.txt中的数据如下：

```text
12 Ashley White 3.9
34 Brad Smith 3.5
56 Lisa Johnson 2.9
45 Sheila Robinson 2.5
23 Rita Gupta 3.4
10 Ajay Kumar 3.6
67 Jose Ramey 3.8
2 Sheila Duffy 4.0
16 Tommy Pitts 2.4
36 Salma Quade 3.9
75 Jennifer Ackerman 4.0
41 Steve Sharma 3.5
```

## ANSI/ISO标准C++和标准C++中头文件的命名约定

本书中的程序均使用ANSI/ISO标准C++编写。如第1章所述，C++有两个版本——ANSI/ISO标准C++和标准C++。在很大程度上，这两个标准是相同的。标准C++的头文件扩展名为.h，而ANSI/ISO标准C++的头文件没有扩展名。此外，某些头文件（如math.h）在ANSI/ISO标准C++中以前缀字母c开头。C++语言是由C语言演变而来的。因此，某些头文件（如math.h、stdlib.h和string.h）是从C语言引入C++的。而像iostream.h、iomanip.h和fstream.h这样的头文件则是专为C++设计的。回想一下，当程序中包含一个头文件时，该头文件的全局标识符也会成为程序的全局标识符。在ANSI/ISO标准C++中，为了利用命名空间机制，所有头文件都被修改，使标识符在命名空间内声明。回顾一下，这个命名空间的名字是std。

在ANSI/ISO标准C++中，专为C++设计的头文件的扩展名.h被去掉了。对于从C语言引入C++的头文件，扩展名.h也被去掉，并且这些头文件的名称以字母c开头。以下是标准C++和ANSI/ISO标准C++中最常用的头文件名称：

| 标准C++头文件名 | ANSI/ISO标准C++头文件名 |
|---|---|
| `assert.h` | `cassert` |
| `ctype.h` | `cctype` |
| `float.h` | `cfloat` |
| `fstream.h` | `fstream` |
| `iomanip.h` | `iomanip` |
| `iostream.h` | `iostream` |
| `limits.h` | `climits` |
| `math.h` | `cmath` |
| `stdlib.h` | `cstdlib` |
| `string.h` | `cstring` |

要包含一个头文件，例如 `iostream`，需要以下语句：

```cpp
#include <iostream>
```

此外，要使用诸如 cin、cout、endl 等标识符，程序应使用以下语句之一：

```cpp
using namespace std;
```

或者在标识符前加上前缀 `std::`。

## 附录F：头文件

C++标准库包含许多预定义函数、命名常量和专用数据类型。本附录讨论了一些最常用的库例程（以及几个命名常量）。关于函数、命名常量等的更多解释和信息，请查阅你的系统文档。标准C++头文件的名称在括号中给出。

### 头文件 cassert（cassert.h）

下表描述了函数 `assert`。其规范包含在头文件 cassert（cassert.h）中。

| 函数 | 描述 | 行为 |
|---|---|---|
| `assert(expression)` | `expression` 是任意 `int` 表达式；`expression` 通常是逻辑表达式 | - 如果 `expression` 的值非零（`true`），程序继续执行。<br>- 如果 `expression` 的值为0（`false`），程序立即终止执行。将显示该表达式、包含源代码的文件名以及源代码中的行号。 |

> **注意**  
> 要禁用所有assert语句，请将预处理指令 `#define NDEBUG` 放在指令 `#include <cassert>` 之前。

