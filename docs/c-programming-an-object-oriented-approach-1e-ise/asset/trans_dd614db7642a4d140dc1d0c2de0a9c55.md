
**表16.11** 三个字符串流类的构造函数

```cpp
istringstream(const string str, ios::openmode mod = ios::in);
ostringstream(const string str, ios::openmode mod = ios::out);
stringstream(const string str, ios::openmode mod = ios::in | ios::out);
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_770_0.png)

> **注意：**
> 
> 当字符串连接到流时，标记位于缓冲区的开头。
> 标记会随每次读取或写入操作或其他成员函数而移动。

**图16.13** 连接到字符串和程序的字符串流对象

图16.13以图形方式显示了三个字符串流对象。

## 成员函数

*istringstream* 类继承超类 *istream* 中定义的所有顺序访问和随机访问成员函数（*open* 和 *close* 函数除外）。*ostringstream* 也是如此，但它继承自超类 *ostream*。*stringstream* 类也是如此，但它继承自超类 *ostream*。

此外，每个类都提供了新成员函数 *str* 的两个版本。第一个版本替换连接到流的字符串；第二个版本返回连接到流的字符串的副本。表16.12显示了这些函数的原型。

程序16.19是一个简单的字符串示例。在第一部分中，我们创建一个连接到字符串的 *istringstream* 对象并打印该字符串。然后我们更改连接到同一个 *istringstream* 的字符串并打印该字符串。在第二部分中，我们对 *ostringstream* 做同样的操作。

**表16.12** str 函数的两个版本

```cpp
void str(string str);       // Connect the parameter to the host object
string str() const;         // Returns the string connected to the host object
```

## **程序16.19** 测试字符串流类

```cpp
/**************************************************************
 * A program to show how to use string stream classes          *
 **************************************************************/
#include <iostream>
#include <string>
#include <sstream>
using namespace std;

int main ()
{
    // Using istringstream object
    istringstream iss ("Hello friends!");
    cout << iss.str () << endl;
    iss.str ("Hello world!");
    cout << iss.str () << endl;
    // Using ostringstream object
    ostringstream oss ("Bye friends!");
    cout << oss.str () << endl;
    oss.str ("Bye world!");
    cout << oss.str () << endl;
    return 0;
}

Run:
Hello friends!
Hello world!

Bye friends!
Bye world!
```

## 16.4.2 应用：适配器

字符串流类最常见的应用是充当 string 类的适配器。众所周知，string 类没有构造函数来包装基本类型的值（char 除外）并由此生成字符串。它也没有成员函数来解包字符串并从中取出基本数据类型的值。

在编程中，我们有时需要将基本数据类型转换为字符串，并将字符串转换为基本数据类型。为此，我们使用 stringstream 类的对象作为适配器。

在包装时，我们将基本数据类型插入 ostringstream 对象，然后将 ostringstream 对象转换为 string 对象。在解包时，我们将字符串转换为 istringstream 对象，并从 istringstream 对象中提取基本数据类型。这两种操作如图16.14所示。

![](img/d68f6199646ca63591a6d8419e0ed4ba_772_0.png)

我们可以创建一个函数模板，将任何基本数据类型转换为字符串。我们还可以创建一个函数模板，返回嵌入在字符串中的基本数据类型。我们将这两个模板函数包含在名为 convert.h 的头文件中，如程序16.20所示。请注意，在第13行我们必须使用特化，如第15章所述，因为模板函数 `toData` 仅将模板类型用作返回类型。没有特化，模板函数无法检测返回类型。

## **程序16.20** 文件 convert.h

```cpp
/*************************************************************
 * The header file defines two template functions. The first    *
 * inserts a fundamental type into a string. The second extracts *
 * a fundamental type embedded in a string.                     *
 *************************************************************/
#ifndef CONVERT_H
#define CONVERT_H
#include <iostream>
#include <string>
#include <sstream>
using namespace std;

// toString function changes any data type to string
template <typename T>
string toString (T data)
{
    ostringstream oss ("");
    oss << data;
    return oss.str ();
}
// toData function takes out the data embedded in a string
template <typename T>
T toData (string str)
{
    T data;
    istringstream iss (str);
    iss >> data;
    return data;
}
#endif
```

程序16.21演示了 *convert.h* 模板函数的用法。

## **程序16.21** 文件 app.cpp

```cpp
/****************************************************************
 * A simple application program that uses toString and toData    *
 * template functions                                           *
 ****************************************************************/
#include "convert.h"

int main()
{
   // Converting integer 12 to a string
   string str = toString(12);
   cout << "String: " << str << endl;
   // Converting string "15.67" to double
   double data = toData<double>("15.67");
   cout << "Data: " << data;
   return 0;
}
```

**运行：**

String: 12

Data: 15.67

# 16.5 格式化数据

在第3章中，我们讨论了操纵器并使用了其中一些。操纵器使用 *ios* 类中定义的格式化数据成员（格式化标志、格式化字段和格式化变量）。由于所有流类都继承自 *ios* 类，因此它们都继承这些数据成员以及用于设置和取消字段、将值存入变量的相应成员函数。要创建自定义操纵器，我们必须理解如何直接使用这些*标志*、*字段*和*变量*。

## 16.5.1 直接使用标志、字段和变量

理解如何使用标志、字段和变量，将有助于我们在本章后面创建自定义操纵器。

### 格式化标志

如表16.13所示，*ios* 类定义了一个名为 *fmtflags* 的类型，该类型可以取七个值中任意值的组合。每一位都可以设置（值为1）或取消（值为0）。这些标志彼此独立，我们可以使用其中一个或多个来格式化数据。

我们可以使用 *setf()* 或 *unsetf()* 函数来设置或取消它们，如表16.14所示。

### 格式化字段

*ios* 类还定义了一组三个用于格式化数据的字段。每个字段组有两个或三个字段，可以互斥地设置或取消。一次只能设置一个位。表16.15显示了此类别中定义的三个字段。

**表16.16 设置或取消字段的成员函数**

| 成员函数 | 描述 |
|---|---|
| `fmtField ios::setf(addfield, field)` | 它设置相应字段 |
| `fmtField ios::unsetf(field)` | 它取消相应字段 |

**表16.17 设置和取消变量字段**

| 变量 | 类型 |
|---|---|
| `width` | `int` |
| `precision` | `int` |
| `fill` | `char` |

| 成员函数 | 描述 |
|---|---|
| `int ios::width(int n)` | 设置一个值要使用的位数。 |
| `int ios::width()` | 将宽度字段重置为0。 |
| `int ios::precision(int n)` | 设置小数点后的位数。 |
| `int ios::precision()` | 取消精度字段。 |
| `int ios::fill(char c)` | 设置用于填充空位的字符类型。 |
| `int ios::fill()` | 取消填充字段。 |

每组中的字段不是独立的，一次只能设置其中一个。默认设置以颜色显示，但请注意，*floatfield* 没有默认值（如果没有显式选择，系统会选择最合适的值）。

设置这些字段中的任何一个，其方法都与用于 *fmtflags* 的方法不同，因为它保证每个类别中只设置一个值（表16.16）。

要设置字段，我们必须使用两个参数。第二个参数（field）取消该字段组中的所有字段；然后第一个参数设置所需字段。

### 格式化变量

表16.17中显示的格式化变量名为 *width*（类型为 *int*）、*precision*（类型为 *int*）和 *fill*（类型为 *char*）。

这些格式化变量用于定义为一个值预留多少位、小数点后预留多少位，以及应使用什么字符填充未使用的位置。有六个成员函数用于设置和取消这些标志，如表16.17所示。请注意，如果未设置 *fill* 字段，则填充字符默认为空格。

程序16.22展示了如何直接格式化三个数据项，其类型分别为 *boolean*、*integer* 和 *floating-point*。本程序有两个目标：(1) 表明可以使用格式化标志、字段和变量来格式化数据；(2) 表明这个过程有多么冗长和复杂。稍后，我们将展示可以使用操纵器实现相同目标。

## 程序16.22 打印三个数据项

```cpp
/*********************************************************
 * A program to show how to format three data types using the
 * formatting flags, fields and variables
 *********************************************************/
#include <iostream>
```
