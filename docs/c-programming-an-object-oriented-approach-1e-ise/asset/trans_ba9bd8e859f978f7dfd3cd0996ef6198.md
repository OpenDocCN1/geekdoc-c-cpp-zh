
在程序 16.15 的第 22 行，我们取一个 int 类型变量的地址，将其解释为指向字符的指针，并将其内容作为字符写入文件。在第 23 行我们也这样做，但该变量是 double 类型。

在第 35 行，我们取一个 int 类型变量的地址，将内存中保留的位置解释为指向字符的指针，并将从文件中提取的字符存储到其中。在第 36 行我们也这样做，但该位置是 double 类型。

注意，在两种情况下（读取和写入），我们都将基本数据类型的地址解释为指向字符的指针。

## 用户定义对象的转换

之所以可以进行这种转换，是因为基本数据类型的对象在内存中存储为位（或字节）序列。我们唯一需要做的是修改读/写函数，使其访问类类型的变量，而不是基本数据类型的变量。

读取时，我们需要一个空对象（由默认构造函数创建），用文件中的字符填充它。写入时，我们需要一个已填充的对象（由带参数构造函数创建），将其转换为字符并写入文件，如下所示：

```cpp
istream& read (reinterpret_cast <char*> (&object), sizeof (class))
ostream& write (reinterpret_cast <char*> (&object), sizeof (class))
```

我们可以创建一个表示学生信息（身份标识、姓名和 GPA）的类，将该类的实例写入文件，然后从文件中读取这些实例。接下来我们展示接口文件、实现文件和应用文件。程序 16.16 展示了接口文件。

### 程序 16.16 文件 student.h

```cpp
/**********************************************************
 * The program defines the interface file for the Student class
 * to be used to store student records in a binary file
 **********************************************************/
#ifndef STUDENT_H
#define STUDENT_H
#include <iostream>
#include <fstream>
#include <cassert>
#include <iomanip>
#include <cstring>
#include <string>
using namespace std;

class Student
{
private:
   int stdId;
   char stdName [20];
   double stdGpa;
public:
    Student(int, const string&, double);
    Student();
    ~Student();
    int getId() const;
    string getName() const;
    double getGpa() const;
};
#endif
```

程序 16.17 展示了 Student 类的实现文件。注意，我们使用访问器函数来获取数据成员的值，但也可以为该类重载插入运算符。

### 程序 16.17 文件 student.cpp

```cpp
/******************************************************
 * The implementation file for Student class
 ******************************************************/
#include "student.h"

// Parameter Constructor
Student::Student(int id, const string& name, double gpa)
: stdId(id), stdGpa(gpa)
{
    strcpy(stdName, name.c_str());
    if (stdId < 1 || stdId > 99)
    {
        cout << "Identity is out of range. Program aborted.";
        assert(false);
    }
    if (stdGpa < 0.0 || stdGpa > 4.0)
    {
        cout << "The gpa value is out of range. Program aborted.";
        assert(false);
    }
}

// Default Constructor
Student::Student()
{
}

// Destructor
Student::~Student()
{
}

// Accessor function
int Student :: getId() const
{
    return stdId;
}

// Accessor function
string Student :: getName() const
{
    return stdName;
}

// Accessor function
double Student :: getGpa() const
{
    return stdGpa;
}
```

程序 16.18 展示了将对象写入文件和从文件读取对象的应用文件。我们首先将若干对象转换为二进制数据并写入文件。然后打开同一个文件，依次读取学生对象。

### 程序 16.18 文件 app.cpp

```cpp
/**************************************************************
* The application file to write students record to a binary   *
* file and then read the records sequentially                  *
**************************************************************/
#include "student.h"

int main()
{
    // Opening File.dat for binary output
    fstream stdStrm1;
    stdStrm1.open ("File.dat", ios :: binary | ios :: out);
    if (!stdStrm1.is_open())
    {
        cout << "File.dat cannot be opened for writing!";
        assert (false);
    }

    // Instantiation of five objects
    Student std1 (1, "John", 3.91);
    Student std2 (2, "Mary", 3.82);
    Student std3 (3, "Lucie", 4.00);
    Student std4 (4, "Edward", 3.71);
    Student std5 (5, "Richard", 3.85);

    // Writing the five objects to the binary file and close it
    stdStrm1.write(reinterpret_cast<char*>( &std1), sizeof(Student));
    stdStrm1.write(reinterpret_cast<char*>( &std2), sizeof(Student));
    stdStrm1.write(reinterpret_cast<char*>( &std3), sizeof(Student));
    stdStrm1.write(reinterpret_cast<char*>( &std4), sizeof(Student));
    stdStrm1.write(reinterpret_cast<char*>( &std5), sizeof(Student));
    stdStrm1.close();

    // Opening file.dat for input
    fstream stdStrm2;
    stdStrm2.open("File.dat", ios :: binary | ios :: in);
    if (!stdStrm2.is_open())
    {
        cout << "File.dat cannot be opened for reading!";
        assert (false);
    }

    // Read Student objects, display them, and close the File.data
    cout << left << setw (4) << "ID" << " ";
    cout << setw (15) << left << "Name" << " ";
    cout << setw (4) << "GPA" << endl;

    Student std;
    for (int i = 0; i < 5; i++)
    {
        stdStrm2.read(reinterpret_cast<char*>( &std), sizeof(Student));
        cout << setw (4) << std.getId() << " ";
        cout << setw (15) << left << std.getName() << " ";
        cout << fixed << setw (4) << setprecision (2) << std.getGpa();
        cout << endl;
    }

    stdStrm2.close();
    return 0;
}
```

| 编号 | 姓名    | GPA |
|---:|---------|----:|
| 1  | John    | 3.91 |
| 2  | Mary    | 3.82 |
| 3  | Lucie   | 4.00 |
| 4  | Edward  | 3.71 |
| 5  | Richard | 3.85 |

## 随机访问

我们也可以随机读取或写入二进制文件。换句话说，不必读取所有学生的记录，我们可以使用某个学生的身份标识来读取该学生的记录。然而，这涉及两项注意事项。

首先，我们必须确保文件中存储的所有对象大小相同，以便使用 `seekg()` 和 `seekp()` 函数。对于仅包含基本数据类型数据成员的对象，每个对象的大小是其数据成员大小之和。对于 `Student` 类，表示姓名的数组大小也是固定的。

其次，在给定对象某些信息的情况下，我们必须采取一些预防措施来找到该对象的位置。例如，我们可以使用上一个示例中学生的身份标识，通过以下方式找到 Student 对象的位置：

```cpp
seekg ((id − 1) * sizeof (Student))
```

但如果身份标识不是从 1 开始，我们必须将身份标识转换为学生记录编号。

## 16.4 字符串流

字符串流使用三个类：*istringstream*、*ostringstream* 和 *stringstream*。这些类用于从字符串输入数据或向字符串输出数据。它们分别继承自 *istream*、*ostream* 和 *iostream*。除了少数例外，其超类中讨论的所有成员函数都可以在这些类中使用，并且这些类还可以增加更多类。字符串流类定义在 `<sstream>` 头文件中，使用它们时必须在程序中包含该头文件。

> 要使用字符串流，我们需要 `<sstream>` 头文件。

字符串流的源或目标不同于控制台流或文件流的源或目标。在控制台流中，源或目标是程序外部的物理设备。在文件流中，源或目标是文件，即存在于程序外部的实体。在字符串流中，源或目标实际上是程序本身内部的字符串。换句话说，我们从程序中已有的字符串读取；我们向程序中的字符串写入。为清晰起见，在本节使用的图中，我们将源或汇表示为程序外部的字符串，但必须记住它是程序的一部分。

我们不能打开或关闭这些流，因为连接到这些流的源或汇实体不是外部的；它们是在程序内部创建和销毁的。因此，这些流没有 *open()* 或 *close()* 函数。

> 字符串流没有定义 *open()* 和 *close()* 函数。

### 16.4.1 实例化

与文件流类似，每个字符串流都使用构造函数进行实例化。表 16.11 展示了 *istringstream*、*ostringstream* 和 *stringstream* 类的构造函数；我们展示了打开模式的默认值。

每个构造函数都会实例化一个 *istringstream*、*ostringstream* 或 *stringstream* 类型的对象，并将该对象连接到作为第一个参数定义的字符串对象。注意，必须包含一个字符串对象，但它可以是空字符串。
