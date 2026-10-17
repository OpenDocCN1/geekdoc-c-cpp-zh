
运行结果：
Enter line of text:
This is a line of text.
Words in the text:
This
is
a
line
of
text.

在程序 10.19 的循环之后，我们将 `wStart` 指向当前单词的开头，即文本中的第一个单词（第 21 行）。在循环的每次迭代中：

- a. 我们将 `wEnd` 设置为当前单词的结尾（第 24 行）。
- b. 我们提取 `wStart` 和 `wEnd` 之间的字符串（第 25 行）。
- c. 我们更新 `wStart` 的值，使其指向下一个单词的开头以供下次迭代（第 26 行）。

当我们退出循环时，所有的单词都被提取并打印了。分析该循环，确定如果在之间发现两个或三个空格会发生什么。

# 比较字符串

C++ 字符串提供了两种比较字符串的方法：整数比较和布尔比较。

## 第 10 章 字符串

| pos1 | n1 | | pos2 | n2 |
|---|---|---|---|---|
| 主宿字符串 | | 参数字符串 | | |

比较两个 C++ 字符串

| pos1 | n1 | | pos2 | n2 |
|---|---|---|---|---|
| 主宿字符串 | | 参数字符串 | | |

比较 C++ 字符串和 C 字符串

注意：
如果 `pos1` 或 `pos2` 缺失，意味着字符串的开头。
如果 `n1` 或 `n2` 缺失，意味着字符串的结尾。

- 图例：
- C++ 字符串
- C 字符串

图 10.11 比较两个字符串

**整数比较** 整数比较比较两个字符串并返回三个值之一：当两个字符串相等时返回0，第一个大于第二个时返回正数，当第一个小于第二个时返回负数。其语法规则较少。第一个字符串为主宿字符串。字符串参数可以是 C++ 字符串或 C 字符串。每个都可以是字符串或子字符串。C++ 字符串的子字符串可以通过给出起始索引和长度来定义；C 字符串的子字符串必须从第一个字符开始。图 10.11 显示了这一思路。

```cpp
int result = str.compare(pos1, n1, str2, pos2, n2); // 两个 C++ 字符串
int result = str.compare(pos1, n1, str2); // C++ 字符串和 C 字符串
```

表 10.2 显示了比较两个字符串的成员函数。第一个比较主宿字符串与另一个 C++ 字符串；第二个比较主宿字符串与 C 字符串，它不使用 `pos` 参数，因为它必须从开头开始。按照惯例，*pos1* 和 *n1* 定义第一个字符串的起始索引和长度；*pos2* 和 *n2* 定义第二个字符串的起始索引和 长度。图 10.11 显示了我们如何使用这些成员函数。

### 示例 10.20
程序 10.20 比较字符串。

#### 程序 10.20 字符串的整数比较

```cpp
********************************************************************
* 测试整数比较的程序。                               *
********************************************************************
#include <string>
#include <iostream>
using namespace std;
```

### 程序 10.20 字符串的整数比较（续）

```cpp
int main () {
    // 声明两个 C++ 字符串
    string str1("Hello friends");
    string str2("Hello friends");
    // 比较两个 C++ 字符串
    cout << str1 << " compared with " << str2 << ":";
    cout << str1.compare(str2) << endl;
    // 比较两个 C++ 字符串的部
    cout << "Hello compared with Hello: ";
    cout << str1.compare(0, 5, str2, 0, 5) << endl;
    // 比较第一个 C++ 字符串的部分和 C 字符串
    cout << "Hello compared with Hello: ";
    cout << str1.compare(0, 5, str2) << endl;
    // 比较 C++ 字符串的部分和 C 字符串的部分
    cout << "Hel compared with Hell: ";
    cout << str2.compare(0, 3, "Hello", 4);
    return 0;
}
```

Hello friends compared with Hello: 1
Hello compared with Hello: 0
Hello compared with Hello: -8
Hel compared with Hell: -1

我们检查结果：

1. 在第一次比较（第 15 行）中，我们正在比较 "Hello friends" 和 "Hello friends"。比较逐个字符进行，直到比较 'm' 字符和 'f' 字符。'm' 字符大于 'f' 字符，函数返回 1（一个正数）。
2. 在第二次比较（第 18 行）中，我们正在比较 "Hello" 和 "Hello"。两个字符串相等；结果为 0。
3. 在第三次比较（第 21 行）中，我们正在比较 "Hello" 和 "Hello friends"。空字符与空格进行比较。结果是负的 (-8)。
4. 在第四次比较（第 24 行）中，我们正在比较 "Hel" 和 "Hell"。当我们到达该字符时，我们正在比较一个空字符与 '1'。结果是一个负数 (-1)。

我们必须小心，不要将整数比较的结果直接转换为布尔类型，因为 `i` 和 `l` 都会被转换为 true，这是不正确的。

**逻辑比较** 逻辑比较比较两个字符串并返回一个布尔值（true 或 false）。与整数比较一样，比较的是两个字符串。第一个始终为主宿字符串，第二个是 C 字符串。与整数比较不同，我们无法比较子字符串。如果我们想这样做，必须为它们创建临时字符串。

以下显示了我们如何使用这些成员函数。

```cpp
bool result = str.compare(pos1, n1, str2, pos2, n2); // 两个 C++ 字符串
bool result = str.compare(pos1, n1, str2); // C++ 字符串和 C 字符串
```

### 示例 10.21

程序 10.20 比较字符串。

#### 程序 10.21 使用运算符比较字符串

```cpp
********************************************************************
* 测试整数比较的程序。                               *
********************************************************************
#include <string>
#include <iostream>
using namespace std;
// 声明两个函数
void reverse(string& str);
bool isPalindrome(string& str);
int main ()
{
    // 构建一个默认字符串对象
    string str;
    // 输入
    cout << "Enter string:";
    getline(cin, str);
    // 检查是否为回文
{
    if (isPalindrome(str))
    {
        cout << str << " is a palindrome.";
    }
    else
    {
        cout << str << " is not a palindrome.";
    }
    return 0;
}
********************************************************************
* isPalindrome 函数调用 reverse 函数
* 比较其参数与其反转参数
********************************************************************
bool isPalindrome(string& str)
{
    string temp (str);
    reverse(temp);
    return str == temp;
}
void reverse(string& str)
{
    for (int i = 0, j = str.length() - 1; i < j; ++i, --j)
    {
        char temp = str[i];
        str[i] = str[j];
        str[j] = temp;
    }
}
```

### 示例 10.22

10.2 C++ 字符串类 479

如果一个字符串正读反读都相同，它就是回文。"rotor'、dad' 和 'noon' 是回文。更复杂的回文例子有 'Madam, I am Adam' 和 'Able was ere I saw Elba.'我们可以通过将其与其反转比较来轻松检查字符串是否为回文。在某些情况下，我们需要在反转字符串之前移除标点并转换字符大小。程序 10.22 显示了如何检查回文。

```cpp
********************************************************************
* 检查输入字符串是否为回文的程序.*
********************************************************************
#include <string>
#include <iostream>
#include <cctype>
using namespace std;
// 声明两个函数
void reverse(string& str);
bool isPalindrome(string& str);
int main ()
{
    // 构建一个默认字符串对象
    string str;
    // 输入
    cout << "Enter string:";
    getline(cin, str);
    // 预处理字符串
    string processed = "";
    for (char c : str) {
        if (isalnum(c))
            processed += tolower(c);
    }
    // 检查回文
    if (isPalindrome(processed))
    {
        cout << str << " is a palindrome.";
    }
    else
    {
        cout << str << " is not a palindrome.";
    }
    return 0;
}
********************************************************************
* isPalindrome 函数调用 reverse 函数
* 比较其参数与其反转参数
********************************************************************
bool isPalindrome(string& str)
{
    string temp (str);
    reverse(temp);
    return str == temp;
}
void reverse(string& str)
{
    for (int i = 0, j = str.length() - 1; i < j; ++i, --j)
    {
        char temp = str[i];
        str[i] = str[j];
        str[j] = temp;
    }
}
```

#### 程序 10.22 测试回文（继续）

```cpp
38 return (temp == strg);
39 }
40 /* reverse 函数反转字符串参数。 *
41 ******************************************************************/
42 void reverse(string &strg)
43 {
44 string temp (strg);
45 int size = strg.size();
46 for (int i = 0; i < size; i++)
47 {
48 strg[i] = temp[size - 1 - i];
49 }
50 }
```

运行：
输入字符串：rotor
rotor 是回文。

运行：
输入字符串：mom
mom 是回文。

运行：
输入字符串：son
son 不是回文。

# Push_Back

我们需要向字符串中添加一个字符。string 库定义了 `push_back` 函数，它可以在字符串末尾添加一个字符。该库成员函数的使用方法所示：

| `strg.push_back(c);` | // 在末尾附加 c |

在我们的程序设计部分，我们展示了如何向字符串前面插入一个字符。我们还展示了如何从前面或末尾弹出一个字符。

# 修改操作

C++ string 库提供了一系列用于修改操作的不同函数。然而，如果我们构造一个临时字符串作为参数，成员函数的数量可以减少到四个。`temp` 字符串是我们在正在查找的字符集：

| `temp(strg);` | // 一个完整的 C++ 字符串 |
| `temp(strg, pos2);` | // C++ 字符串的一部分 |
| `temp(1, c);` | // 由一个字符组成的字符串 |
| `temp(cstr);` | // 一个完整的 C 字符串 |
| `temp(cstr, n);` | // C 字符串的前 n 个字符 |

## 10.2 C++ 字符串类

![](img/ce9c99d45f71111839bc062830bd19fd_499_0.png)

**图 10.12** append、insert、replace 和 assign 背后的通用思路

图 10.12 展示了这些函数组如何使用临时字符串来修改主字符串。

以下展示了我们如何使用这四类函数：

```cpp
strg.append(temp);          // 附加
strg.insert(pos1, temp);   // 插入
strg.replace(pos1, n1, temp); // 替换
strg.assign(temp);         // 赋值
```

# 部分或全部删除

有两个函数可以完全或部分删除字符串中的字符，而不破坏它。该对象仍然存在，但其字符已部分或全部被移除。

```cpp
strg.clear();                // 删除字符串中的所有字符
strg.erase(pos, n);        // 删除字符串的一部分
```

# 重载运算符

一些修改操作是通过重载运算符实现的。C++ 重载了赋值运算符 (`=`)、复合赋值运算符 (`+=`) 和加法运算符 (`+`)，如下所示。`temp`、`temp1` 和 `temp2` 是字符串类的实例。

```cpp
strg string = temp;        // 赋值
strg string += temp;      // 复合赋值
strg string = temp1+temp2; // 加法
```

# 程序 10.23 打印人的全名

```cpp
1 * 一个显示字符串和字符拼接的程序。 *
2 *****************************************************************/
3 #include <string>
4 #include <iostream>
5 using namespace std;
6 
7 int main ()
8 {
9 // 声明
10 string first, last;
11 char init;
12 // 输入名、姓和首字母
13 cout << "Enter first name: ";
14 cin >> first;
15 cout << "Enter last name: ";
16 cin >> last;
17 cout << "Enter initial: ";
18 cin >> init;
19 // 以种格式打印全名
20 cout << "Full name in first format: " << endl;
21 cout << first << " " + last << " " << init << endl;
22 // 以另一种格式打印全名
23 cout << "Full name in second format: " << endl;
24 cout << last << " " + first << " " << init << endl;
25 return 0;
26 }
```
