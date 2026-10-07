

# 第 17 章 输入、输出与文件

限制了文件名中的字符数量，以及 `tmpnam()` 在当前目录下不生成重复文件名的情况下可调用的最大次数。以下示例生成了 10 个临时名称：

```cpp
#include <stdio>
#include <iostream>

int main() {
    using namespace std;
    cout << "This system can generate up to " << TMP_MAX
         << " temporary names of up to " << L_tmpnam
         << " characters.\n";
    char pszName[L_tmpnam] = {'\0'};
    cout << "Here are ten names:\n";
    for (int i=0; i<10; i++) {
        tmpnam(pszName);
        cout << pszName << endl;
    }
    return 0;
}
```

更通地说，通过使用 `tmpnam()`，你现在可以生成 `TMP_MAX` 个唯一的文件名，每个名称最多包含 `L_tmpnam` 个字符。名称本身取决于编译器。你可以运行此程序来查看你的编译器产生了哪些名称。

## 内存内格式化 (Incore Formatting)

iostream 族支持程序与终端之间的 I/O。fstream 族使用相同的接口提供程序与文件之间的 I/O。C++ 库还提供了一个 `ostream` 族，它使用相同的接口提供程序与字符串对象之间的 I/O。也就是说，你可以使用在处理 `cout` 时用过的 `ostream` 方法将格式化信息写入字符串对象，并可以使用如 `getline()` 等 `istream` 方法从字符串对象读取信息。从字符串对象读取格式化信息或向字符串对象写入格式化信息的过程被称为内存内格式化（inline formatting）。让我们简单查看这些设施。`sstream` 族取代了支持字符数组的 `sstream` 头文件。

`sstream` 头文件定义了一个派生自 `ostream` 类的 `ostringstream` 类。还有一个基于 `wstream` 的 `wstringstream` 类（用于宽字符）。如果你创建一个字符串对象，你可以向它写入信息并由它进行存储。你可以对 `ostringstream` 对象使用与 `cout` 相同的方法。也就是说，你可以执行如下所示的操作：

```cpp
stringstream outstr;
double price = 380.0;
char* ps = " for a copy of the ISO/IEC C++ standard!";

outstr.precision(2);

outstr << "Pay only CHF " << price << ps << endl;
```

格式化文本进入缓冲区，该对象使用动态内存分配根据需要扩展缓冲区大小。`ostringstream` 类有一个名为 `str()` 的成员函数，它返回一个由缓冲区内容初始化的字符串对象：

```cpp
string mes = outstr.str(); // 返回带有格式化信息的字符串
```

使用 `str()` 方法会“冻结”该对象，你将无法向其写入内容。列表 17.21 出了一个内存内格式化的简短示例。

## 列表 17.21 strout.cpp

```cpp
// strop.cpp -- 内存内格式化（输出）
#include <iostream>
#include <sstream>
#include <string>
int main()
{
    using namespace std;
    ostringstream outstr; // 管理字符串流

    string hdisk;
    cout << "What's the name of your hard disk? ";
    getline(cin, hdisk);
    int cap;
    cout << "What's its capacity in GB? ";
    cin >> cap;
    // 将格式化信息写入字符串流
    outstr << "The hard disk " << hdisk << " has a capacity of "
        << cap << " gigabytes.\n";
    string result = outstr.str(); // 保存结果
    cout << result; // 显示内容

    return 0;
}
```

以下是列表 17.21 中程序的示例运行：

```What's the name of your hard disk? Datarapture
What's its capacity in GB? 2000
The hard disk Datarapture has a capacity of 2000 gigabytes.
```

`ostringstream` 类允许你使用 `istream` 族的方法从 `istringstream` 对象读取数据，该对象可以从字符串对象初始化。

假设 `facts` 是一个字符串对象。要创建一个与该字符串关联的 `stringstream` 对象，可以使用以下代码：

```cpp
stringstream instr(facts); // 使用 facts 初始化流
```

然后你使用 `istream` 方法从 `instr` 读取数据。例如，如果 `instr` 包含一组字符格式的整数，你可以如下读取：

```cpp
int n;
int sum = 0;
while (instr >> n)
    sum += n;
```

列表 17.22 使用重载的 `>>` 运算符一次一次读取字符串的内容。

## 列表 17.22 strcin.cpp

```cpp
// strcin.cpp -- 从字符数组进行格式化读取
#include <iostream>
#include <sstream>
#include <string>
int main()
{
    using namespace std;
    string lit = "It was a dark and stormy day, and the full moon glowed brilliantly";
    istringstream instr(lit); // 使用 lit 用于输入
    string word;
    while (instr >> word) // 一次读取一个单词
        cout << word << endl;
    return 0;
}
```

这里是列表 17.22 中程序的输出：

```It
was
a
dark
and
stormy
day,
and
the
full
moon
glowed
brilliantly.
```

## 总结

流是进入或流内存的字节流。缓冲区是内存中的临时存放区域，充当程序与文件之间的中介。信息可以使用磁盘驱动器等大数据块在缓冲区和文件之间传输。C++ 通过将缓冲流连接到程序及其源头来处理输入。同样，C++ 通过将缓冲流连接到程序及其目标来处理输出。`istream` 和 `ofstream` 头文件定义了一系列丰富的类，用于管理流。包含 `istream` 文件的 C++ 程序会自动打开流，并用对象管理它们。`cin` 对象连接到标准输入设备（默认是键盘）。`cout` 对象管理标准输出流，该流连接到标准输出设备（通常是显示器）。`cerr` 和 `clog` 对象管理连接到标准错误设备的无缓冲区的流和带缓冲区的流。

I/O 类库提供了多种实用方法。`istream` 类定义了提取运算符（`>>`）的版本，以识别所有基本的 C++ 类型并将输入转换为这些类型。`get()` 方法和 `getline()` 方法为单字符输入和字符串输入提供了进一步的支持。`ostream` 类定义了插入运算符（`<<`）的版本，以识别所有基本的 C++ 类型并将其转换为适当的字符输出。`put()` 方法为单字符输出提供了进一步的支持。`istream` 和 `ostream` 类为宽字符提供了类似的支持。

你可以使用 `ios_base` 类方法以及在 `istream` 和 `iomanip` 头文件中定义的操纵符（可以与插入运算符连接的函数）来控制格式化输出。这些方法和操纵符允许你控制数制、字段宽度、显示的小数、用于显示浮点值的系统以及其他元素。

`ofstream` 头文件提供了类定义，这些将 `istream` 方法扩展到文件 I/O。`ofstream` 类将 `istream` 对象与文件关联，你可以使用所有的 `istream` 方法来读取文件。同样，将 `ostream` 对象与文件关联允许你使用 `ostream` 方法写入文件。将 `ofstream` 对象与文件关联则允许你对该文件同时使用输入和输出方法。

要将文件与流关联，你可以在初始化流对象时提供文件名，或者也可以创建一个文件流对象并使用 `open()` 方法将流与文件关联。`close()` 方法终止连接。

