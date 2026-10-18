

# DISPLAY 8.4 使用类 `string` 的程序

```cpp
//Demonstrates the standard class string.
#include <iostream>
#include <string>
using namespace std;

int main( )
{
    string phrase;
    string adjective("fried"), noun("ants");
    string wish = "Bon appetit!";

    phrase = "I love " + adjective + " " + noun + "!";
    cout << phrase << endl;
    cout << wish << endl;

    return 0;
}
```

*初始化为空字符串*

*初始化字符串变量的两种方式*

## Sample Dialogue

```
I love fried ants!
Bon appetit!
```

# 类 `string`

类 `string` 可用于表示字符组成的字符串值。类 `string` 提供的字符串表示比第 8.1 节讨论的 C 字符串更灵活。

类 `string` 定义在同名库 `<string>` 中，其定义放在 std 命名空间中。因此，使用类 `string` 的程序应包含以下内容（或大致等价的内容）：

```cpp
#include <string>
using namespace std;
```

类 `string` 有一个默认构造函数，将 `string` 对象初始化为空字符串，还有一个构造函数接受 C 字符串作为参数，并将 `string` 对象初始化为表示作为参数给出的字符串的值。例如：

```cpp
string s1, s2("Hello");
```

# 使用类 string 的 I/O

你可以使用插入运算符 << 和 cout 输出 string 对象，就像对其他类型的数据一样。这在 Display 8.4 中有所说明。使用类 string 进行输入则稍微复杂一些。

提取运算符 >> 和 cin 对 string 对象的工作方式与对其他数据相同，但请记住提取运算符会忽略初始空白，并在遇到更多空白时停止读取。这对字符串同样适用。例如，考虑以下代码：

```
string s1, s2;
cin >> s1;
cin >> s2;
```

如果用户输入

```
May the hair on your toes grow long and curly!
```

那么 s1 将接收值 "May"，删除任何前导（或尾随）空白。变量 s2 接收字符串 "the"。使用提取运算符 >> 和 cin，你只能读取单词；你无法读取包含空白的行或其他字符串。有时这正是你想要的，但有时却完全不是你想要的。

如果你希望程序将整行输入读入 string 类型的变量，可以使用函数 getline。使用 getline 与 string 对象时的语法与我们在第 8.1 节中对 C 字符串描述的略有不同。你不使用 cin.getline；相反，你将 cin 作为 getline 的第一个参数。²（因此，这个版本的 getline 不是成员函数。）

```
string line;
cout << "Enter a line of input:\n";
getline(cin, line);
cout << line << "END OF OUTPUT\n";
```

嵌入完整程序中时，此代码会产生如下对话：

```
Enter some input:
Do bedo to you!
Do bedo to you!END OF OUTPUT
```

如果该行有前导或尾随空白，则它们也会成为 getline 读取的字符串值的一部分。这个版本的 getline 在库 <string> 中。你可以使用连接到文本文件的流对象代替 cin 来使用 getline 从文件进行输入。

你不能使用 cin 和 >> 读取空白字符。如果你想一次读取一个字符，可以使用 cin.get，我们在第 6 章中讨论过。函数 cin.get 读取类型为 char 的值，而不是类型为 string 的值，但在处理字符串输入时可能很有帮助。Display 8.5 包含一个程序，说明了 getline 和 cin.get 用于字符串输入。函数 newLine 的意义在 Pitfall 小节“Mixing cin >> variable and getline”中解释

# DISPLAY 8.5 使用类 `string` 的程序（第 1 部分，共 2 部分）

```
//Demonstrates getline and cin.get.
#include <iostream>
#include <string>
void newLine( );
int main( )
{
    using namespace std;
  
    string firstName, lastName, recordName;
    string motto = "Your records are our records.";

    cout << "Enter your first and last name:\n";
    cin >> firstName>>lastName;
    newLine( );

    recordName = lastName + ", " + firstName;
    cout << "Your name in our records is: ";
    cout << recordName<<endl;

    cout << "Our motto is\n"
        << motto <<endl;
    cout << "Please suggest a better (one-line) motto:\n";
    getline(cin, motto);
    cout << "Our new motto will be:\n";
    cout << motto <<endl;

    return 0;
}
  
//Uses iostream:
void newLine( )
{
    using namespace std;
```

# DISPLAY 8.5 使用类 `string` 的程序（第 2 部分，共 2 部分）

```
char nextChar;
do
{
    cin.get(nextChar);
} while (nextChar != '\n');
}
```

## Sample Dialogue

Enter your first and last name:
B'Elanna Torres
Your name in our records is: Torres, B'Elanna
Our motto is
Your records are our records.
Please suggest a better (one-line) motto:
Our records go where no records dared to go before.
Our new motto will be:
Our records go where no records dared to go before.

# 使用 string 对象的 I/O

你可以使用插入运算符 << 与 cout 输出 string 对象。你可以使用提取运算符 >> 和 cin 输入字符串。使用 >> 进行输入时，代码会读取以空白分隔的字符串。你可以使用函数 getline 将整行文本输入到 string 对象中。

## EXAMPLES

```
string greeting("Hello"), response, nextWord;
cout << greeting << endl;
getline(cin, response);
cin >> nextWord;
```

# SELF-TEST EXERCISES

15. 考虑以下代码（并假设它嵌入在完整且正确的程序中然后运行）：

```
string s1, s2;
cout << "Enter a line of input:\n";
cin >> s1 >> s2;
cout << s1 << "*" << s2 << "<END OF OUTPUT>";
```

如果对话如下开始，下一个输出行会是什么？

Enter a line of input:

A string is a joy forever!

16. 考虑以下代码（并假设它嵌入在完整且正确的程序中然后运行）：

```
string s;
cout << "Enter a line of input:\n";
getline(cin, s);
cout << s << "<END OF OUTPUT>";
```

如果对话如下开始，下一个输出行会是什么？

Enter a line of input:

A string is a joy forever!

# PROGRAMMING TIP More Versions of getline

到目前为止，我们描述了使用 `getline` 的以下方式：

```
string line;
cout << "Enter a line of input:\n";
getline(cin, line);
```

此版本在遇到换行符 '\n' 时停止读取。有一种版本允许你指定不同的字符作为停止信号。例如，以下将在遇到第一个问号时停止：

```
string line;
cout << "Enter some input:\n";
getline(cin, line, '?');
```

有意义地将 `getline` 用作 *void* 函数，但它实际上返回对第一个参数的引用，即上述代码中的 `cin`。因此，以下将从 `s1` 读取一行文本，并将非空白字符的字符串读入 `s2`。

```
string s1, s2;
getline(cin, s1) >> s2;
```

调用 `getline(cin,s1)` 返回对 `cin` 的引用，因此在调用 `getline` 之后发生的下一件事等价于

```
cin >> s2;
```

这种使用 getline 的方式似乎是为 C++ 问答节目设计的，而不是为了满足任何实际编程需求，但有时它会派上用场。

# PITFALL Mixing cin >> variable; and getline

在使用 cin >> variable; 进行输入时要小心混合使用 getline 进行输入。例如，考虑以下代码：

```
int n;
string line;
cin >> n;
getline(cin, line);
```

# 用于类 string 对象的 getline

用于 string 对象的 getline 函数有两个版本：

```
istream& getline(istream& ins, string& strVar, char delimiter);
```

和

```
istream& getline(istream& ins, string& strVar);
```

此函数的第一个版本从作为第一个参数给出的 istream 对象读取字符（在本章中始终为 cin），将字符插入到字符串变量 strVar 中，直到遇到分隔符字符的实例。分隔符字符从输入中删除并丢弃。第二个版本使用 '\n' 作为 delimiter 的默认值；否则，它的工作方式相同。

这些 getline 函数返回它们的第一个参数（在本章中始终为 cin），但它们通常被用作 void 函数。

当此代码读取以下输入时，你可能会期望 n 的值被设置为 42，line 的值被设置为表示 "Hello hitchhiker." 的字符串值：

```
42
Hello hitchhiker.
```

然而，虽然 n 确实被设置为 42 的值，但 line 被设置为等于空字符串。发生了什么？

使用 cin >> n 会跳过输入上的前导空白，但会为下一次输入留下该行的其余部分，在本例中只是 '\n'。像这样的语句

```
cin >> n;
```
