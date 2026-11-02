
格式化；以十进制、八进制和十六进制格式输出整数；以各种精度输出浮点值，强制小数点，以科学记数法和定点记数法输出；在指定宽度的字段中输出对齐的数据；在填充指定字符的字段中输出数据；以及以科学记数法和十六进制记数法输出大写字母。

### 21.3.1 char * 变量的输出

C++ 会自动确定数据类型——这是相对 C 的一项改进，但这一特性有时会“碍事”。例如，假设我们想打印存储在 char * 指针中的地址。<< 运算符已被重载，用于将 char * 输出为以空字符结尾的 C 风格字符串。要输出地址，可以将 char * 强制转换为 void *（这可以对任何指针变量进行）。图 21.3 演示了以字符串格式和地址格式打印 char * 变量。这里的地址以十六进制（基数为 16）数打印——一般来说，地址的打印方式取决于实现。要了解有关十六进制数的更多信息，请参见附录 C。关于控制数字的基数，我们将在第 21.6.1 节和第 21.7.4 节进一步说明。

```cpp
// Fig. 21.3: fig21_03.cpp
// Printing the address stored in a char * variable.
#include <iostream>
using namespace std;

int main()
{
    const char *const word = "again";

    // display value of char *, then display value of char *
    // after a static_cast to void *
    cout << "Value of word is: " << word << endl
         << "Value of static_cast< const void * >( word ) is: "
         << static_cast< const void * >( word ) << endl;
} // end main
```

Value of word is: again
Value of static_cast< const void * >( word ) is: 0135CC70

图 21.3 | 打印存储在 char * 变量中的地址。

### 21.3.2 使用成员函数 put 输出字符

我们可以使用 put 成员函数输出字符。例如，语句 `cout.put( 'A' );` 显示单个字符 A。对 put 的调用可以级联，如语句 `cout.put( 'A' ).put( '\n' );` 所示，它输出字母 A，后跟一个换行字符。与 << 一样，前一条语句按这种方式执行，因为点运算符（.）从左到右结合，并且 put 成员函数返回对接收 put 调用的流对象（cout）的引用。put 函数也可以用一个表示 ASCII 值的数值表达式调用，如下面的语句所示，该语句同样输出 A：

```
cout.put(65);
```

## 21.4 流输入

现在让我们考虑流输入。istream 提供了格式化和非格式化输入功能。流提取运算符（>>）通常会跳过输入流中的空白字符（如空格、制表符和换行符）；稍后我们将看到如何改变这种行为。每次输入后，流提取运算符返回对接收提取消息的流对象的引用（例如表达式 cin >> grade 中的 cin）。如果将该引用用作条件（例如，在 while 语句的循环继续条件中），则会隐式调用流重载的 void * 转换运算符函数，根据上一次输入操作的成功或失败，将该引用转换为非空指针值或空指针。非空指针转换为 bool 值 true 表示成功，空指针转换为 bool 值 false 表示失败。当尝试读取超过流末尾的位置时，流重载的 void * 转换运算符返回空指针，以表示文件结束。

每个流对象都包含一组状态位，用于控制流的状态（即格式化、设置错误状态等）。流重载的 void * 转换运算符使用这些位来确定返回非空指针还是空指针。如果输入了错误类型的数据，流提取会设置流的 failbit；如果操作失败，则会设置流的 badbit。第 21.7 节和第 21.8 节详细讨论流状态位，然后展示在 I/O 操作后如何测试这些位。

### 21.4.1 get 和 getline 成员函数

不带参数的 get 成员函数从指定流中输入一个字符（包括空白字符和其他非图形字符，例如表示文件结束的键序列），并将其作为函数调用的值返回。当在流上遇到文件结束时，这个版本的 get 返回 EOF。

*使用成员函数 eof、get 和 put*

图 21.4 演示了在输入流 cin 上使用成员函数 eof 和 get，以及在输出流 cout 上使用成员函数 put。回想第 4 章，EOF 表示为 int。该程序一次读取一个字符到 character 中，以便测试输入的每个字符是否为 EOF。程序首先打印 cin.eof() 的值——即 false（输出中为 0）——以表明 cin 上尚未发生文件结束。用户输入一行文本并按 Enter，然后按文件结束键（在 Microsoft Windows 系统上为 <Ctrl> z，在 Linux 和 Mac 系统上为 <Ctrl> d）。第 15 行读取每个字符，而第 16 行使用成员函数 put 输出到 cout。遇到文件结束时，while 语句结束，第 20 行显示 cin.eof() 的值，此时为 true（输出中为 1），以表明 cin 上已设置文件结束。该程序使用 istream 成员函数 get 的无参数版本，它返回正在输入的字符（第 15 行）。函数 eof 仅当程序尝试读取超过流中最后一个字符的位置后才返回 true。

```cpp
1 // Fig. 21.4: fig21_04.cpp
2 // get, put and eof member functions.
3 #include <iostream>
4 using namespace std;
5
6 int main()
7 {
8     int character; // use int, because char cannot represent EOF
9
10    // prompt user to enter line of text
11    cout << "Before input, cin.eof() is " << cin.eof() << endl
12         << "Enter a sentence followed by end-of-file:" << endl;
13
14    // use get to read each character; use put to display it
15    while ( ( character = cin.get() ) != EOF )
16        cout.put( character );
17
18    // display end-of-file character
19    cout << "\nEOF in this system is: " << character << endl;
20    cout << "After input of EOF, cin.eof() is " << cin.eof() << endl;
21 } // end main
```

```
Before input, cin.eof() is 0
Enter a sentence followed by end-of-file:
Testing the get and put member functions
Testing the get and put member functions
A-Z
EOF in this system is: -1
After input of EOF, cin.eof() is 1
```

图 21.4 | get、put 和 eof 成员函数。

带字符引用参数的 get 成员函数从输入流中输入下一个字符（即使它是空白字符），并将其存储在字符参数中。这个版本的 get 返回对调用 get 成员函数的 istream 对象的引用。

get 的第三个版本接受三个参数——一个内置 char 数组、一个大小限制和一个分隔符（默认值为 '\n'）。这个版本从输入流中读取字符。它要么读取比指定最大字符数少一个的字符后终止，要么在读到分隔符时立即终止。会插入一个空字符，以终止程序用作缓冲区的字符数组中的输入字符串。分隔符不会被放入字符数组，但仍保留在输入流中（分隔符将是下一个被读取的字符）。因此，连续第二次调用 get 的结果是一个空行，除非从输入流中移除分隔符字符（可能使用 cin.ignore()）。

### 比较 cin 和 cin.get

图 21.5 比较了使用流提取与 cin 的输入（它会读取字符直到遇到空白字符）和使用 cin.get 的输入。对 cin.get 的调用（第 22 行）未指定分隔符，因此使用默认的 '\n' 字符。
