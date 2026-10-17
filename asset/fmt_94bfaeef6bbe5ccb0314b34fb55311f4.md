
# 使用 string 类的显示 5 程序（部分部分，共 2 部分）

| 31 | `char next_char;` |
| 32 | `do` |
| 33 | `cin.get(next_char);` |
| 35 | `}` while (`next_char != '\n'`); |
| 36 | `|` |

## 示例对话

Enter your first and last name:
B'Elanna Torres
Your name in our records is: Torres, B'Elanna
Our motto is
Your records are our records.
Please suggest a better (one-line) motto:
Our records go where no records dared to go before.
Our new motto will be:
Our records go where no records dared to go before.

# 字符串对象的 I/O 使用 `<<` 和 `>>` 输出字符串

你可以使用插入运算符 `<<` 来输出字符串对象。你可以使用提取运算符 `>>` 和 `cin` 输入字符串。当使用 `>>` 进行输入时，代码会读取以空白符分隔的字符串。你可以使用函数 `getline` 将整行文本输入到字符串对象中。

## 示例

```cpp
string greeting("Hello"), response, next_word;
cout << greeting << endl;
getline(cin, response);
cin >> next_word;
```

![](img/e625ad4e2abbedaa387b8aa67d62ec3a_471_0.png)

## 自测练习题

15. 考虑以下代码（假设它被嵌入在一个完整且正确的程序中并运行）：

```cpp
string s1, s2;
```

# 字符串与向量

```cpp
cout << "Enter a line of input:\n";
cin >> s1 >> s2;
cout << s1 << " *" << s2 << "-END OF OUTPUT";
```

如果对话开始如下，下一行输出将是什么？

Enter a line of input:
A string is a joy forever!

- 16. 考虑以下代码（假设它被嵌入在一个完整且正确的程序中并运行）：

```cpp
string s;
cout << "Enter a line of input:\n";
getline(cin, s);
cout << s << "-END OF OUTPUT";
```

如果对话开始如下，下一行输出将是什么？

Enter a line of input:
A string is a joy forever!

# 编程提示 getline 的更多版本

到目前为止，我们描述了使用 `getline` 的以下方法：

```cpp
string line;
cout << "Enter a line of input:\n";
getline(cin, line);
```

这个版本在遇到行尾标记 `'\n'` 时停止读取。还有一个版本允许你指定不同的字符作为停止信号。例如，以下代码将在遇到第一个问号时停止：

```cpp
string line;
cout << "Enter some input:\n";
getline(cin, line, '?');
```

如果 `getline` 是一个 void 函数，使用它是合理的，但它实际上返回其第一个参数的引用，在上面的代码中是 `cin`。因此，以下代码将一行文本读入 `s1`，并将非空白字符读入 `s2`：

```cpp
string s1, s2;
getline(cin, s1) >> s2;
```

调用 `getline(cin, s1)` 返回 `cin` 的引用，因此在调用 `getline` 后，发生的事情等同于

```cpp
cin >> s2;
```

# 字符串与向量

这种对 `getline` 的用法似乎是为了 C++ 测试而设计的，而不是为了满足任何实际的编程需求，但在某些情况下可能会有用。

# 陷阱混合使用 cin >> variable; 和 getline

在混合使用 `cin >> variable;` 和 `getline` 时要小心。例如，考虑以下情况：

```cpp
int n;
string line;
cin >> n;
getline(cin, line);
```

`cin >> n` 的调用在缓冲区中留下了一个换行符，因此 `getline` 只读取该换行符并返回一个空字符串。为了修复这个问题，可以使用：

```cpp
cin >> n;
cin.ignore();
getline(cin, line);
```

`getline` 有两个版本：

- `getline(cin, string);`
- `getline(cin, string, delimiter);`

第一个版本读取到行尾标记 `'\n'`。第二个版本读取到指定的分隔符。

# 字符串与向量

`string` 类允许你执行我们在第1节中讨论的C字符串的操作。你可以像访问元素一样访问字符串对象中的字符，因此字符串对象具有数组的所有优点加上C字符串没有的优点，例如自动增加容量。如果 `last_name` 是字符串对象的名称，那么 `last_name[0]` 提供访问 `last_name` 所代表字符串的第0个字符的方法。这种方括号的使用在显示6中得到了演示。

显示6还演示了 `length` 成员函数。每个字符串对象都有一个不接受参数的 `length` 成员函数，返回该字符串对象代表的字符串的长度。因此，字符串对象不仅可以像数组一样使用，`length` 函数还使其行为像一个部分填充的数组，自动跟踪已占据了多少位置。

当用于 `string` 类时，数组括号不会检查非法性。如果你使用非法索引（即大于或等于对象中字符串长度的索引），结果将是不可预测的并且注定是糟糕。你可能会遇到奇怪的行为，而没有任何错误消息告诉你问题是非法索引。

有一个 `at` 成员函数，它可以检查非法的索引值。该成员函数的行为与方括号基本相同，但有两个点不同：你使用函数符号配合 `at`，所以而不是

# 字符串与向量

## DISPLAY 6 字符串对象可以像数组一样工作

```cpp
1 //演示如何像使用数组一样使用字符串对象。
2 #include <iostream>
3 #include <string>
4 using namespace std;
5 int main() {
6 {
7 string first_name, last_name;
8 cout << "Enter your first and last name:\n"
9 cin >> first_name>>last_name;
10 cout << "Your last name is spelled:\n"
11 int i;
12 for (i = 0; i<last_name.length(); i++)
13 {
14 cout << last_name[i] << " "
15 last_name[i] = '-';
16 }
17 cout << endl;
18 for (i = 0; i<last_name.length(); i++)
19 cout << last_name[i] << " "; // 在每个字母下方放置一个 "-"
20 cout << endl;
21 cout << "Good day " << first_name << endl;
22 return 0;
23 }
```

## 示例对话

输入你的名字和姓氏：

John Crichton

你的姓拼写为：

Crichton

------------------------------------------------

你好，John

对于 `a[i]`，你使用 `a.at(i)`；该成员函数会检查 `i` 是否评估为非法索引。如果 `a.at(i)` 中的 `i` 值是一个非法索引，那么你将得到一个运行时错误消息，告诉你哪里出了问题。在以下两个示例代码段中，尝试的访问超出了范围，但其中第一个可能不会产生错误消息，尽管它将访问一个不存在的带索引变量：

```cpp
string str("Mary");
cout << str[6] << endl;
```

# 字符串与向量

然而，第二个示例将导致程序异常终止，因此你至少知道出问题了：

```cpp
string str("Mary");
cout << str.at(6) << endl;
```

但请注意，当 `str.at(i)` 具有非法索引 `i` 时，某些系统提供的错误信息非常糟糕。

你可以通过为索引变量（如 `str[i]`）赋值一个字符值来更改字符串中的单个字符。这也可以通过字符串成员函数完成。例如，要将字符串对象 `str` 中的第三个字符改为 'X'，你可以使用以下代码段之一：

```cpp
str.at(2) = 'X';
```

或

```cpp
str[2] = 'X';
```

与普通的字符数组一样，string 类型对象的字符位置从 0 开始索引，因此字符串中的第三个字符的索引位置是 2。

显示 7 给出了 `string` 类成员函数的部分列表。在许多方面，`string` 类对象的行为比我们在第 1 节介绍的 C 字符串更好。特别是，字符串对象上的 `==` 运算符返回的结果符合我们对字符串相等的直观概念——即：如果两个字符串以相同顺序包含相同的字符，则返回 true，否则返回 false。同样，比较运算符 `<`、`>`、`!=`、`>=` 使用字典序比较字符串对象。如果字符串全由字母且全大写或全小写，那么对于这种情况，字典序排序与日常字母排序是相同的。

## 显示 7 标准类 string 的成员函数（部分 1，共 2 部分）

| 示例 | 备注 |
| --- | --- |
| `string str;` | 默认构造函数创建一个空字符串对象 str。 |
| `string str("sample");` | 创建一个带有数据 "sample" 的字符串对象。 |
| `string str (a_string);` | 创建一个字符串对象 str，它是 `a_string` 的拷贝，`a_string` 是 `string` 类的一个对象。 |

## 显示 7 标准类 string 的成员函数（部分 2，共 2 部分）

## 辅助访问器

| 示例 | 备注 |
| --- | --- |
| `str[i]` | 返回索引 i 处字符的读写引用。不检查非法索引。 |
| `str.at(i)` | 返回索引 i 处字符的读写引用。与 `str[i]` 相同，但此版本版本会检查非法索引。 |
| `str.substr(position, length)` | 返回从 `position` 开始且长度为 `length` 的子字符串。 |
| `str.length()` | 返回 str 的长度。 |

## 赋值/修改器

| 示例 | 备注 |
| --- | --- |
| `str1 = str2;` | 初始化 str1 为 str2 的数据。 |
| `str1 += str2;` | 将 str2 的字符追加到 str1 的末尾。 |
| `str.empty()` | 如果 str 是空字符串返回 true；否则返回 false。 |
| `str1 + str2` | 返回一个将 str2 的数据追加到 str1 末尾的字符串。 |
| `str.insert(pos, str2)` | 在位置 pos 处插入 str2。 |
| `str.erase(pos, length)` | 删除从位置 pos 开始的长度为 `length` 的子字符串。 |

## 比较

| 示例 | 备注 |
| --- | --- |
| `str1 == str2, str1 != str2` | 比较相等或不相等；返回布尔值。 |
| `str1 <= str2, str1 >= str2` | 都是字典序比较。 |

## 查找

| 示例 | 备注 |
| --- | --- |
| `str.find(str1)` | str 中 str1 首次出现的索引。如果未找到 str1，返回特殊值 `string::npos`。 |
| `str.find(str1, pos)` | str 中 str1 首次出现的索引；搜索从 pos 开始。 |
| `str.find_first_of(str1, pos)` | str 中任何属于 str1 字符的首次出现索引；搜索从 pos 开始。 |
| `str.find_not_of(str1, pos)` | str 中任何不属于 str1 字符的首次出现索引；搜索从 pos 开始。 |

## 编程示例 回文测试

回文是指正读和反读都相同的字符串。程序测试输入字符串以判断其是否为回文。回文测试将忽略所有空格和标点符号，并在判断时认为字母的大小写相同。一些回文示例有：

- Able was Elba
- Madam, I'm Adam
- A man, a canal, Panama

`remove_punct` 函数使用了成员函数 `substr` 和 `find`。调用对象提取了所需子字符串的位置和长度。

## 显示 8 回文测试（部分 1，共 3 部分）

```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;
void swap(char& v1, char& v2);
// 修改 v1 和 v2 的值。
string reverse(const string& s);
// 返回 s 的反序。
string remove_punct(const string& s, const string& punct);
// 返回去除了字符串中任何指定字符的 s。
string make_lower(const string& s);
// 返回所有大写字母改为小写的 s，其他字符不变。
bool is_pal(const string& s);
// 如果 s 是回文返回 true，否则返回 false。
int main()
{
    string str;
    cout << "Enter a candidate for palindrome test\n"
         << "followed by pressing Return.\n";
    getline(cin, str);
    if (is_pal(str))
        cout << "\"" << str << "\" is a palindrome.";
    else
        cout << "\"" << str << "\" is not a palindrome.";
    cout << endl;
    return 0;
}
void swap(char& v1, char& v2) {
    char temp = v1;
    v1 = v2;
    temp = temp;
}
string reverse(const string& s) {
    int start = 0;
    int end = s.length();
    string temp(s);
    while (start < end) {
        end--;
        swap(temp[start], temp[end]);
        start++;
    }
    return temp;
}
string make_lower(const string& s) {
    string temp(s);
    for (int i = 0; i < s.length(); i++)
        temp[i] = tolower(s[i]);
    return temp;
}
string remove_punct(const string& s, const string& punct) {
    string no_punct; // 初始化为空字符串
    int s_length = s.length();
    int punct_length = punct.length();
    for (int i = 0; i < s_length; i++) {
        string a_char = s.substr(i, 1); // 单字符字符串
        int location = punct.find(a_char, 0); // 查找 s 中连续字符在 punct 中的位置。
        if (location < 0 || location >= punct_length) {
            no_punct = no_punct + a_char; // a_char 不在 punct 中，所以保留
        }
    }
    return no_punct;
}
bool is_pal(const string& s) {
    string punct(",\.:?!'\""); // 包含空格
    string str(s);
    str = make_lower(str);
    string lower_str = remove_punct(str, punct);
    return (lower_str == reverse(lower_str));
}
```
