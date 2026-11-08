

```text
Enter a number: 33
Enter a number: 83
Enter a number: 98
Enter a number: 78
Enter a number: 123
Enter a number: 67
Enter a number: 09
Enter a number: 56
Enter a number: 23
Enter a number: 99
The average of the array elements are 66.9
```

现在我们来学习字符串。

## 字符串

C++ 有两种字符串：C 字符串和标准 C++ string 类。在 C 语言中使用的 C 字符串，是以 NULL '\0' 字符结尾的字符数组。另一方面，标准 C++ 包含一个名为 string 的新类。这个类在多个方面改进了传统的 C 字符串。例如，我们不必担心创建大小合适的数组来保存字符串变量，因为 C++ string 类会处理内存管理。此外，string 类提供了运算符重载的好处，这赋予了旧运算符新的含义。例如，在 string 类中，+ 运算符被重载，因此当我们编写以下语句时，+ 运算符充当连接运算符：

```cpp
S1 = S2 + S3;
```

在上述语句中，这三个都是 string 类的对象。在 C 中，可以使用名为 strcat 的库函数完成同样的事情。代码清单 12.3 探讨了 string 类的一些特性：

### 代码清单 12.3：展示 string 类的特性

```cpp
1: // Demonstrating string classes in C++
2: #include <iostream>
3: #include <string>
4: using namespace std;
5:
6: int main ()
7: {
8:     string S1("Tom");                 //Initialization
9:     string S2 = "Jerry";              //Initialization
10:    string S3;
11:
12:    S3 = S1;                          //Assignment
13:    cout<< "S3 = "<<S3<<endl;
14:
15:    S3 = S1 + " and ";                //Concatenation
16:    S3 += S2;                         //Concatenation
17:    cout<< "S3 = "<<S3<<endl;
18:
19:    return 0;
20: }
```

在代码清单 12.3 中，我们定义了三个 string 类的对象：S1、S2 和 S3。首先，我们使用两种不同的方式初始化了 S1 和 S2。然后，在第 12 行完成了从 S1 到 S3 的赋值，这解释了为什么程序会打印 Tom。连接方法也通过 + 和 += 运算符执行，字符串 Tom and Jerry 在 S3 中构造出来。以下是上述程序的输出：

```text
Tom
Tom and Jerry
```

表 12.5 展示了 C++ 中 string 类的各种成员函数：

**表 12.5：string 类的成员函数**

| 成员函数 | 描述 |
|---|---|
| size | 返回字符串对象的长度 |
| length | 返回字符串对象的长度 |
| max_size | 返回字符串的最大大小 |
| resize | 调整字符串对象的大小 |
| capacity | 返回已分配存储的大小 |
| reserve | 请求更改容量 |
| clear | 清空字符串 |
| empty | 测试字符串是否为空 |
| operator [] | 获取字符串中的字符 |
| at | 获取字符串中的字符 |
| operator += | 将字符串追加到另一个字符串末尾 |
| append | 将字符串追加到另一个字符串末尾 |
| push_back | 将字符追加到字符串 |
| assign | 为字符串分配内容 |
| insert | 将字符插入字符串 |
| erase | 从字符串中删除字符 |
| replace | 替换字符串的一部分 |
| swap | 交换两个字符串的内容 |
| c_str | 获取等效的 C 字符串 |
| data | 获取字符串数据 |
| get_allocator | 获取分配器 |
| copy | 从字符串复制字符序列 |
| find | 在字符串中查找内容 |
| rfind | 查找内容在字符串中最后出现的位置 |
| find_first_of | 在字符串中查找字符 |
| find_last_of | 从末尾在字符串中查找字符 |
| find_first_not_of | 查找字符串中不存在的字符 |
| find_last_not_of | 从末尾查找字符串中不存在的字符 |
| substr | 生成子字符串 |
| compare | 比较两个字符串 |
| begin | 返回指向字符串开头的迭代器 |
| end | 返回指向字符串末尾的迭代器 |
| rbegin | 返回指向反向开头的迭代器 |
| rend | 返回指向反向末尾的迭代器 |

现在我们来学习 C++ 中的结构体。

## 结构体

结构体是简单变量的集合，在 C++ 中表示为单个用户定义的数据类型。结构体中的变量可以是基本数据类型（int、char 或 float）和用户定义的数据类型（结构体或枚举）。在 C++ 基础中讲解结构体的主要原因是，结构体的语法几乎与 C++ 中的类相同。结构体是数据的集合；而类是数据和函数的集合。代码清单 12.4 展示了 C++ 中结构体的使用：

### 代码清单 12.4：展示 C++ 中结构体的使用

```cpp
1: // Demonstrating user-defined structures in C++
2: #include <iostream>
3: using namespace std;
4:
5: struct employee_data
6: {
7:     char        employee_name[30];
8:     int         age;
9:     double      salary;
10: };
11:
12: int main ()
13: {
14:     struct employee_data emp;
15:
16:     cout<<"Enter Employee Name: ";
17:     cin >> emp.employee_name;
18:     cout<<"Enter Employee Age: ";
19:     cin >> emp.age;
20:     cout<<"Enter Employee Salary: ";
21:     cin >> emp.salary;
22:
23:     cout    <<"\nEmployee "<<emp.employee_name<<" is "
24:             <<emp.age<<" years old with Rs "<<emp.salary<<"\n";
25:
26:     return 0;
27: }
```

在代码清单 12.4 中，第 1 行是注释；而第 2 行和第 3 行是预处理指令。我们从第 5 行到第 10 行开始声明结构体。在程序中，声明了 employee_data 结构体，其成员为 employee_name、age 和 salary。请注意，结构体的所有声明都必须以分号结尾，如第 10 行所示。结构体声明仅作为创建 employee_data 类型变量的蓝图。该声明本身既不定义任何变量，也不在内存中预留任何空间。它仅仅规定了结构体变量在定义时应具有的形式。

main() 函数的第一条语句表示定义了一个 employee_data 类型的变量 emp。该定义为结构体类型变量 emp 在内存中预留 42 字节空间，其中包括 30 字节用于姓名、4 字节用于年龄、8 字节用于薪资（假设我们在 32 位机器上工作）。然而，有时该定义会占用更多内存以对齐数据字节，具体取决于编译器；这一概念称为字节对齐。

字节对齐是一个非常有趣的特性。大多数 16 位和 32 位处理器不允许将字存储在任意偏移处。因此，作为微处理器设计的一部分，通过利用字节对齐来实现这一点，处理器可以一次性从内存单元读取数据并向内存单元写入数据。编译器也遵循目标微处理器施加的字节对齐限制。这意味着编译器必须向结构体中填充额外字节，以免违反目标微处理器施加的任何限制。考虑以下结构体：

```cpp
struct Message
{
    short opcode;
    char subfield;
    long message_length;
    char version;
    short destination_processor;
};
```

对于上述结构体，字节对齐后的实际结构体如下：

```cpp
struct Message
{
    short opcode;
    char subfield;
    char pad1;          // Pad to start the long word at a 4 byte boundary
    long message_length;
    char version;
    char pad2;          // Pad to start a short at a 2 byte boundary
    short destination_processor;
    char pad3[4];       // Pad to align the complete structure to a 16 byte boundary
};
```

尽管我们展示了一个字节对齐的初步示例，但它可能因编译器而异。然而，字节对齐的基本思想是相同的。

在代码清单 12.4 的第 16、18 和 20 行，我们从用户那里提示输入员工的个人信息，并将其保存到 emp 变量的数据成员中。这意味着在第 17 行输入的员工姓名会保存到 emp.employee_name 中；在第 19 行输入的员工年龄会保存到 emp.age 中；在第 21 行输入的员工薪资会保存到 emp.salary 中。因此，每当我们访问结构体类型变量的内部数据成员时，都可以使用点运算符。然而，如果我们处理的是 struct employee_data 类型的指针，例如，

```cpp
struct employee_data *ptr;
```

那么访问员工信息要使用间接运算符，即 ->。在这种情况下，我们可以通过 ptr->employee_name、ptr->age 和 ptr->salary 访问信息。

以下是代码清单 12.4 的输出：

```text
Enter Employee Name: John
Enter Employee Age: 40
Enter Employee Salary: 16000
Employee John is 40 years old with Rs 16000 salary.
```

现在，我们学习如何同时声明和定义结构体变量。考虑以下代码片段：

```cpp
1:struct employee_data
2:{
3:    char employee_name[30];
4:    int age;
5:    double salary;
6:}emp;
```

在上述代码片段中，第 6 行包含结构体变量 emp 的定义。这就是我们如何将结构体变量的声明和定义结合起来的方式。

