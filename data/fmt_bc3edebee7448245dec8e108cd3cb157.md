
### std::flush

刷新流但不插入换行符。操作符：`std::flush`。示例：

```cpp
cout << flush; // 使用操作符，效果相同
```

### std::unit

只刷新标准输出流。操作符：`std::unit`。示例：

```cpp
cout << unit; // 使用操作符，效果相同
```

### std::dbuf

返回缓冲区并刷新标准输出流。操作符：`std::dbuf`。示例：

```cpp
cout << dbuf; // 使用操作符，效果相同
```

### ios::skipws

从流中提取值时跳过前导空白字符（空格、制表符、换行符等）。这是默认值。如果未设置此标志，则不跳过前导空白字符。操作符：`std::skipws`。示例：

```cpp
cin.setf(ios::skipws);
```

```cpp
cin >> ws; // 使用操作符，效果相同
```

### ios::unitbuf

每次输出操作后设置此标志。通常不需要刷新流，这样做会导致不必要的 I/O 处理。因此，除非明确打算刷新流，否则应避免使用 `unitbuf`。互补标志：`ios::noutbuf`。操作符：`std::unitbuf`, `std::noutbuf`。示例：

```cpp
cout.setf(ios::unitbuf);
cout << endl;
cout.write("xyz", 3); // flush writes wrote.
```

## 6.4 输出

C++ 的输出主要基于 `std::ostream` 类。`ostream` 类定义了将信息插入流的各种运算符和成员：插入运算符 (`<<`) 以及向流写入未格式化信息的特殊成员（如 `write`）。

`ostream` 类作为其他类的基类，提供了 `ostream` 类的功能并添加了它们自身的特性。在接下来的章节中，将讨论以下类：

- `ostream` 类

### 6.4.1 基础输出：‘ostream’ 类

`ostream` 定义了基本的输出设施。`cout`、`clog` 和 `cerr` 对象都是 `ostream` 对象。`ios` 类定义的所有与输出相关的设施在 `ostream` 类中也可用。

我们可以使用以下 `ostream` 构造函数来定义输出对象：

- `std::ostream object(std::streambuf *sb);`

此构造函数创建了一个 `ostream` 对象，它是现有 `streambuf` 对象的封装。无法定义一个用于插入的普通 `ostream` 对象（例如使用 `std::ostream::out`）。当使用 `cout` 或其友元对象时，我们实际上在使用一个已经预定义的 `ostream` 对象，该对象通过一个（也是预定义的）处理实际接口的 `streambuf` 对象来接口处理标准输出。然而，可以通过传递一个空指针来定义一个 `ostream` 对象。此类对象不能用于插入（即当向其插入内容时，它会抛出 `ios::bad`），但它以后可以被赋予一个 `streambuf`。因此，它可以先进行构造，直到合适的时候再提供使用（另见 14.8）。

要在 C++ 源码中定义 `ostream` 类，必须包含 `<iostream>` 头文件。为了确保使用预定义的 `ostream` 对象（`std::cerr`、`std::cout` 等），必须包含 `<iostream>` 头文件。

### 6.4.1 写入 ‘ostream’ 对象

插入运算符 (`<<`) 用于以安全的方式将值插入 `ostream` 对象中。这被称为格式化输出，因为存储在缓冲区内存中的二进制值会根据某些格式化规则转换为人类可读的 ASCII 字符。

插入运算符指向接收信息的流对象。`<<` 的正常结合性保持不变。当遇到类似下面的语句时：

```cpp
cout << "hello " << "world";
```

左侧的操作数首先计算（`cout << "hello "`），并返回一个 `ostream` 对象（该对象实际上是同一个 `cout` 对象）。现在，语句简化为：

```cpp
cout << "world";
```

第二个字符串被插入到 `cout` 中。

`<<` 有很多（重载的）变体，许多类型的变量都可以插入 `ostream` 对象中。它是一个期望 `int`、`double`、指针等类型的重载 `operator<<`。每个运算符都返回已插入插入信息的 `ostream` 对象，然后可以紧跟下一次插入。

流缺乏诸如 C 语言中 `printf` 和 `fprintf` 函数那样的格式化输出设施。虽然在流的世界中实现这些设施并不困难，但 C++ 程序几乎很少需要类似 `printf` 的功能。此外，由于它是类型不安全的，最好完全避免使用。

当写入二进制文件时，不使用也不需要文本格式化：一个 `int` 值应该作为一系列原始字节写入，而不是作为从 0 到 9 的 ASCII 字符。可以使用 `ostream` 对象的以下成员函数来写入“二进制文件”：

- `ostream put(char c);`

向输出流写入单个字符。由于字符是一个字节，此成员函数也可以用于向文本文件写入单个字符。

- `ostream write(char const *buffer, int length);`

将存储在 `char const *buffer` 中的许多字节写入 `ostream` 对象。字节按其在缓冲区中的存储方式写入，完全没有任何格式化。第一个参数是 `char const *`，写入任何其他类型都需要进行类型转换。例如，要以字节值的解释性强制类型转换来写入一个 `int`：

```cpp
int x;
out.write(reinterpret_cast<char const *>(&x), sizeof(int));
```

上述 `write` 写入的字节将根据取决于底层硬件的字节序（endianness）的顺序写入 `ostream`。大端计算机先写入多字节值的最高位字节，小端计算机先写入最低位字节。

### 6.4.1.2 ‘ostream 定位’

虽然不是每个 `ostream` 对象都支持重新定位，但它们通常支持。这意味着可以重写流中写过的某部分。重新定位经常用于可能随机访问信息的应用程序中。

可以使用以下成员获取并修改当前位置：

- `ios::pos_type tellp()`：返回流中下一次操作将进行的文件的当前（绝对）位置。

- `ostream& seekp(ios::off_type step, ios::seekdir org)`：修改流的实际位置。该函数期望一个 `off_type step`，代表流位置相对于 `org` 移动的字节数。`step` 的值可以是负数、零或正数。步进的起点 `org` 是 `ios::seekdir` 枚举中的一个值。其值为：

- `ios::beg`：步长相对于流的开始计算。默认使用此值。

- `ios::cur`：步长相对于流的当前位置（由 `tellp()` 返回）计算。

- `ios::end`：步长相对于流的位置解释。超出最后一个文件位置进行定位或写入是允许的。

虽然不是每个 `ostream` 对象都支持重新定位，但它们通常支持。这意味着可以重写流中写过的某部分。重新定位经常用于可能随机访问信息的应用程序中。

可以使用以下成员获取并修改当前位置：

- `ios::pos_type tellp()`：返回流中下一次操作将进行的文件的当前（绝对）位置。

- `ostream& seekp(ios::off_type step, ios::seekdir org)`：修改流的实际位置。该函数期望一个 `off_type step`，代表流位置相对于 `org` 移动的字节数。`step` 的值可以是负数、零或正数。步进的起点 `org` 是 `ios::seekdir` 枚举中的一个值。其值为：

- `ios::beg`：步长相对于流的开始计算。默认使用此值。

- `ios::cur`：步长相对于流的当前位置（由 `tellp()` 返回）计算。

- `ios::end`：步长相对于流的位置解释。超出最后一个文件位置进行定位或写入是允许的。

### 6.4.3 ‘ostream’ 刷新

除非设置了 `ios::unitbuf` 标志，否则在以下情况下 `ostream` 缓冲区会自动刷新：

- `ostream` 对象销毁；

- 显式调用 `flush()`；

- 遇到 `eof` 等结束操作符。

## 6.4.2 输出：‘ofstream’ 类

`ofstream` 类派自 `ostream` 类，它拥有 `ostream` 类的所有功能，并用于写入文件。要在 C++ 源码中使用 `ofstream`，必须包含 `<fstream>` 头文件。为了确保使用预定义的 `ostream` 对象（`std::cerr`、`std::cout` 等），必须包含 `<iostream>` 头文件。

与其直接将 `ofstream` 对象与文件关联，不如先构造对象再打开。

- `ofstream object`：基本构造函数。

- `ofstream object(char const *name, ios::openmode mode = ios::out);` 将 `ofstream` 对象与实际文件关联。如果在调用 `open` 之前设置了 `ios::fail` 标志，则流会被清除。已经打开的流会失败。要重新关联另一个文件，必须先关闭：

```cpp
ofstream out("/tmp/out2");
out << "hello\n";
out.close(); // 刷新并关闭 out
out.open("/tmp/out2");
out << "world\n";
```

- `void close()`：关闭 `ofstream` 对象。该函数会设置对象的 `ios::fail` 标志。文件会将任何缓冲区刷新到关联的文件。当关联的 `ofstream` 对象销毁时，文件会自动关闭。

- `bool is_open() const`：假设流已正确构造，但尚未附加文件。例如，执行了 `ofstr` 语句。现在我们使用 `good()` 检查其状态，它返回非零（即 OK）值。'good' 状态表示流对象构造正确，并不意味着文件也打开。要测试流是否实际打开，应该调用 `is_open()`。如果返回 `true`，则流是打开的。示例：

```cpp
ofstream out("/tmp/scratch");
```

### 6.4.2.1 打开流对象的模式

在构造或打开 `ofstream`（或 `istream`，见 6.5.2 节）对象时，可以使用以下文件模式或文件。这些值的类型为 `ios::openmode`。可以使用 `|` 运算符组合标志。

- `ios::app`: 在每次输出命令之前将流重新定位到其末尾（另见下文的 `ios::ate`）。如果文件不存在，则创建它。在任何现有内容的中间打开流时

- `ios::ate`: 初始从文件末尾开始。请注意，只有当其他标志允许对象执行此操作时，才会保留现有内容。例如，`ofstream out("gone", ios::ate)` 会重写文件 `gone`，隐含的 `ios::out` 导致了重写。如果应该重写现有文件，应该也指定 `ios::in` 模式。`ate` 模式初始将文件置于文件末尾。之后，可以使用 `seekp` 在文件中间写入信息。使用 `app` 模式时，信息只写入文件末尾（实际上忽略了 `seekp` 操作）。

- `ios::binary`: 以二进制模式打开文件（用于区分文本文件和二进制文件的系统，如 MS-Windows）。

- `ios::in`: 打开文件进行读取。文件必须存在。

- `ios::out`: 打开文件进行写入。如果不存在，则创建它。如果已存在，则重写它。

- `ios::trunc`: 初始从空文件开始。文件的现有内容都会丢失。

以下文件标志的组合具有特殊含义：

| in | out | 含义 |
| :--- | :--- | :--- |
| in | out | 流可以读可写。然而，文件必须存在。 |
| in | out | trunc | 流可以读可写。它首先会（重）创建一个空文件。 |

一个有趣的细节是，`istream`、`ofstream` 和 `fstream` 类的 `open` 成员有一个类型为 `ios::openmode` 的第二个参数。相比此，`|` 运算符应用于两个枚举值时会返回一个 `int`。`|` 运算符在此仍可以使用这里的原因将在随后的章节中回答（参见第 11.13 节）。

## 6.4. 输出

### 6.4.3 输出到内存：'ostream' 类

要使用流设施将信息写入内存，应使用 `std::ostringstream` 对象。`ostringstream` 类派生自 `ostream` 类，`ostream` 的功能对 `ostringstream` 对象同样可用。要使用和定义 `ostringstream` 对象，必须包含头文件 `<sstream>`。此外，`ostringstream` 类提供了以下构造函数和成员：

- `ostringstream ostr(string const &init, ios::openmode mode = ios::out);` 当指定 `openmode=ios::ate` 时，`ostringstream` 对象由字符串初始化，剩余的插入操作将附加到 `ostringstream` 对象的内容之后。

- `ostringstream ostr(ios::openmode mode = ios::out);` 此构造函数也可以作为默认构造函数使用。或者，它允许例如在对象目前为止存储的信息末尾进行强制添加（使用 `ios::app`）。示例：

- `std::string str() const;` 返回存储在 `ostringstream` 对象内部的字符串副本。

- `void str(std::string const &str);` 使用新的初始内容重新初始化当前对象。

```cpp
std::ostringstream out;
```

该示例说明了 `ostringstream` 类的使用；向对象中插入了多个值。然后，`ostringstream` 对象包含的文本存储在 `std::string` 中，其长度和内容被重用。此类 `ostringstream` 对象通常用于进行“类型到字符串”的转换，例如将 `int` 值转换为文本。格式化标志也可以用于 `ostringstream`，因为它们是 `ostream` 类的一部分。

这是一个显示使用 `ostringstream` 对象的示例：

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
    ostr.unset(ios::hex);
    ostr << 12;
    cout << ostr.str() << '\n';

    ostr.str("new text");
    cout << ostr.str() << '\n';

    ostr.seekp(4, ios::beg);
    ostr << "world";
    cout << ostr.str() << '\n';
}
/*
  此程序的输出：
hello
hello 0x0309
hello 0x0309 -- 12
new text
new world
*/
```

### 6.4.4 'put_time' 操纵符

操纵符 `std::put_time(std::tm const *specs, char const *fmt)` 可将时间规范插入 `std::ostream` 对象中。

时间规范由 `std::tm` 对象提供，而时间的显示方式由格式字符串 `fmt` 定义。

从 `chrono::time_point` 开始，必须执行以下步骤将时间点插入 `std::ostream`：

- 获取 `time_point`（例如：`std::system_clock::now()`）；

- 将时间点传递给时钟函数 `time_t`，保存返回的 `time_t` 值：`time_t secs = std::system_clock::to_time_t(std::system_clock::now());`；

- 将 `secs` 的地址传递给 `localtime` 或 `std::localtime`。这些函数返回包含所需时间组件的 `std::tm` 结构，这些组件分别表示计算机的本地时间或 GMT；

- 将 `localtime` 或 `gm` 的返回值与格式字符串（例如 `"%c"`）传递给 `put_time`，将其插入 `std::ostream` 中：可以定义一个返回 `put_time` 返回值并期望 `time_point` 和格式字符串的简单函数，它可以处理上述陈述（例如，为了简便，省略了 `std::` 和 `std::chrono::` 规范）：

```cpp
auto localTime(time_point<system_clock> const tp, char const *fmt)
{
    time_t secs = system_clock::to_time_t(tp);
    return put_time(localtime(&secs), fmt);
}
// 使用方法：
cout << localTime(system_clock::now(), "%c") << '\n';
```
