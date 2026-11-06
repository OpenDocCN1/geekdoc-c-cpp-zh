
运算符具有可交换性（与两个基本类型操作数时完全相同）。问题在于，如果要将加法运算符重载为成员函数，类对象必须出现在加法运算符的左侧。因此，我们将该运算符重载为全局函数，以允许 HugeInteger 出现在加法的右侧。处理左侧 HugeInteger 的 operator+ 函数仍然可以是成员函数。全局函数只是交换其参数并调用该成员函数。

## 11.5 重载流插入运算符和流提取运算符

你可以使用流提取运算符 >> 和流插入运算符 << 输入和输出基本类型数据。C++ 类库重载了这些运算符，以处理每种基本类型，包括指针和 C 风格 char * 字符串。你也可以重载这些运算符，为自己的类型执行输入和输出。图 11.3–11.5 中的程序重载了这些运算符，以按 "(000) 000-0000" 的格式输入和输出 PhoneNumber 对象。该程序假定电话号码输入正确。

```cpp
1   // Fig. 11.3: PhoneNumber.h
2   // PhoneNumber class definition
3   #ifndef PHONENUMBER_H
4   #define PHONENUMBER_H
5
6   #include <iostream>
7   #include <string>
8   using namespace std;
9
10  class PhoneNumber
11  {
12     friend ostream &operator<<( ostream &, const PhoneNumber & );
13     friend istream &operator>>( istream &, PhoneNumber & );
14  private:
15     string areaCode; // 3-digit area code
16     string exchange; // 3-digit exchange
17     string line; // 4-digit line
18  }; // end class PhoneNumber
19
20  #endif
```

图 11.3 | 将重载的流插入运算符和流提取运算符声明为友元函数的 PhoneNumber 类。

```cpp
1   // Fig. 11.4: PhoneNumber.cpp
2   // Overloaded stream insertion and stream extraction operators
3   // for class PhoneNumber.
4   #include <iomanip>
5   #include "PhoneNumber.h"
6   using namespace std;
```

图 11.4 | 类 PhoneNumber 的重载流插入运算符和流提取运算符。（第 1 部分，共 2 部分）

```cpp
// overloaded stream insertion operator; cannot be
// a member function if we would like to invoke it with
// cout << somePhoneNumber;
ostream& operator<<( ostream &output, const PhoneNumber &number )
{
    output << "(" << number.areaCode << ") "
        << number.exchange << "-" << number.line;
    return output; // enables cout << a << b << c;
} // end function operator<<

// overloaded stream extraction operator; cannot be
// a member function if we would like to invoke it with
// cin >> somePhoneNumber;
istream& operator>>( istream &input, PhoneNumber &number )
{
    input.ignore(); // skip (
    input >> setw( 3 ) >> number.areaCode; // input area code
    input.ignore( 2 ); // skip ) and space
    input >> setw( 3 ) >> number.exchange; // input exchange
    input.ignore(); // skip dash (-)
    input >> setw( 4 ) >> number.line; // input line
    return input; // enables cin >> a >> b >> c;
} // end function operator>>
```

图 11.4 | 类 PhoneNumber 的重载流插入运算符和流提取运算符。（第 2 部分，共 2 部分）

```cpp
// Fig. 11.5: fig11_05.cpp
// Demonstrating class PhoneNumber's overloaded stream insertion
// and stream extraction operators.
#include <iostream>
#include "PhoneNumber.h"
using namespace std;

int main()
{
    PhoneNumber phone; // create object phone

    cout << "Enter phone number in the form (123) 456-7890:" << endl;

    // cin >> phone invokes operator>> by implicitly issuing
    // the global function call operator>>( cin, phone )
    cin >> phone;

    cout << "The phone number entered was: ";

    // cout << phone invokes operator<< by implicitly issuing
    // the global function call operator<<( cout, phone )
    cout << phone << endl;
} // end main
```

图 11.5 | 重载的流插入运算符和流提取运算符。（第 1 部分，共 2 部分）

```text
    Enter phone number in the form (123) 456-7890:
    (800) 555-1212
    The phone number entered was: (800) 555-1212
```

图 11.5 | 重载的流插入运算符和流提取运算符。（第 2 部分，共 2 部分）

流提取运算符函数 operator>>（图 11.4，第 21–30 行）接受 istream 引用 input 和 PhoneNumber 引用 number 作为参数，并返回一个 istream 引用。函数 operator>> 将以下形式的电话号码输入

```text
    (800) 555-1212
```

到 PhoneNumber 类的对象中。当编译器看到表达式

```cpp
    cin >> phone
```

在图 11.5 第 16 行中，编译器会生成全局函数调用

```cpp
    operator>>( cin, phone );
```

当此调用执行时，引用参数 input（图 11.4，第 21 行）成为 cin 的别名，引用参数 number 成为 phone 的别名。该运算符函数将电话号码的三个部分作为字符串读入由参数 number 引用的 PhoneNumber 对象的 areaCode（第 24 行）、exchange（第 26 行）和 line（第 28 行）成员中。流操纵符 setw 限制读入每个字符串的字符数。当与 cin 和字符串一起使用时，setw 将读取的字符数限制为其参数指定的字符数（即 setw( 3 ) 允许读取三个字符）。通过调用 istream 成员函数 ignore（图 11.4，第 23、25 和 27 行）跳过括号、空格和短横线字符，该函数丢弃输入流中指定数量的字符（默认一个字符）。函数 operator>> 返回 istream 引用 input（即 cin）。这使得对 PhoneNumber 对象的输入操作可以与对其他 PhoneNumber 对象或其他数据类型对象的输入操作级联。例如，程序可以在一条语句中输入两个 PhoneNumber 对象，如下所示：

```cpp
    cin >> phone1 >> phone2;
```

首先，表达式 cin >> phone1 通过生成全局函数调用来执行

```cpp
    operator>>( cin, phone1 );
```

此调用随后返回 cin 的引用作为 cin >> phone1 的值，因此表达式的剩余部分被简单地解释为 cin >> phone2。它通过生成全局函数调用来执行

```cpp
    operator>>( cin, phone2 );
```

流插入运算符函数（图 11.4，第 11–16 行）接受一个 ostream 引用（output）和一个 const PhoneNumber 引用（number）作为参数，并返回一个 ostream 引用。函数 operator<< 显示 PhoneNumber 类型的对象。当编译器看到表达式

```cpp
    cout << phone
```

在图 11.5 第 22 行中，编译器会生成全局函数调用

```cpp
operator<<( cout, phone );
```

函数 operator<< 将电话号码的各个部分作为字符串显示，因为它们存储为 string 对象。

![](img/023f159fdd47d944d48e08843cea732d_511_0.png)

> **错误预防提示 11.1**
> 
> 从重载的 << 或 >> 运算符函数返回引用通常是成功的，因为 cout、cin 和大多数流对象是全局的，或者至少具有较长的生命周期。返回对自动变量或其他临时对象的引用是危险的——这可能创建指向不存在对象的“悬空引用”。

函数 operator>> 和 operator<< 在 PhoneNumber 中声明为全局友元函数（图 11.3，第 12–13 行）。它们是全局函数，因为 PhoneNumber 类的对象是该运算符的右操作数。请记住，二元运算符的重载运算符函数只有在左操作数是该函数所属类的对象时，才能作为成员函数。如果重载的输入和输出运算符出于性能原因需要直接访问非公有类成员，或者因为类可能不提供合适的 get 函数，则将它们声明为友元。此外，函数 operator<< 参数列表中的 PhoneNumber 引用（图 11.4，第 11 行）是 const，因为 PhoneNumber 将只是被输出；而函数 operator>> 参数列表中的 PhoneNumber 引用（第 21 行）是非 const，因为必须修改 PhoneNumber 对象，以将输入的电话号码存储到该对象中。

![](img/023f159fdd47d944d48e08843cea732d_511_1.png)

> **软件工程观察 11.3**
> 
> 为用户定义类型新增的输入/输出能力被添加到 C++ 中，而无需修改标准输入/输出库类。这是 C++ 可扩展性的另一个例子。

## 11.6 重载一元运算符

类的一元运算符可以重载为不带参数的非静态成员函数，或重载为带一个参数的全局函数，该参数必须是该类的一个对象（或对象的引用）。实现重载运算符的成员函数必须是非静态的，以便它们可以访问该类每个对象中的非静态数据。请记住，静态成员函数只能访问类的静态成员。

在本章后面，我们将重载一元运算符 !，以测试我们创建的 String 类（第 11.11 节）的对象是否为空，并返回一个 bool 结果。考虑表达式 !s，其中 s 是 String 类的对象。当像 ! 这样的一元运算符被重载为不带参数的成员函数，并且编译器看到表达式 !s 时，编译器会生成函数调用 s.operator!()。操作数 s 是正在对其调用 String 类成员函数 operator! 的类对象。该函数在类定义中声明如下：

```cpp
class String
{
public:
    bool operator!() const;
    ...
}; // end class String
```
