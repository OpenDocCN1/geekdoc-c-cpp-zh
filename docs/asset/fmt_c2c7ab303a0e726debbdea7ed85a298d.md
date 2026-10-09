
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
myFile << "C++ is powerful." << endl;

myFile.close();

} else {

cout << "无法打开文件" << endl;

}

return 0;

}
```

一旦程序成功编译，**output.txt** 文件可以找到。**output.txt** 的内容如下：

Hello, World!
C++ is powerful.

## 读取文件

我们可以通过流提取运算符 (`>>`) 从文件中读取信息，正如我们使用该运算符从键盘上输入信息一样。唯一的区别在于我们使用 `ifstream` 或 `fstream` 对象而不是 `cin` 对象。程序 13.4 显示了如何读取文件：

```cpp
// 程序 13.4
// 读取文件
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
int main() {
string readline;
ifstream myFile("input.txt");
if (myFile.is_open()) {
while (getline(myFile, readline)) {
cout << readline << endl;
}
myFile.close();
} else {
cout << "无法打开文件" << endl;
}
return 0;
}
```

## 检查标志位

某些成员函数用于检查流的具体状态，它们都返回表 13.3 所示的布尔值。

表 13.3：检查状态的函数。

| 函数 | 描述 |
| --- | --- |
| bad() | 读取或写入操作失败时返回 true。例如，尝试写入未打开的文件或写入的设备没有剩余空间。 |
| fail() | 不仅在 `bad()` 的情况下返回 true，而且当发生格式错误时也返回 true，例如在尝试读取整数时提取了字母字符。 |
| eof() | 当为了读取打开的文件到达末尾时返回 true。 |
| good() | 这是最通用的状态标志。当上述任何一个函数返回 true 时，它返回 false。 |
| clear() | 可用于重置标志位 |

程序 13.5 显示了一个以读写模式打开的文件示例。在执行过程中，程序要求用户输入存储在 **input.txt** 中的信息。然后，程序从文件中读取信息并输出到屏幕上。

```cpp
// 程序 13.5
// 读取和写入文件
#include <fstream>
#include <iostream>
using namespace std;
int main()
{
char indata[100];
// 以写入模式打开文件。
ofstream outfile;
outfile.open("input.dat");
cout << "写入文件：input.dat" << endl;
cout << "输入城市名称：";
cin.getline(indata, 100);
// 将输入的数据写入文件。
outfile << indata << endl;
outfile.close();
// 以读取模式打开文件。
ifstream infile;
infile.open("input.dat");
cout << endl << "从文件读取：input.dat" << endl;
infile >> indata;
// 将数据写入屏幕。
cout << indata << endl;
}
```

```cpp
// 关闭已打开的文件。
infile.close();
return 0;
}
```

程序 13.5 的结果所示：

写入文件：input.dat
输入你的城市名称：北京
从文件读取：input.dat
北京

## 13.4 复习题

- 1. 解释以下内容：(a) 输入流 (b) 输出流以及 (c) 缓冲区。
- 2. 关于 (a) `cin`、(b) `cout`、(c) `cerr` 和 (d) `clog` 写一个简短笔记。
- 3. 描述与文件相关的类：(a) `ofstream`、(b) `ifstream` 和 (c) `fstream`。
- 4. 讨论二进制文件和文本文件之间的区别。
- 5. 写一个程序从文件 `input.txt` 读取信息，并写入另一个名为 `output.txt` 的文件中。
- 6. 编写一个程序输入两个文件并将内容合并到一个输出文件中。

input1.txt

![](img/7f9692ccbd64225fae08eb0ce84bee5_265_0.png)

input2.txt

![](img/7f9692ccbd64225fae08eb0ce84bee5_265_1.png)

output.txt

![](img/7f9692ccbd64225fae08eb0ce84bee5_265_2.png)

# 14 类与对象

若穷极极致，必得智慧。
拥有智慧，方能选择。
程毅

## 14.1 引言

在本章中，我们将学习面向对象编程最重要的部分，即类和对象。常见的面向对象编程（OOP）语言是 C++ 和 Java。像 C、PASCAL、FORTRAN 等语言通常被称为面向过程的或结构化编程语言。近年来，许多程序员发现 OOP 是比面向过程编程更好的方法。

软件本质上是许多相互关联程序的集合，这些程序反过来由数据和方法组成。在传统的编程语言中，数据和方法是松散结合的。因此，很难找到哪些数据属于哪个函数？此外，传统的面向过程的语言无法表示实时实体或情况。实时实体的几个例子包括银行、客户、大学和学生。OOP 通过通过对象和类（面向对象编程中最重要的两个概念）表示实时实体的有效方法解决了所有这些问题。每个读者或程序员都必须意识到这些概念。

## 14.2 对象定义

什么是对象？

对象是 OOP 的核心特征。如果我们观察周围环境，可能会发现许多现实世界的对象，如狗、包、电脑、笔、电话等。这些对象可能是有形的，也可能是无形的。如果我们分析所有这些对象，会发现它们具有两个共同特征：数据和行为。让我们以狗对象为例。与此对象相关的数据是名称、年龄、身高重量。除了这些数据外，狗可能表现出一些行为，如行走、吠叫、咬（有时！）、吃东西等等。

总的来说，每个对象都有两个基本特征：数据和行为。对象的数据基本上由数据类型表示，相关的行为在 OOP 中由方法表示。对象是一个既有数据又有方法的软件实体。

### 对象在软件开发中有什么用？

我们可能会思考一个问题：对象的概念在软件开发中有什么用？为了回答这个问题，我们必须理解软件的应用场景。如今，软件是为各种应用设计的，例如学生数据管理、银行应用、客户交易、铁路预订等。所有这些软件都使用实体，如客户、银行、交易、预订等。所有这些实时实体都表示为对象。因此，对于程序员和客户来说，编写易于的程序是非常容易的。

## 14.3 类定义

### 什么是类？

在 14.2 节中，我们分析了对象的含义。**类**是用于创建对象的通用术语。OOP 中的类在单一名称下通过数据和行为表示现实世界的实体。例如，陈先生是一个学生，这意味着陈先生属于学生类。在这个例子中，陈先生是一个对象，而学生是一个类。一个类可以有很多对象。让我们来看这句话：

- 陈先生、芳小姐和布先生都是学生。

从上述语句中我们推断出什么？它表明陈、芳、布都属于学生类。这清楚地表明类负责创建一个或多个对象。现在，让我们比较以下语句：

```cpp
int Chen_Weight, Fang_Weight, Bruce_weight;
Student Chen, Bruce;
```

如果我们比较上述两个语句，它们看起来相似。在第一条语句中，三个变量都是整数。在第二条语句中，三个对象都属于 Student 类。因此，类就像是创建许多对象的模板或模型。通常，对象是类的实例。在 14.2 节中，我们学习了对象拥有数据和方法。我们知道陈、芳、布都是学生，共享许多以数据和方法表示的特征并在类中定义。因此，类用于定义所有对象共有的数据和方法。所以，C++ 类是数据和方法（函数）的集合，创建了一种新的数据类型，用于创建该类的对象。通常，类的定义语法如下：

```cpp
class class_name
{
public:
<variable declaration> // 数据成员
<method declaration> // 成员函数
private:
<variable declaration> // 数据成员
<method declaration> // 成员函数
protected:
<variable declaration> // 数据成员
<method declaration> // 成员函数
};
```

如所示，C++ 中有不同的关键字作为访问修符：`public`、`private` 和 `protected`。它们指导访问类成员的规则，例如类内部的函数（方法）或数据。私有访问修符支持 OOP 的数据隐藏功能。类的私有成员只能在类外部访问。另一方面，公共成员可以在类外部访问。这些访问修符后面跟着一个冒号。如果没有提到访问修符，则默认成员函数或数据变为私有。关于相同的更多细节请见 14.7 节。类定义以分号结束。

```cpp
class Student
{
public:
int student_number;
char name[20];
int marks;
char university_name[40];
void get_name_number()
{
cout << "Student Number=" << student_number << endl;
cout << "Student Name=" << name << endl;
}
void get_marks()
{
cout << "Student Marks=" << marks << endl;
}
};
```

在创建对象之前定义类。这意味着类定义作为以后创建对象的模板。例如，下面的

`Student Fang;`

声明了一个 `Student`类型的对象 `Fang`。在这里，`Fang` 是 `Student`类的实例。我们也可以创建多个 `Student` 类型的对象：

`Student Fang, Wang;`

每个对象都为它们的成员分配了独立的内存。因此，我们可以为每个对象的成员存储不同的值。

### 如何访问数据和方法？

在之前的示例中，`student_number`、`name`、`marks` 是类的数据成员，而 `get_name_number()` 和 `get_marks()` 是类的方法成员。为了使用这些数据和方法成员，我们使用 `.` 运算符。以下语句将 18976587 赋值给 `Fang` 对象的 `student_number` 数据：

```cpp
Fang.student_number = 18976587;
```

同样，我们可以调用 `Fang` 对象的方法成员：

```cpp
Fang.get_marks();
```

之前的语句调用了 `Fang` 对象的 `get_marks()` 方法。程序 14.1 完全总结了前面的类和对象，并且使用了数据和方法成员。类定义总是写在 `main()` 函数之前。这是因为对象必须在 main 中使用之前定义。在 main 之后定义类会导致错误。

```cpp
// 程序 14.1
// 理解类和对象的程序
#include <iostream>
#include <cstring>
using namespace std;
```

```cpp
public:
int student_number;
char name[20];
int marks;
char university_name[40];
```

```cpp
void get_name_number()
{
cout << "Student Number=" << student_number << endl;
cout << "Student Name=" << name << endl;
}
```

```cpp
void get_marks()
{
cout << "Student Marks=" << marks << endl;
}
```

```cpp
int main()
{
Student Fang;
Fang.student_number = 18976587;
strcpy(Fang.name,"Xiaong Dong Fang");
Fang.marks = 87;
Fang.get_name_number();
Fang.get_marks();
return 0;
}
```

程序 14.1 的结果所示所示：

Student Number=18976587
Student Name=Xiaong Dong Fang
Student Marks=87

### 在 C++ 中比较 OOP 程序与非 OOP 程序

程序 14.2 和 14.3 演示了不使用对象（或类）和使用对象（或类）编写的方法。理解 OOP 程序与非 OOP 程序之间的区别非常有用。程序 14.2 是一个简单的程序，用于在不用对象的情况下相两个数字。

```cpp
// Program 14.2
// 不使用对象相两个数字的程序
#include<iostream>
using namespace std;
int main()
{
int a = 99,b = 88;
int c = a + b;
cout << "Result=" << c << endl;
return 0;
}
```

程序 14.2 的结果所示所示：

Result=187

现在，我们将使用 C++ 中的对象和类将程序 14.2 重写为程序 14.3。在这里，我们需要创建一个类，并为该类创建一个对象。程序 14.3 如下所示：

```cpp
// Program 14.3
// 使用类和对象相两个数字的程序
#include<iostream>
using namespace std;
class Add_Two
{
public:
int a,b,c;
void Result()
{
c = a + b;
cout << "Result=" << c << endl;
}
};
int main()
{
Add_Two TWOADD;
//设置字段
TWOADD.a = 99;
TWOADD.b = 88;
TWOADD.Result();
return 0;
}
```

程序 14.3 的结果所示所示：

Result=187

## 14.4 重载方法

一个类可以有许多方法，每个方法都有零个或多个参数。可以编写多个同名的方法吗？答案是肯定的。一个类可以有多个同名的方法。这个概念被称为方法重载。要重载一个方法，必须满足以下条件：

- 1. 方法名应该相同。
- 2. 方法应该具有不同的参数列表或签名。
- 3. 方法应该在同一个类或子类中。

方法的签名由方法名和类型类型参数的数据决定。以下三个方法具有三个不同的签名：

```cpp
void oneMethod(int a, int b);
void oneMethod(int a, float b);
void oneMethod(int a, float b, long c);
```

如果多个方法具有相同名称但不同的签名，我们称该方法是被重载的，并这些这些重载方法。程序 14.4 演示了此方面的例子。

```cpp
// Program 14.4
// 理解重载方法的程序
#include<iostream>
using namespace std;
class Overload
{
public:
int add(int a,int b)
{
return (a+b);
}
float add(float a,float b)
{
return (a+b);
}
double add(double a,double b)
{
return (a+b);
}
};
int main()
{
Overload SAME;
int a = 10;
int b = 20;
float c = 23.75F;
float d = 78.987F;
double e = 23456.89645;
cout << "Integer Addition : a + b = " << SAME.add(a,b) << endl;
cout << "Float Addition : a + b = " << SAME.add(c,d) << endl;
cout << "Double Addition : a + b = " << SAME.add(e,f) << endl;
return 0;
}
```
*(注：原文代码中 f 变量未定义，此处翻译保留代码逻辑)*

程序 14.4 的结果所示所示：

```
Integer Addition: a + b = 30
Float Addition: a + b = 102.737
Double Addition: a + b = 23480.89645
```
