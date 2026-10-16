

```
public:
Token_stream(istream& s) : ip{&s}, owns{false} { }
Token_stream(istream* p) : ip{p}, owns{true} { }
~Token_stream() { close(); }
Token get(); // read and return next token
Token& current(); // most recently read token
void set_input(istream& s) { close(); ip = &s; owns=false; } void set_input(istream* p) { close(); ip = p; owns = true; }
private:
void close() { if (owns) delete ip; }
istream *ip; // pointer to an input stream
bool owns; // does the Token_stream own the istream?
Token ct {Kind::end} ; // current token
};
```

我们用一个输入流初始化一个 Token_stream (§4.3.2, 第38章)，它从中获取字符。Token_stream 遵循的约定是：它拥有作为指针传入的 istream（并最终删除它；§3.2.1.2, §11.2），但不拥有作为引用传入的 istream。这对于这个简单的程序来说可能有点复杂，但对于持有指向需要销毁的资源的指针的类来说，这是一种有用且通用的技术。

一个 Token_stream 持有三个值：指向其输入流的指针（ip）、一个布尔值（owns），表示是否拥有输入流，以及当前标记（ct）。

我给 ct 一个默认值，因为不这样做显得粗心。人们不应该在调用 get() 之前调用 current()，但如果他们这样做了，他们会得到一个定义良好的 Token。我选择 Kind::end 作为 ct 的初始值，这样如果程序误用 current()，也不会得到一个不在输入流中的值。

我分两个阶段介绍 Token_stream::get()。首先，我提供一个看似简单但给用户带来负担的版本。接下来，我将其修改为略显不那么优雅但使用起来容易得多的版本。get() 的思路是读取一个字符，用该字符决定需要组成哪种标记，在需要时读取更多字符，然后返回表示所读字符的 Token。

初始语句从 *ip（ip 指向的流）读取第一个非空白字符到 ch 中，并检查读取操作是否成功：

```
Token Token_stream::get()
{
char ch = 0; *ip>>ch;

switch (ch) {
case 0:
return ct={Kind::end}; // assign and return
```

默认情况下，operator >> 会跳过空白（即空格、制表符、换行符等），并且如果输入操作失败，则 ch 的值保持不变。因此，ch==0 表示输入结束。

赋值是一个运算符，赋值的结果是被赋值变量的值。这使我能够在同一语句中将值 Kind::end 赋给 ct 并返回它。单条语句而不是两条语句在维护时很有用。如果赋值和返回在代码中被分开，程序员可能会更新其中一个而忘记更新另一个。

还要注意 {}-list 记法（§3.2.1.3, §11.3）在赋值右手侧的使用。那是一个表达式。我本可以把该 return 语句写成：

```
ct.kind = Kind::end; // assign
return ct; // return
```

然而，我认为将一个完整的对象 {Kind::end} 赋值为更清晰，而不是处理 ct 的各个成员。{Kind::end} 等价于 {Kind::end,0,0}。如果我们关心 Token 的后两个成员，这很好；如果我们担心性能，这就不太好。这里两者都不是，但一般来说，处理完整对象比单独操作数据成员更清晰、更不易出错。下面的案例给出了另一种策略的例子。

在考虑完整函数之前，先分别考虑其中的一些案例。表达式终止符 ‘;’、括号和运算符的处理很简单，只需返回它们的值：

```
case ‘;’: // end of expression; print
case ‘*’:
case ‘/’:
case ‘+’:
case ‘-’:
case ‘(’:
case ‘)’:
case ‘=’:
return ct={static_cast<Kind>(ch)};
```

需要 static_cast（§11.5.2），因为没有从 char 到 Kind 的隐式转换（§8.4.1）；只有某些字符对应 Kind 值，所以我们必须在此情况下“认证” ch。

数字的处理如下：

```
case ‘0’: case ‘1’: case ‘2’: case ‘3’: case ‘4’: case ‘5’: case ‘6’: case ‘7’: case ‘8’: case ‘9’: case ‘.’:
ip->putback(ch); // put the first digit (or .) back into the input stream
*ip >> ct.number_value; // read the number into ct
ct.kind=Kind::number;
return ct;
```

将 case 标签水平堆叠而不是垂直堆叠通常不是一个好主意，因为这种排列更难阅读。然而，为每个数字写一行很繁琐。因为 operator >> 已经为读取浮点值到 double 定义，所以代码很简单。首先，初始字符（数字或点）被放回 cin。然后，浮点值可以被读入 ct.number_value。

如果标记不是输入结束、运算符、标点字符或数字，它必须是名称。名称的处理方式与数字类似：

```
default: // name,name =, or error
if (isalpha(ch)) {
ip->putback(ch); // put the first character back into the input stream
*ip>>ct.string_value; // read the string into ct
ct.kind=Kind::name;
return ct;
}
```

最后，我们可能只是遇到错误。处理错误的简单但相当有效的方法是调用 error() 函数写出错误，然后如果 error() 返回则返回一个 print 标记：

```
error("bad token");
return ct={Kind::print};
```

标准库函数 isalpha()（§36.2.1）用于避免将每个字符作为单独的 case 标签列出。应用于字符串的 operator >> 会一直读取到遇到空白。因此，用户必须在以名称作为操作数的运算符之前用空格终止名称。这并不理想，所以我们将在 §10.2.3 中回到这个问题。

下面，终于给出了完整的输入函数：

```
Token Token_stream::get()
{
char ch = 0; *ip>>ch;

switch (ch) {
case 0:
return ct={Kind::end}; // assign and return

case ';': // end of expression; print
case '*':
case '/':
case '+':
case '-':
case '(': 
case ')':
case '=':

return ct={static_cast<Kind>(ch)};
case '0': case '1': case '2': case '3': case '4': case '5': case '6': case '7': case '8': case '9': case '.':

ip->putback(ch); // put the first digit (or .) back into the input stream
*ip >> ct.number_value; // read number into ct
ct.kind=Kind::number;
return ct;

default: // name,name =, or error
```

标准库函数 **isspace()** 提供了对空白的标准化测试（§36.2.1）；**isspace(c)** 如果 **c** 是空白字符则返回非零值，否则返回零。该测试以表查找实现，因此使用 **isspace()** 比测试各个空白字符要快得多。类似的函数测试字符是否为数字（**isdigit()**）、字母（**isalpha()**）或数字或字母（**isalnum()**）。

跳过空白后，下一个字符用于确定即将出现的词法标记的类型。

由 **>>** 读取到字符串直到遇到空白所引起的问题是通过一次读取一个字符，直到找到不是字母或数字的字符来解决的：

```
default: // NAME, NAME=, or error
if (isalpha(ch)) {
    string_value = ch;
    while (ip->get(ch) && isalnum(ch))
        string_value += ch; // append ch to end of string_value
    ip->putback(ch);
    return ct={Kind::name};
}
```

幸运的是，这两个改进都可以通过修改代码的单个局部部分来实现。构造程序使其改进仅通过局部修改即可实现是一个重要的设计目标。

你可能会担心一次一个地向 **string** 的末尾添加字符会效率低下。对于非常长的 **string** 来说确实如此，但所有现代 **string** 实现都提供“小字符串优化”（§19.3.3）。这意味着处理我们可能在计算器中（甚至在编译器中）用作名称的那种字符串不会涉及任何低效操作。特别是，使用短 **string** 不需要使用自由存储。短 **string** 的最大字符数取决于实现，但 14 是一个不错的猜测。

## 10.2.4 错误处理

检测和报告错误总是很重要的。然而，对于这个程序，简单的错误处理策略就足够了。**error()** 函数只是计数错误、写出错误消息并返回：

```
int no_of_errors;

double error(const string& s)
{
    no_of_errors++;
    cerr << “error: ” << s << '\n';
    return 1;
}
```

流 **cerr** 是一个通常用于报告错误的无缓冲输出流（§38.1）。

返回值的理由是错误通常发生在

