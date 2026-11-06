
- `ostringstream ostr(ios::openmode mode = ios::out);`

    此构造函数也可以用作默认构造函数。或者，它允许例如将内容强制追加到对象中目前已存储信息的末尾（使用 `ios::app`）。

    示例：

    ```cpp
    std::ostringstream out;
    ```

- `std::string str() const;`

    返回存储在 ostringstream 对象内部的字符串的副本。

- `void str(std::string const &str);`

    使用新的初始内容重新初始化当前对象。

以下示例说明了 `ostringstream` 类的用法：将若干值插入该对象。然后，`ostringstream` 对象中包含的文本被存储到一个 `std::string` 中，随后打印该字符串的长度和内容。此类 `ostringstream` 对象最常用于进行“类型到字符串”的转换，例如将 int 值转换为文本。格式化标志也可以与 `ostringstream` 一起使用，因为它们是 ostream 类的一部分。

下面是一个展示正在使用 `ostringstream` 对象的示例：

```cpp
#include <iostream>
#include <sstream>

using namespace std;

int main()
{
    ostringstream ostr("hello ", ios::ate);

    cout << ostr.str() << '\n';

    ostr.setf(ios::showbase);
    ostr.setf(ios::hex, ios::basefield);
    ostr << 12345;

    cout << ostr.str() << '\n';

    ostr << " -- ";
    ostr.unsetf(ios::hex);
    ostr << 12;

    cout << ostr.str() << '\n';

    ostr.str("new text");
    cout << ostr.str() << '\n';

    ostr.seekp(4, ios::beg);
    ostr << "world";
    cout << ostr.str() << '\n';
}
/*
    Output from this program:
hello
hello 0x3039
hello 0x3039 -- 12
new text
new world
*/
```

## 6.5. 输入

默认情况下，首先跳过所有空白字符，然后提取所有连续的非空白字符。一旦处理完一个提取运算符，就会返回从中提取信息的 `istream` 对象，并且它可以立即用于同一表达式中出现的其他 `istream` 操作。

流缺少用于格式化输入的设施（例如 C 的 `scanf` 和 `vscanf` 函数所使用的设施）。尽管将这些设施添加到流的世界中并不困难，但 C++ 程序中几乎从不需要类似 `scanf` 的功能。此外，由于它可能类型*不安全*，最好完全避免格式化输入。

当必须读取二进制文件时，通常不应格式化信息：`int` 值应作为一系列未更改的字节来读取，而不是作为一系列 ASCII 数字字符 0 到 9 来读取。以下成员函数可用于从 `istream` 对象读取信息：

- `int gcount() const:`

    返回上一次未格式化输入操作从输入流中读取的字符数。

- `int get():`

    下一个可用的单个字符以 `unsigned char` 值的形式返回，并使用 `int` 返回类型。如果没有更多字符可用，则返回 `EOF`。

- `istream& get(char &ch):`

    从输入流读取的下一个单个字符存储在 `ch` 中。该成员函数返回流本身，可以检查该流以确定是否获取到了字符。

- `istream& get(char *buffer, int len, char delim = '\n'):`

    最多从输入流读取 `len - 1` 个字符到从 `buffer` 开始的数组中，该数组长度至少应为 `len` 字节。遇到分隔符 `delim` 时读取也会停止。然而，分隔符本身*不会从输入流中移除*。

    将字符存储到 `buffer` 后，会在存储到 `buffer` 的最后一个字符之后写入一个 ASCII-Z 字符。如果在读取 `len - 1` 个字符之前遇到分隔符，或者在读取 `len - 1` 个字符之后未遇到分隔符，则函数 `eof` 和 `fail`（见第 6.3.1 节）返回 0（`false`）。可以指定 ASCII-Z 分隔符：这样就能从（二进制）文件中读取以 ASCII-Z 字符结尾的字符串。

- `istream& getline(char *buffer, int len, char delim = '\n'):`

    此成员函数的操作与 `get` 成员函数类似，但如果实际遇到 `delim`，`getline` 会将其从流中移除。如果遇到分隔符本身，则它*不会*存储在 `buffer` 中。如果（在读取 `len - 1` 个字符之前）*未*找到 `delim`，则 `fail` 成员函数以及可能还有 `eof` 会返回 true。请注意，`std::string` 类还提供了一个函数 `std::getline`，通常优先于这里描述的 `getline` 成员函数（见第 5.2.4 节）。

- `istream& ignore():`

    从输入流中跳过一个字符。

- `istream& ignore(int n):`

    从输入流中跳过 `n` 个字符。

- `istream& ignore(int n, int delim):`

    最多跳过 `n` 个字符，但在从输入流中移除 `delim` 后停止跳过字符。

- `int peek()`:

    此函数返回下一个可用的输入字符，但不会实际从输入流中移除该字符。如果没有更多字符可用，则返回 EOF。

- `istream& putback(char ch)`:

    字符 `ch` 被推回输入流，以便再次作为下一个可用字符读取。如果不允许这样做，则返回 EOF。通常，可以推回一个字符。示例：

    ```
    string value;
    cin >> value;
    cin.putback('X');
                 // displays: X

    cout << static_cast<char>(cin.get());
    ```

- `istream& read(char *buffer, int len)`:

    最多从输入流读取 `len` 个字节到缓冲区中。如果先遇到 EOF，则读取的字节数会更少，此时成员函数 `eof` 返回 true。此函数通常在读取*二进制*文件时使用。第 6.5.2 节包含一个使用此成员函数的示例。成员函数 `gcount()` 可用于确定 `read` 取回的字符数。

- `istream& readsome(char *buffer, int len)`:

    最多从输入流读取 `len` 个字节到缓冲区中。所有可用字符都会被读入缓冲区，但如果遇到 EOF，则读取的字节数会更少，且不会设置 `ios::eofbit` 或 `ios::failbit`。

- `istream& unget()`:

    将最近从流中读取的字符放回。

### 6.5.1.2 ‘istream’ 定位

尽管并非每个 iostream 对象都支持重新定位，但有些对象支持。这意味着可以重复读取流中的同一部分。重新定位经常用于*数据库应用程序*，在这些程序中必须能够随机访问数据库中的信息。

可以使用以下成员获取和修改当前位置：

- `ios::pos_type tellg()`:

    返回流当前的（绝对）位置，即流的下一读取操作将发生的位置。

- `istream& seekg(ios::off_type step, ios::seekdir org)`:

    修改流的实际位置。该函数需要一个 `off_type step`，表示当前流位置相对于 `org` 移动的字节数。步长值可以为负、零或正。

    步长的原点 `org` 是 `ios::seekdir` 枚举中的一个值。其值为：

    - `ios::beg`:

        步长相对于流的开头计算。默认使用此值。

    - `ios::cur`:

        步长相对于流的当前位置（由 `tellg` 返回）计算。

    - `ios::end`:

        步长相对于流的当前末尾位置解释。

可以定位到超过文件最后位置的位置。定位到 `ios::beg` 之前会设置 `ios::failbit` 标志。

### 6.5.2 从文件输入：类 ‘ifstream’

std::ifstream 类派生自 istream 类：它具有与 istream 类相同的能力，但可用于访问文件以进行读取。

为了在 C++ 源代码中使用 ifstream 类，必须包含 fstream 头文件。包含 fstream 不会自动提供标准流 cin、cout 和 cerr。包含 iostream 以声明这些标准流。

以下构造函数可用于 ifstream 对象：

- `ifstream object`:

    这是基本构造函数。它定义一个 ifstream 对象，之后可以使用其 `open()` 成员将其与实际文件关联（见下文）。

- `ifstream object(char const *name, ios::openmode mode = ios::in)`:

    此构造函数可用于定义一个 ifstream 对象，并使用输入模式 mode 立即将其与名为 name 的文件关联。第 6.4.2.1 节概述了可用的输入模式。示例：

    ```cpp
    ifstream in("/tmp/input");
    ```

    也可以不直接将 ifstream 对象与文件关联，而是先构造该对象，之后再打开它。

- `void open(char const *name, ios::openmode mode = ios::in)`:

    此成员函数用于将 ifstream 对象与实际文件关联。如果在调用 open 之前已设置 `ios::fail` 标志，并且打开成功，则该标志会被清除。打开已经打开的流会失败。要将流重新关联到另一个文件，必须先关闭它：

    ```cpp
    ifstream in("/tmp/in");
    in >> variable;
    in.close();        // closes in
    in.open("/tmp/in2");
    in >> anotherVariable;
    ```

- `void close()`:

    此成员函数关闭 ifstream 对象。该函数会设置已关闭对象的 `ios::fail` 标志。关闭文件会将任何缓冲的信息刷新到关联文件。当关联的 ifstream 对象不再存在时，文件会自动关闭。

- `bool is_open() const`:

    假设一个流已被正确构造，但尚未附加到文件。例如，已执行语句 `ifstream ostr`。当我们现在通过 `good()` 检查其状态时，会返回一个非零（即正常）值。此处的“good”状态表示流对象已正确构造。这并不意味着文件也已打开。要测试流是否实际打开，应调用 `is_open`。如果它返回 true，则
