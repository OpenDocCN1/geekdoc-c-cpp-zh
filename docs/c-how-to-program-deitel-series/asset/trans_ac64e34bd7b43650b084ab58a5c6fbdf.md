
### 不能重载的运算符

C++的大多数运算符都可以重载。图10.2列出了不能重载的运算符。

| 不能重载的运算符 |
|---|
| `.` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `.*` (指向成员的指针) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `::` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `?:` |

**图10.2** &nbsp; 不能重载的运算符。

### 运算符重载的规则与限制

在为自己的类准备重载运算符时，有几条规则和限制需要牢记：

- *运算符的优先级不能通过重载改变。* 不过，可以使用圆括号来强制表达式中重载运算符的求值顺序。
- *运算符的结合性不能通过重载改变*——如果某个运算符通常从左向右结合，那么其所有重载版本也是如此。
- *不能改变运算符的“元数”*（即运算符操作数的个数）——重载的一元运算符仍然是一元运算符；重载的二元运算符仍然是二元运算符。运算符`&`、`,`、`+`和`−`都同时具有一元和二元版本；这些一元和二元版本可以分别重载。
- *不能创建新运算符；只能重载现有运算符。*
- 运算符作用于基本类型值时的含义不能通过运算符重载改变。例如，不能使`+`运算符对两个int执行减法。运算符重载只适用于用户定义类型的对象，*或者用户定义类型的对象与基本类型对象的混合。*
- 相关的运算符，如`+`和`+=`，必须分别重载。
- 重载`()`、`[]`、`->`或任何赋值运算符时，运算符重载函数*必须*声明为类成员。对于所有其他可重载运算符，重载函数可以是成员函数或非成员函数。

> **软件工程观察 10.1**
> 
> *为类类型重载运算符，使它们尽可能接近内置运算符作用于基本类型的方式。*

## 10.4 重载二元运算符

二元运算符可以重载为带一个参数的非静态成员函数，或带两个参数的非成员函数（其中一个参数必须是类对象或类对象的引用）。出于性能原因，非成员运算符函数通常声明为类的友元。

### 作为成员函数的二元重载运算符

考虑使用<比较你定义的String类的两个对象。当将二元运算符<重载为String类的非静态成员函数时，如果y和z是String类对象，则y < z被视作已编写y.operator<(z)，调用带一个参数的operator<成员函数，其声明如下：

```cpp
class String
{
public:
   bool operator< ( const String & ) const;
   ...
}; // end class String
```

只有当左操作数是该函数作为成员的类的对象时，二元运算符的重载函数才能作为成员函数。

### 作为非成员函数的二元重载运算符

作为非成员函数，二元运算符<必须接受两个参数——其中之一必须是重载运算符所关联类的对象（或对象的引用）。如果y和z是String类对象或String类对象的引用，则y < z被视作程序中已编写调用operator<(y, z)，调用如下声明的函数operator<：

```cpp
bool operator< ( const String &, const String & );
```

## 10.5 重载二元流插入与流提取运算符

可以使用流提取运算符>>和流插入运算符<<输入和输出基本类型数据。C++类库为每种基本类型（包括指针和char *字符串）重载了这些二元运算符。你也可以重载这些运算符，以便对自己的类型执行输入和输出操作。图10.3–10.5中的程序重载了这些运算符，用于按“(000) 000–0000”格式输入和输出PhoneNumber对象。该程序假定电话号码输入正确。

```cpp
// Fig. 10.3: PhoneNumber.h
// PhoneNumber class definition
#ifndef PHONENUMBER_H
#define PHONENUMBER_H

#include <iostream>
#include <string>

class PhoneNumber
{
```

图10.3 | 带有重载流插入和流提取运算符作为友元函数的PhoneNumber类。（第1部分，共2部分。）

```cpp
#include "PhoneNumber.h"
using namespace std;

int main()
{
    PhoneNumber phone; // create object phone

    cout << "Enter phone number in the form (123) 456-7890:" << endl;

    // cin >> phone invokes operator>> by implicitly issuing
    // the non-member function call operator>>(cin, phone);
    cin >> phone;

    cout << "The phone number entered was: ";

    // cout << phone invokes operator<< by implicitly issuing
    // the non-member function call operator<<(cout, phone)
    cout << phone << endl;
} // end main
```

```
Enter phone number in the form (123) 456-7890:
(800) 555-1212
The phone number entered was: (800) 555-1212
```

图10.5 | 重载的流插入和流提取运算符。（第2部分，共2部分。）

### 重载流提取（>>）运算符

流提取运算符函数operator>>（图10.4，第21–30行）接受istream引用input和PhoneNumber引用number作为参数，并返回istream引用。运算符函数operator>>输入如下形式的电话号码：

(800) 555-1212

到PhoneNumber类的对象中。当编译器看到表达式

```
cin >> phone
```

在图10.5的第16行，编译器生成非成员函数调用

```
operator>>( cin, phone );
```

当此调用执行时，引用参数input（图10.4，第21行）成为cin的别名，引用参数number成为phone的别名。该运算符函数将电话号码的三个部分作为字符串读入由参数number引用的PhoneNumber对象的areaCode（第24行）、exchange（第26行）和line（第28行）成员中。流操纵符setw限制读入每个字符串的字符数。当与cin和字符串一起使用时，setw将读取的字符数限制为其参数指定的字符数（即setw(3)允许读取三个字符）。通过调用istream成员函数ignore（图10.4，第23、25和27行）跳过圆括号、空格和破折号字符，该函数丢弃输入流中指定数量的字符（默认一个字符）。函数operator>>返回istream引用input（即cin）。这使得PhoneNumber对象的输入操作可以与另一个PhoneNumber对象或其他数据类型的输入操作级联。例如，程序可以在一条语句中输入两个PhoneNumber对象，如下所示：

```
cin >> phone1 >> phone2;
```

首先，表达式`cin >> phone1`通过非成员函数调用执行

```
operator>>( cin, phone1 );
```

该调用随后返回对`cin`的引用作为`cin >> phone1`的值，因此表达式的其余部分被简单地解释为`cin >> phone2`。这通过以下*非成员函数调用*执行：

```
operator>>( cin, phone2 );
```

![](img/b42ba5cd262b1358d16610173f975e4d_478_0.png)

> **良好编程实践 10.1**
>
> 重载运算符应模仿其内置对应物的功能——例如，+运算符应执行加法，而不是减法。避免过度或不一致地使用运算符重载，因为这会使程序难以理解和阅读。

### 重载流插入（<<）运算符

流插入运算符函数（图10.4，第11–16行）接受一个ostream引用（output）和一个const PhoneNumber引用（number）作为参数，并返回一个ostream引用。函数operator<<显示PhoneNumber类型的对象。当编译器看到表达式

```
cout << phone
```

在图10.5的第22行，编译器生成*非成员函数调用*

```
operator<<( cout, phone );
```

函数operator<<将电话号码的各部分显示为字符串，因为它们存储为string对象。

### 作为非成员友元函数的重载运算符

函数operator>>和operator<<在PhoneNumber中被声明为*非成员友元函数*（图10.3，第11–12行）。它们是*非成员函数*，因为PhoneNumber类的对象必须是运算符的*右*操作数。如果这些是PhoneNumber成员函数，则必须使用以下别扭的语句来输出和输入PhoneNumber：

```
phone << cout;
phone >> cin;
```

这样的语句会让大多数C++程序员感到困惑，他们熟悉的是`cout`和`cin`分别作为`<<`和`>>`的*左*操作数。

只有当*左*操作数是该函数作为成员的类的对象时，二元运算符的重载函数才能作为成员函数。*如果重载的输入和输出运算符需要直接访问非公有类成员，或者类可能没有提供适当的get函数，则它们被声明为友元。* 另外，函数operator<<的参数列表（图10.4，第11行）中的PhoneNumber引用是const，因为PhoneNumber将仅被输出，而PhoneNumber引用在

