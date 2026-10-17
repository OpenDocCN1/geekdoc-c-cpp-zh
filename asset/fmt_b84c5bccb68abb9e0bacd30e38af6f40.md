
```cpp
int main()
{
  // 与示例 6.20 相同
}
```

程序的运行结果如下。

```
Please enter the number of points:2

Default Constructor called.

Default Constructor called.

Default Constructor called.

Default Constructor called.

Copy of pointsArray1:

Point_0 of array2: 5, 10

Point_1 of array2: 15, 20

After the moving of pointsArray1:

Point_0 of array2: 25, 30

Point_1 of array2: 35, 40

Deleting...

Destructor called.

Deleting...

Destructor called.

Destructor called.

Destructor called.

Destructor called.
```

从运行结果可以看出，实现了深拷贝。在 `pointsArray1` 中移动不再影响 `pointsArray2`，且分别释放 `pointsArray1` 和 `pointsArray2` 的内存空间不会导致错误。深拷贝的过程如图 6.11 所示。

![](img/5618306d085ac1bac8275d6c4c5bbf2a_261_0.png)

**图 6.11：** 深拷贝示意图。

## 6.5 字符串

我们在第2章中介绍过，字符串常量是用一对双引号括起来的序列。例如，“abcd”、“China”和“This is a string”都是字符串常量。在内存中，字符串常量根据字符串字符的顺序存储，每个字符占用一个字节；末尾添加 `'\0'` 作为结束标记。

然而，在 C 中，字符串变量不是 C++ 的基本数据类型。那么如何存储和处理字符串呢？C 使用字符数组来存储字符串，C++ 仍然可以使用这种方法。此外，标准 C++ 定义了 `string` 类。我们将在本节介绍这两种方法。

### 6.5.1 使用数组存储和处理字符串

#### 1. 字符数组的声明和引用

字符数组的声明和引用方法与其他类型的数组相同。可以通过下面的示例来解释。

示例 6.22：输出字符串。

```cpp
//6_22.cpp
#include<iostream>
using namespace std;
int main()
{
    static char c[10]=
    {'I', ' ', 'a', 'm', ' ', 'a', ' ', 'b', 'o', 'y'};
    // 一维字符数组的声明和初始化
    int i;
    for(i=0;i<10;i++) //逐个输出字符数组中的元素
        cout<<c[i];
        cout<<endl;
}
```

结果是：

| I am a boy |

示例 6.23：输出菱形图形。

```cpp
//6_23.cpp
#include<iostream>
```
# 246 6 数组、指针与字符串
using namespace std;
int main()
{
/* 二维字符数组的声明和初始化，
elements[] 未初始值的元素都被设置为 0*/
static char diamond[][5]={'*',' ',' ','','*'},{'*',' ',' ','','*'},
{'*',' ',' ','','*'}, {'*',' ',' ','','*'}, {'*',' ',' ','','*'};
int i,j;
for (i=0;i<5;i++)
// 逐个输出二维字符数组的元素
{
for(j=0;j<5 && diamond[i][j]!=0;j++)
cout<<diamond[i][j];
cout<<endl;
}
}
```

结果是：

+   * *

*

* *

**

#### 2. 使用字符数组存储字符串

在示例 6.22 和示例 6.23 中，我们逐个处理数组元素，数组中的字符是独立的。末尾没有 `'\0'`，因此这不构成 C++ 字符串。如果在字符数组初始化的末尾加上 `'\0'`，就会得到一个 C++ 字符串。

## 6.5 字符串 — 247

```cpp
char c[]="China";cout<<c;
```

在输入/输出整个字符串时，我们应该注意：

- 1. 输出的字符不包含 `'\0'`；
- 2. 我们使用字符数组名来指定要输出的字符串，遇到 `'\0'` 时输出结束；
- 3. 在输入多个字符串时，我们应该用空格隔开；输入单个字符串时，字符串内部不应空格。

例如，程序中有后续的语句：

```cpp
static char str1[5],str2[5],str3[5];cin>>str1>>str2>>str3;
```

如果我们在运行时输入以下数据：

```
How are you?
```

内存中变量的状态如下：

| str1: | H | o | w | \0 |

| str2: | a | e | \0 |

| str3: | y | o | u | ? | \0 |

如果我们将代码修改为：

```cpp
static char str[13];cin>>str;
```

并在运行时输入以下数据：

```
How are you?
```

内存中变量 `str` 的内容为：

| str: | H | o | w | \0 |

由于读取在遇到空格时停止，因此我们只能接收到第一个单词。

我们可以使用字符串处理系统函数来处理字符串，例如 `strcat`（连接）, `strcpy`（复制）, `strcmp`（比较）, `strlen`（获取长度）, `strl`（转为小写），以及 `strupr`（转为大写）。在使用这些函数之前，我们应该在源文件中包含头文件 `cstring`。读者可以在编译系统的帮助下找到这些函数的说明。

### 6.5.2 string 类

使用数组存储字符串并调用系统函数处理字符串是不方便的。此外，数据与函数处理数据的分离并不符合面向对象方法的要求。因此，C++ 标准库在 C++ 中引入了面向对象的字符串的概念，定义了 `string` 类，它提供了处理字符串的必要操作。使用 `string` 类时应包含相应的头文件。`string` 类封装了字符串的属性，并提供了一系列函数来访问这些属性。属性或类的数据组件包含：

- 字符序列
- 字符序列的大小或长度
- 字符类型
- 字符特性
- 字符的大小
- 分配器
- 迭代器（我们将在第 10 章详细介绍）

`string` 类还有许多与字符串操作相关的函数，包括：

- 搜索
- 赋值
- 连接
- 附加

这里我们简要介绍 `string` 类的构造函数以及几个常用的成员函数和操作。为了简单起见，函数原型进行了简化，与头文件中的形式不同。更多详细信息，读者可以参考编译系统的在线帮助。

#### 1. 构造函数的原型

```cpp
string(); //默认构造函数，创建一个长度为 0 的字符串
string(const string& rhs); //拷贝初始化构造函数
string(const char *s);
//使用指针 s 指向的字符串来初始化
// string 类的对象
string(const string& rhs, unsigned pos, unsigned int n);
//从字符串 rhs 的位置 pos 处获取 n 个字符
//初始化 string 类的对象
// 注意：字符串中第一个字符的位置为 0
string(const char *s, unsigned int n);
```
```cpp
//使用指针 s 指向的字符串中的前 n 个字符
//初始化 string 类的对象
string(unsigned int, char c);
//将参数 c 指定的字符重复 n 次
//初始化 string 类的对象
```

#### 2. 常用成员函数简介

`string` 类有许多成员函数，包括许多重载函数。这里我们只列出一部分。读者可以参考在线帮助了解其他函数。

```cpp
int length() const;
//返回字符串的字符数
```
```cpp
int find(const string& str);
//在字符串中查找 str出现的位置
```
```cpp
string& assign(const char*);
//赋值这个字符串
```
```cpp
int compare(const string& str);
//比较这个字符串
```
假设有两个字符串 `s1` 和 `s2`；它们的比较规则如下：

- a) 如果 `s1` 和 `s2` 的长度相同，返回 0。
- b) 如果 `s1` 的长度小于 `s2`，返回负值。
- c) 如果 `s1` 的长度大于 `s2`，返回正值。

```cpp
string& append(const char*);
//在字符串末尾附加 s
```
```cpp
string& insert(unsigned int pos, const char* s);
//在字符串的 pos 处插入 s
```
```cpp
string substr(unsigned int pos, unsigned int n);
//从字符串的 pos 处截取 n 个字符
```
```cpp
void swap(string& str);
//交换这个字符串
```

## 6.1 字符串运算符

| 运算符 | 示例 | 注释 |
| :--- | :--- | :--- |
| + | s+t | 连接 s 和 t |
| = | s=t | 赋值给 s |
| += | s+=t | 更新 s |
| == | s1==t | 判断 s1 是否等于 t |
| != | s1!=t | 判断 s1 是否等于 t |
| <= | s1<=t | 判断 s1 是否小于等于 t |
| > | s1>t | 判断 s1 是否大于 t |
| >= | s1>=t | 判断 s1 是否大于等于 t |
| [] | s[i] | 访问下标 i 的字符 |

## 6.6 程序实例 – 人员管理系统

在前两个章节中，我们以一个小型公司的人员管理程序为例，说明了类和成员函数的设计、静态数据成员的应用以及程序结构的。在本节中，将在第 5 章示例 5.11 的基础上进一步完善人员管理程序。在前两个章节中，由于还没有学习数组和字符串的概念，我们忽略了姓名的表示。现在我们可以在类类中添加一个新的数据成员来表示姓名，并完善人员管理程序的数据成员。相应地，我们需要添加成员函数来操作这个数据成员。

## 252 — 6 数组、指针与字符串

```cpp
employee {
#name: char [20]
#individualEmpNo: int
#grade: int
#accumPay: float
}
```
```cpp
+ employee();
+ ~employee()
+ setName(char*): void
+ promote(): void
+ SetAccumPay(float pa): void
+ GetIndividualEmpNo(): int;
```

![](img/5618306d085ac1bac8275d6c4c5bbf2a_269_0.png)

```cpp
//employee.h
class employee {
protected:
  char name[20]; // 
  int individualEmpNo; // 工员号
  int grade; // 等级
  float accumPay; // 月薪
  static int employeeNo; // 该公司当前最大的员工编号
public:
  employee(); // 构造函数
  ~employee(); // 析构函数
  void setName(char*); // 设置名字函数
  char * GetName(); // 获取名字函数
  void promote(); // 升职函数
  void SetAccumPay(float pa); // 设置月薪函数
  int GetIndividualEmpNo(); // 获取编号函数
  int GetGrade(); // 获取等级函数
  float GetAccumPay(); // 获取月薪函数
};
```
```cpp
//employee.cpp
#include<iostream>
#include<cstring> // 包含字符串头文件
// 操作
#include "employee.h"
using namespace std;
int employee::employeeNo = 1000; // 员工编号的基础为1000
employee::employee()
{
  individualEmpNo = employeeNo++;
  // 新输入员工的编号是当前最大
  //  own加1
  grade = 1; // 等级的初始值为1
  accumPay = 0.0; // 月薪的初始值为0.0
}
```
```cpp
void employee::promote(int increment)
{ 
  grade += increment; 
}
//  promote, 升职的等级由 increment 决定
```
```cpp
void employee::setName(char* names)
{
  strncpy(name, names); // 设置名字
}
```
```cpp
char* employee::GetName()
{
  return name; // 获取员工名字
}
```
```cpp
void employee::SetAccumPay(float pa)
{ 
  accumPay = pa; // 设置月薪
}
```
```cpp
int employee::GetIndividualEmpNo()
{ 
  return individualEmpNo; // 获取员工编号
}
```
```cpp
int employee::GetGrade()
{ 
  return grade; // 获取等级
}
```
```cpp
float employee::GetAccumPay()
{ 
  return accumPay; // 获取月薪
}
```
```cpp
// 6_25.cpp
#include<iostream>
#include "employee.h"
using namespace std;
int main()
{
    employee emp[4];
    char namestr[20]; // 临时存储输入获取的
    // 名字在 namestr 中
    float pa;
    int grade, i;
    for (i = 0; i < 4; i++)
    {
      cout << "Please input the name of next employee:";
      cin >> namestr;
      emp[i].SetName(namestr); // 设置员工 emp[i] 的名字
      cout << "Please input the monthly pay of the employee:";
      cin >> pa;
      emp[i].SetAccumPay(pa); // 设置员工 emp[i] 的月薪
      cout << "Please input promotion grades of the employee:";
      cin >> grade;
      emp[i].promote(grade); // emp[i] 升职
    }
    // 显示信息
    for (i = 0; i < 4; i++)
    {
      cout << emp[i].GetName() << " number" << emp[i].GetIndividualEmpNo()
        << " grade is " << emp[i].GetGrade() << " grade, current month salary "
        << emp[i].GetAccumPay() << endl;
    }
    return 0;
}
```
