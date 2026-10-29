

# 自测练习（续）

如果对话以如下内容开始，下一行输出是什么？

```
输入一行内容：
A string is a joy forever!
```

## 提示：getline 的更多用法

到目前为止，我们介绍了使用 getline 的以下方式：

```
string line;
cout << "Enter a line of input:\n";
getline(cin, line);
```

这个版本在遇到行尾标记 `'\n'` 时停止读取。还有一种版本允许你指定其他字符作为停止信号。例如，下面的代码会在遇到第一个问号时停止：

```
string line;
cout << "Enter some input:\n";
getline(cin, line, '?');
```

将 getline 当作一个 void 函数来使用是合理的，但实际上它会返回其第一个参数的引用，在前面的代码中就是 cin。因此，下面的代码会将一行文本读入 s1，并将一串非空白字符读入 s2：

```
string s1, s2;
getline(cin, s1) >> s2;
```

调用 getline(cin, s1) 会返回 cin 的引用，因此在调用 getline 之后，接下来执行的操作等价于：

cin >> s2;

## 陷阱：混用 cin >> variable; 和 getline

混合使用 cin >> variable; 和 getline 进行输入时要特别小心。例如，考虑以下代码：

```
int n;
string line;
cin >> n;
getline(cin, line);
```

## 陷阱：（续）

当这段代码读取以下输入时，你可能会认为 n 的值会被设为 42，而 line 的值会被设为表示 `"Hello hitchhiker."` 的字符串：

```text
42
Hello hitchhiker.
```

然而，虽然 n 确实被设为了 42，line 却被设成了空字符串。发生了什么？

使用 `cin >> n` 会跳过输入中的前导空白，但会将该行剩余的内容（在本例中只有 `\n`）留给下一次输入。像下面这样的语句：

```cpp
cin >> n;
```

总会在该行中留下一些内容供后续的 `getline` 读取（即使只剩下 `\n`）。在本例中，`getline` 看到 `\n` 后就停止读取，因此 `getline` 读入了一个空字符串。

如果你发现程序似乎莫名其妙地忽略了输入数据，请检查是否混用了这两种输入方式。你可能需要使用第 9.5 节中的 `newline` 函数，或者使用库 `iostream` 中的 `ignore` 函数。例如：

```cpp
cin.ignore(1000, '\n');
```

使用这些参数时，对 ignore 成员函数的调用会读取并丢弃该行剩余的全部内容，直到并包括 `\n`（或者在找不到行尾的情况下，丢弃 1000 个字符后停止）。

使用 cin 同时配合 `>>` 和 `getline` 的程序还可能出现其他令人困惑的问题。此外，当你从一个 C++ 编译器换到另一个编译器时，这些问题可能会时隐时现。遇到所有其他方法都无效的情况，或者如果你希望确保程序具有可移植性，可以改用 cin.get 进行逐字符输入。

我们在本章讨论的 getline 的所有版本都可能出现这些问题。

## 用于 string 类对象的 getline

用于字符串对象的 getline 函数有两个版本：

```cpp
istream& getline(istream& ins, string& strVar, char delimiter);
```

以及

```cpp
istream& getline(istream& ins, string& strVar);
```

该函数的第一个版本从作为第一个参数给出的 istream 对象中读取字符（在本章中始终是 cin），并将字符插入字符串变量 strVar，直到遇到分隔字符。

该字符会从输入中移除并丢弃。第二个版本使用 `'\n'` 作为 delimiter 的默认值；除此之外，它的工作方式相同。

这些 getline 函数会返回它们的第一个参数（在本章中始终是 cin），但通常会将它们当作 void 函数来使用。

## 使用 string 类进行字符串处理

string 类允许你执行与第 9.1 节中讨论的 C 字符串相同的操作，并且还提供更多操作。（多得多！标准 string 类拥有超过 100 个成员函数和其他相关函数。）

你可以用访问数组元素的相同方式访问字符串对象中的字符，因此字符串对象不仅具有字符数组的优点，还具有数组所没有的一些优点，例如能够自动增加容量。

如果 lastName 是一个字符串对象的名称，那么 lastName[i] 就可以访问由 lastName 表示的字符串中的第 i 个字符。显示 9.6 演示了这种方括号数组表示法的用法。

显示 9.6 还演示了成员函数 length。每个字符串对象都有一个名为 length 的成员函数，该函数不接受任何参数，并返回该字符串对象所表示字符串的长度。因此，字符串对象不仅可以像数组一样使用，length 成员函数还使它表现得像一个能够自动记录已占用位置数量的部分填充数组。

对 string 类对象使用数组方括号时，不会检查索引是否合法。如果使用了非法索引（也就是说，索引大于或等于对象中字符串的长度），结果将无法预测，但肯定不会理想。你可能只会得到奇怪的行为，而不会看到任何错误消息来告诉你问题是索引值非法。有一个名为 at 的成员函数会检查索引值是否合法。名为 at 的成员函数基本上与方括号的作用相同，但有以下两点区别：

### 显示 9.6 字符串对象可以像数组一样使用（第 1 部分，共 2 部分）

```
1 //Demonstrates using a string object as if it were an array.
2 #include <iostream>
3 #include <string>
4 using namespace std;

5 int main( )
6 {
7     string firstName, lastName;

8     cout << "Enter your first and last name:\n";
9     cin >> firstName >> lastName;

10    cout << "Your last name is spelled:\n";
11    int i;
```

### 显示 9.6  字符串对象可以像数组一样使用（第 2 部分，共 2 部分）

```
```cpp
for (i = 0; i < lastName.length(); i++)
{
    cout << lastName[i] << " ";
    lastName[i] = '-';
}
cout << endl;
for (i = 0; i < lastName.length(); i++)
    cout << lastName[i] << " "; // Places a "-" under each letter.
cout << endl;

cout << "Good day " << firstName << endl;
return 0;
}
```
```

示例对话

```
```text
Enter your first and last names:
John Crichton
Your last name is spelled:
C r i c h t o n
- - - - - - -
Good day John
```
```

使用 at 时要采用函数表示法，因此不能写成 a[i]，而要写成 a.at(i)；at 成员函数会检查 i 的值是否为非法索引。如果 a.at(i) 中 i 的值是非法索引，你应该会得到一条运行时错误消息，告诉你发生了什么问题。在下面的代码片段中，尝试进行的访问超出了范围，但它很可能不会产生错误消息，尽管代码访问了一个不存在的索引变量：

```
```cpp
string str("Mary");
cout << str[6] << endl;
```
```

不过，下面的示例会导致程序异常终止，因此你至少可以知道出现了问题：

```
```cpp
string str("Mary");
cout << str.at(6) << endl;
```
```

但是请注意，当 a.at(i) 中的索引 i 非法时，有些系统给出的错误消息非常不清楚。

你可以通过向索引变量赋值一个 char 值来改变字符串中的单个字符，例如 str[i]。由于成员函数 at 返回一个引用，因此也可以通过该成员函数完成此操作。例如，要将字符串对象 str 中的第三个字符改为 `'X'`，可以使用以下任一代码片段：

```
```cpp
str.at(2) = 'X';
```
```

或者

str[2] = 'X';

与普通字符数组一样，string 类型对象中的字符位置从 0 开始索引，因此字符串中的第三个字符位于索引位置 2。

显示 9.7 给出了 string 类成员函数的部分列表。

在很多方面，string 类对象比我们在第 9.1 节中介绍的 C 字符串更容易使用。特别是，string 类对象上的 == 运算符会返回符合我们对字符串相等这一直观理解的结果；也就是说，当两个字符串包含顺序相同的相同字符时返回 true，否则返回 false。同样，比较运算符 <、>、<= 和 >= 会使用字典序比较字符串对象。（字典序是按照附录 3 中 ASCII 字符集所给出的符号顺序进行的字母顺序排列。如果字符串只包含字母，并且二者要么全部为大写字母，要么全部为小写字母，那么在这种情况下，字典序就与日常的字母顺序相同。）

### 显示 9.7 标准 string 类的成员函数（第 1 部分，共 2 部分）

| 示例 | 说明 |
|---|---|
| 构造函数 | |
| string str; | 默认构造函数；创建空字符串对象 str。 |
| string str("string"); | 创建一个数据为 `"string"` 的字符串对象。 |
| string str(aString); | 创建字符串对象 str，它是 aString 的副本。aString 是 string 类的对象。 |
| 元素访问 | |
| str[i] | 返回 str 中索引为 i 的字符的可读写引用。 |
| str.at(i) | 返回 str 中索引为 i 的字符的可读写引用。 |
| str.substr(position, length) | 返回调用对象中从 position 开始、长度为 length 个字符的子字符串。 |
| 赋值/修改器 | |
| str1 = str2; | 分配空间并用 str2 的数据对其进行初始化，释放为 str1 分配的内存，并将 str1 的大小设置为 str2 的大小。 |
| str1 += str2; | 将 str2 的字符数据连接到 str1 的末尾；并相应设置大小。 |
| str.empty( ) | 如果 str 是空字符串则返回 true，否则返回 false。 |

