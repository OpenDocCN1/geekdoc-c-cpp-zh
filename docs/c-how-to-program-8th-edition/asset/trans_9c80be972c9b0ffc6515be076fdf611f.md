
```text
After first replacement:
The.values.in.any.left.subtree
are.less.than.the.value.in.the

After second replacement:
The;;alues;;n;;ny;;eft;;ubtree
are;;ess;;han;;he;;alue;;n;;he
```

图 18.7 | 演示函数 erase 和 replace。（第 3 部分，共 3 部分。）

第 26–33 行使用 find 定位空格字符的每次出现。然后通过调用 string 成员函数 replace 将每个空格替换为句点。函数 replace 接受三个参数：字符串中应开始替换的字符下标、要替换的字符数以及替换字符串。当未找到搜索字符时，成员函数 find 返回 `string::npos`。在第 32 行，向 position 加 1，以便在下一个字符的位置继续搜索。

第 37–45 行使用函数 find 查找每个句点，并使用另一个重载函数 replace 将每个句点及其后一个字符替换为两个分号。传递给此版本 replace 的参数包括：替换操作开始处的元素下标、要替换的字符数、一个替换字符串（从中选择子串用作替换字符）、该替换字符串中替换子串开始的元素以及要使用的替换字符串中的字符数。

## 18.9 将字符插入 string

string 类提供用于将字符插入字符串的成员函数。图 18.8 演示了 string 的插入能力。

该程序声明、初始化并输出字符串 string1、string2、string3 和 string4。第 19 行使用 string 成员函数 insert 将 string2 的内容插入到 string1 的元素 10 之前。

第 22 行使用 insert 将 string4 插入到 string3 的元素 3 之前。最后两个参数指定 string4 中应插入的起始元素和最后元素。使用 `string::npos` 会导致插入整个字符串。

```cpp
1  // Fig. 18.8: Fig18_08.cpp
2  // Demonstrating class string insert member functions.
3  #include <iostream>
4  #include <string>
5  using namespace std;

7  int main()
8  {
9      string string1( "beginning end" );
10     string string2( "middle " );
11     string string3( "12345678" );
12     string string4( "xx" );
```

图 18.8 | 演示 string 的 insert 成员函数。（第 1 部分，共 2 部分。）

```cpp
12    char *ptr2 = new char[ length + 1 ]; // including null
14    // copy characters from string1 into allocated memory
15    string1.copy( ptr2, length, 0 ); // copy string1 to ptr2 char*
16    ptr2[ length ] = '\0'; // add null terminator
18    cout << "string string1 is " << string1
19          << "\nstring converted to a C-Style string is "
20          << string1.c_str() << "\nptr1 is";
22    // Assign to pointer ptr1 the const char * returned by
23    // function data(). NOTE: this is potentially dangerous
24    // assignment. If string1 is modified, pointer ptr1 can
25    // become invalid.
26    ptr1 = string1.data();
28    // output each character using pointer
29    for ( int i = 0; i < length; ++i )
30        cout << *( ptr1 + i ); // use pointer arithmetic
32    cout << "\nptr2 is " << ptr2 << endl;
33    delete [] ptr2; // reclaim dynamically allocated memory
34  } // end main
```

```text
string string1 is STRINGS
string converted to a C-Style string is STRINGS
ptr1 is STRINGS
ptr2 is STRINGS
```

**图 18.9** | *将字符串转换为 C 风格字符串和字符数组。（第 2 部分，共 2 部分。）*

该程序声明一个 string、一个 int 和两个 char 指针（第 9–12 行）。string string1 初始化为 "STRINGS"，ptr1 初始化为 0，length 初始化为 string1 的长度。动态分配足够大的内存以容纳与 string string1 等价的基于指针的字符串，并将其附加到 char 指针 ptr2。

第 15 行使用 string 成员函数 copy 将对象 string1 复制到 ptr2 所指向的 char 数组。第 16 行手动在 ptr2 所指向的数组中放置终止空字符。

第 20 行使用函数 c_str 获取一个 `const char *`，它指向一个以空字符终止的 C 风格字符串，其内容与 string1 相同。该指针被传递给流插入运算符进行输出。

第 26 行将类 string 成员函数 data 返回的 `const char *` 赋给指针 ptr1。该成员函数返回一个不以空字符终止的 C 风格字符数组。在示例中我们不修改 string1。如果 string1 被修改（例如，由于诸如 `string1.insert( 0, "abcd" );` 的成员函数调用，字符串的动态内存改变了其地址），ptr1 可能变得无效——这可能导致不可预测的结果。

第 29–30 行使用指针算术输出 ptr1 所指向的字符数组。在第 32–33 行，输出 ptr2 所指向的 C 风格字符串，并删除为 ptr2 分配的内存以避免内存泄漏。

> **常见编程错误 18.2**
> 
> 未用空字符终止由 `data` 返回的字符数组可能导致执行时错误。

![](img/bfd978e7e9b192bab46ec2a89e481263_746_0.png)

> **良好编程实践 18.1**
> 
> 只要有可能，应使用更健壮的 `string` 类对象，而不是基于 C 风格指针的字符串。

![](img/bfd978e7e9b192bab46ec2a89e481263_746_1.png)

## 18.11 迭代器

string 类提供用于向前和向后遍历字符串的迭代器。迭代器以类似于指针操作的语法提供对单个字符的访问。迭代器不进行范围检查。本节提供一些“机械示例”来演示迭代器的使用。我们将在第 22 章《标准模板库（STL）》中讨论迭代器更健壮的用法。图 18.10 演示迭代器。

```cpp
// Fig. 18.10: Fig18_10.cpp
// Using an iterator to output a string.
#include <iostream>
#include <string>
using namespace std;

int main()
{
   string string1( "Testing iterators" );
   string::const_iterator iterator1 = string1.begin();

   cout << "string1 = " << string1
        << "\n(Using iterator iterator1) string1 is: ";

   // iterate through string
   while ( iterator1 != string1.end() )
   {
      cout << *iterator1; // dereference iterator to get char
      ++iterator1; // advance iterator to next char
   } // end while

   cout << endl;
} // end main
```

```text
string1 = Testing iterators
(Using iterator iterator1) string1 is: Testing iterators
```

**图 18.10** | 使用迭代器输出字符串。

第 9–10 行声明 string string1 和 `string::const_iterator` iterator1。const_iterator 是一种不能修改字符串的迭代器——在这里是它所遍历的字符串。迭代器 iterator1 通过 string 类成员函数 `begin` 初始化为 string1 的开头。begin 有两个版本——一个返回用于遍历非 const 字符串的迭代器，另一个 const 版本返回用于遍历 const 字符串的 `const_iterator`。第 12 行输出 `string1`。

第 16–20 行使用迭代器 `iterator1`“遍历”`string1`。类 `string` 的成员函数 `end` 返回一个迭代器（或 `const_iterator`），指向 `string1` 最后一个元素之后的位置。每个元素通过解引用迭代器来打印，就像解引用指针一样，并使用运算符 `++` 将迭代器前进一个位置。

类 `string` 提供成员函数 `rend` 和 `rbegin`，用于从字符串末尾向开头反向访问单个字符串字符。成员函数 `rend` 和 `rbegin` 返回 `reverse_iterators` 或 `const_reverse_iterators`（取决于字符串是非 const 还是 const）。练习 18.8 要求你编写一个程序来演示这些能力。

![](img/bfd978e7e9b192bab46ec2a89e481263_747_0.png)

> **良好编程实践 18.2**
> 
> *当涉及迭代器的操作不应修改所处理的数据时，应使用 `const_iterator`。这是应用最小权限原则的另一个示例。*

## 18.12 字符串流处理

除标准流 I/O 和文件流 I/O 之外，C++ 流 I/O 还包括从内存中的字符串输入以及向内存中的字符串输出的能力。这些能力通常称为内存中 I/O 或字符串流处理。

从字符串输入由类 `istringstream` 支持。向字符串输出由类 `ostringstream` 支持。类名 istringstream 和 ostringstream 实际上是由以下 typedef 定义的别名

```cpp
typedef basic_istringstream< char > istringstream;
typedef basic_ostringstream< char > ostringstream;
```

类模板 basic_istringstream 和 basic_ostringstream 提供与类 istringstream 和 ostringstream 相同的功能，以及特定于内存中格式化的其他成员函数。使用内存中格式化的程序必须包含 `<sstream>` 和 `<iostream>` 头文件。

这些技术的一个应用是数据验证。程序可以一次从输入流读取一整行到字符串中。接下来，验证例程可以仔细检查字符串的内容，并在必要时修正（或修复）数据。然后，程序可以继续从字符串输入，因为它知道输入数据格式正确。

向字符串输出是利用 C++ 流强大输出格式化能力的一种好方法。可以在字符串中准备数据，以模拟编辑后的屏幕格式。该字符串可以写入磁盘文件以保留屏幕图像。

ostringstream 对象使用 string 对象存储输出数据。类 ostringstream 的 `str` 成员函数返回该字符串的副本。

图 18.11 演示了一个 ostringstream 对象。该程序创建 ostringstream 对象 outputString（第 10 行），并使用流插入运算符向该对象输出一系列字符串和数值。

第 22–23 行将 string string1、string string2、string string3、double double1、string string4、int integer、string string5 以及 int integer 的地址——全部输出到内存中的 outputString。第 26 行使用流插入运算符和调用 outputString.str() 来显示第 22–23 行所创建字符串的副本。行
