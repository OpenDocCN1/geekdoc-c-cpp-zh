
其中 `sourceString` 是要拷贝的字符串，`start` 是起始下标，`numberOfCharacters` 是要拷贝的字符数。

# 912 第 21 章 string 类与字符串处理：深度解析

// 图 21.1: Fig21_01.cpp
展示字符串赋值与拼接
```cpp
#include <iostream>
#include <string>
using namespace std;
```

```cpp
int main() {
    string string1="cat";
    string string2=""; // 初始化为空字符串
    string string3=""; // 初始化为空字符串
    string string2= string1; // 将 string1 赋值给 string2
    string3.assign(string1); // 将 string1 赋值给 string3
    cout << "string1: " << string1 << "\n"
         << "string2: " << string2 << "\nstring3: " << string3 << "\n\n";
    // 修改 string2 和 string3
    string2[0] = 'r';
    cout << "After modification of string2 and string3:\n"
         << string1 << "\nstring2: " << string2 << "\nstring3: " << string3;
    // 成员函数 at
    for (size_t i=0; i< string3.size(); ++i) {
        cout << string3.at(i); // 可能抛出 out_of_range 异常
    }
    // 定义 string4 和 string5
    string string4+="apult"; // 拼接
    string string5=""; // 初始化为空字符串
    // 重载 +=
    string3+="pet"; // 创建 carpet
    string1.append("accomb"); // 创建 catcomb
    // 将 string1 从下标 4 到末尾的内容追加到
    string5.append(string1, 4, string1.size() - 4);
    cout << "\nAfter concatenation:\string1: " << string1
         << "\nstring2: " << string2 << "\nstring3: " << string3
         << "\nstring4: " << string4 << "\nstring5: " << string5 << endl;
}
```

string1: cat
string2: cat
string3: cat

After modification of string2 and string3:
string1: cat
string2: rat
string3: car

图 21.1 | 展示字符串赋值和拼接。（第一部分，共 2 部分。）

## 21.3 比较字符串

拼接后：
string1: catacom
string2: rat
string3: carpet
string4: catapult
string5: comb

**图 21.1** | 展示字符串的赋值与拼接。（2部分中的2部分。）

第 18 行使用下标运算符将 'r' 赋值给 `string3[2]`（形成 "car"），并将 'r' 赋值给 `string2[0]`（形成 "rat"）。这些字符串随后。

第 24-26 行使用成员函数 `at` 逐个字符输出 `string3` 的内容。成员函数提供了受检查的访问（或范围检查）；即：越字符串边界会抛出 `out_of_range` 异常。下标运算符 `[]` 不提供受检查的访问。这与其在数组上的用法一致。注意，你也可以使用 C++11 的范围 `for` 循环来遍历字符串中的字符，如下：

```cpp
for (char c : string3) {
    cout << c;
}
```

这确保了你不会访问字符串范围之外的任何元素。

> **常见编程错误 21.1**
使用下标运算符访问字符串边界之外的元素是一个意外的逻辑错误。

声明了 `string4 "apult"`（第 29 行），并初始化为 `string1` 与使用重载的 `+` 运算符拼接的结果，对于类来说，该运算符表示拼接。第 33 行使用重载赋值运算符 `+=` 将 `string3` 和 "pet" 拼接。第 34 行使用成员函数 `append` 将 `string1` 和 "acomb" 拼接。

第 38 行将字符串 "comb" 追加到空字符串 `string5` 中。该成员函数传递了用于检索字符的字符串（`string1`）、字符串中的起始下标（4）以及要追加的字符数（`string1.size() - 4` 返回的值）。

`string` 类提供了用于比较字符串的成员函数。图 21.2 展示了 `string` 比较能力。

```cpp
// Fig 21.2: Fig21_02.cpp
// 比较字符串。
#include <iostream>
#include <string>
using namespace std;
```

**图 21.2** | 比较字符串。（3部分中的第一部分。）

# 第 21 章  string 类与字符串流处理：深入探讨

```cpp
int main() {
    string string1{"Testing the comparison functions."};
    string string2{"Hello"};
    string string3{"stinger"};
    string string4(string2); // "Hello"
    cout << "\n1: " << string1 << "\n2: " << string2;
    cout << "\n3: " << string3 << "\n4: " << string4 << "\n\n";
    // 比较 string1 和 string4
    if (string1 == string4) {
        cout << "string1 = string4\n";
    } else if (string1 > string4) {
        cout << "string1 > string4\n";
    } else { // string1 < string4
        cout << "string1 < string4\n";
    }
    // 比较 string1 和 string2
    int result = string1.compare(string2);
    if (result == 0) {
        cout << "string1.compare(string2) == 0\n";
    } else if (result > 0) {
        cout << "string1.compare(string2) > 0\n";
    } else { // result < 0
        cout << "string1.compare(string2) < 0\n";
    }
    // 比较 string1 (元素 2-5) 和 string3 (元素 0-5)
    result = string1.compare(2, 5, string3, 0, 5);
    if (result == 0) {
        cout << "string1.compare(2, 5, string3, 0, 5) == 0\n";
    } else if (result > 0) {
        cout << "string1.compare(2, 5, string3, 0, 5) > 0\n";
    } else { // result < 0
        cout << "string1.compare(2, 5, string3, 0, 5) < 0\n";
    }
    // 比较 string2 和 string4
    result = string4.compare(0, string2.size(), string2);
    if (result == 0) {
        cout << "string4.compare(0, string2.size(), string2) == 0\n";
    } else if (result > 0) {
        cout << "string4.compare(0, string2.size(), string2) > 0\n";
    } else { // result < 0
        cout << "string4.compare(0, string2.size(), string2) < 0\n";
    }
    // 比较 string2 和 string4
    result = string2.compare(0, 3, string4);
    if (result == 0) {
        cout << "string2.compare(0, 3, string4) == 0\n";
    } else if (result > 0) {
        cout << "string2.compare(0, 3, string4) > 0\n";
    } else { // result < 0
        cout << "string2.compare(0, 3, string4) < 0\n";
    }
}
```

**图 21.2** | 比较字符串。（3部分中的2部分）。

## 21.4 子字符串

`string` 类提供了成员函数 `substr` 用于从字符串中提取子字符串。结果是一个从源字符串拷贝的新字符串对象。图 21.3 展示了 `substr`。程序在第 8 行声明并初始化了一个子字符串。第 12 行使用成员函数 `substr` 从 `string1` 中提取子字符串。第一个参数指定所需的子字符串；第二个参数指定字符串的长度。

```cpp
// Fig. 21.3: Fig21_03.cpp
// 展示字符串函数 substr。
#include <iostream>
#include <string>
using namespace std;
int main() {
    string string1("The airplane landed on time.");
    // 提取子字符串 "plane"，
    // 它从下标 7 开始，包含 5 个字符
    cout << string1.substr(7, 5) << endl;
}
```

**图 21.3** | 展示字符串函数 `substr`。

## 21.5 交换字符串

`string` 类提供了成员函数 `swap` 用于交换字符串。图 21.4 交换了两个字符串。第 8-9 行声明并初始化字符串 `first` 和 `second`。随后输出每个字符串。第 14 行使用成员函数 `swap` 交换 `first` 和 `second` 的值。打印两个字符串以确认它们确实已经过交换。字符串函数 `swap` 对于实现字符串排序的程序非常有用。

## 21.6 string 特性

```cpp
// Fig. 21.4: Fig21_04.cpp
// Using the swap function to swap two strings.
#include <iostream>
#include <string>
using namespace std;
int main() {
    string first="one";
    string second="two";
    // output strings
    cout << "Before swap:\n first: " << first << "\nsecond: " << second << "\n";
    first.swap(second); // swap strings
    cout << "\nAfter swap:\n first: " << first << "\nsecond: " << second << endl;
}
```

Before swap:
first: one
second: two

After swap:
first: two
second: one

**图 21.4** 使用 swap 函数交换两个字符串。

## 21.6 string 特性

string 类提供了许多成员函数，用于收集有关字符串大小、长度、容量、最大长度以及其他特性的信息。字符串的大小（size）或长度（length）是存储在字符串中的字符数。字符串的容量（capacity）是在不分配更多内存的情况下可以存储的字符数。字符串的容量必须至少等于字符串当前的大小，尽管它可以大于这个值。字符串的精确容量取决于实现。最大大小（max_size）是字符串可以拥有的最大尺寸。如果超过了此值，将抛出 length_error 异常。图 21.5 展示了确定字符串特性的 string 类成员函数。

```cpp
// Fig. 21.5: Fig21_05.cpp
// Printing string characteristics.
#include <iostream>
#include <string>
using namespace std;
void printStatistics(const string&);
```

**图 21.5** | 打印字符串特性。（3 部分中的第一部分）。

## 第 21 章 string 类与字符串流处理：深入探析

```cpp
int main() {
    string string1; // empty string
    cout << "Statistics before input:\n" << boolalpha;
    printStatistics(string1);
    // read in only "tomato" soup
    cout << "\nenter a string:";
    cin >> string1; // delimited by whitespace
    cout << "The string entered was: " << string1;
    cout << "\nstatistics after input:\n";
    printStatistics(string1);
    // read in "soup"
    cin >> string1; // delimited by whitespace
    cout << "\nthe remaining string is: " << string1 << endl;
    printStatistics(string1);
    // append 46 characters to string1
    string1 += "123456789abcdefghijklmnopqrstuvwxyz1234567890";
    cout << "\nstringring1 is now: " << string1 << endl;
    printStatistics(string1);
    // add 10 elements to string1
    string1.resize(string1.size() + 10);
    cout << "\nstats after resizing by (length + 10):\n";
    printStatistics(string1);
    cout << endl;
}
void printStatistics(const string& stringRef) {
    cout << "capacity: " << stringRef.capacity() << "\nsize: "
    cout << stringRef.max_size() << "\nsize: "
    cout << "length: " << stringRef.size() << "\nempty: "
    cout << stringRef.empty() << endl;
}
```

Statistics before input:
capacity: 15
max size: 4294967294
size: 0
length: 0
empty: true

Enter a string: tomato soup
The string entered was: tomato
Statistics after input:
capacity: 15
max size: 4294967294

![](img/09cee61886647f0b1e06dc44c0065a38_918_0.png)

```text
size: 6
length: 6
empty: false
The remaining string is: soup
capacity: 15
max size: 4294967294
size: 4
```
