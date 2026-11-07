
也就是说，计算机存储的不是字符，而是该值（通常是 64 位的 double）的二进制表示。对于字符，其二进制表示与文本表示相同——即字符的 ASCII 码（或等价物）的二进制表示。然而，对于数字来说，二进制表示与文本表示差别很大（见图 17.7）。

![](img/9afc44517b591d64e2e19f623c9308ef_1142_0.png)

每种格式都有其优点。文本格式易于阅读。借助它，你可以使用普通的编辑器或文字处理器来读取和编辑文本文件。你可以轻松地将文本文件从一种计算机系统传输到另一种。二进制格式对于数字来说更精确，因为它存储了值的精确内部表示。没有转换错误或舍入错误。以二进制格式保存数据可能更快，因为没有转换，而且可能可以将数据以更大的块保存。二进制格式通常占用更少的空间，具体取决于数据的性质。然而，如果新系统对值使用不同的内部表示，传输到另一个系统可能会成为问题。即使是同一系统上的不同编译器，也可能对结构布局使用不同的内部表示。在这种情况下，你（或其他人）可能必须编写程序将一种数据格式转换为另一种。

让我们看一个更具体的例子。考虑下面的结构定义和声明：

```cpp
const int LIM = 20;
struct planet
{
    char name[LIM];       // name of planet
    double population;    // its population
    double g;             // its acceleration of gravity
};
planet pl;
```

要以文本形式保存结构 `pl` 的内容，可以使用以下代码：

```cpp
ofstream fout("planets.dat", ios_base::out | ios_base::app);
fout << pl.name << " " << pl.population << " " << pl.g << "\n";
```

注意，你必须使用成员运算符显式提供每个结构成员，而且必须分隔相邻数据以便阅读。如果结构包含（比如）30 个成员，这可能会变得很繁琐。

要以二进制格式保存相同的信息，可以使用以下代码：

```cpp
ofstream fout("planets.dat",
             ios_base::out | ios_base::app | ios_base::binary);
fout.write((char *)&pl, sizeof pl);
```

这段代码使用计算机的内部数据表示将整个结构保存为一个单元。你将无法将文件作为文本来读取，但信息将比文本格式存储得更紧凑、更精确。而且，键入这些代码当然也更简单。这种方法带来了两个变化：

- 它使用了二进制文件模式。
- 它使用了 `write()` 成员函数。

让我们更仔细地研究这些变化。

有些系统（如 Windows）支持两种文件格式：文本和二进制。如果要以二进制形式保存数据，应使用二进制文件格式。在 C++ 中，通过在文件模式中使用 `ios_base::binary` 常量来实现。如果想知道为什么在 Windows 系统上应该这样做，请查看以下侧边栏“二进制文件和文本文件”中的讨论。

> ### 二进制文件和文本文件
>
> 使用二进制文件模式会使程序将数据从内存传输到文件，或反之，而不发生任何隐藏的转换。默认的文本模式则未必如此。例如，考虑 Windows 文本文件。它们用两个字符的组合来表示换行：回车符和换行符。Macintosh 文本文件用回车符表示换行。Unix 和 Linux 文件用换行符表示换行。C++ 在 Unix 上成长起来，也用换行符表示换行。为了可移植性，Windows C++ 程序在写入文本模式文件时，会自动将 C++ 换行符转换为回车符和换行符；而 Macintosh C++ 程序在写入文件时会将换行符转换为回车符。在读取文本文件时，这些程序会将本地换行符转换回 C++ 形式。文本格式可能会给二进制数据带来问题，因为 double 值中间的一个字节可能与换行符的 ASCII 码具有相同的位模式。此外，在检测文件结尾的方式上也存在差异。因此，在以二进制格式保存数据时，应使用二进制文件模式。（Unix 系统只有一种文件模式，因此在 Unix 上二进制模式与文本模式相同。）

要以二进制形式而不是文本形式保存数据，可以使用 `write()` 成员函数。回忆一下，此方法将指定数量的字节从内存复制到文件。本章前面使用它复制文本，但它可以逐字节复制任何类型的数据而无需转换。例如，如果将一个 `long` 变量的地址传递给它，并告诉它复制 4 个字节，它就会逐字地将构成该 `long` 值的 4 个字节复制到文件中，而不会将其转换为文本。唯一不方便的是，你必须将地址类型转换为指向 char 的指针类型。你可以使用相同的方法复制整个 planet 结构。要获取字节数，可以使用 `sizeof` 运算符：

```cpp
fout.write( (char *) &pl, sizeof pl);
```

该语句使程序转到 `pl` 结构的地址，并从该地址开始将 36 个字节（`sizeof pl` 表达式的值）复制到与 `fout` 连接的文件。

要从文件中恢复信息，可以使用对应的 `read()` 方法和 `ifstream` 对象：

```cpp
ifstream fin("planets.dat", ios_base::in | ios_base::binary);
fin.read((char *) &pl, sizeof pl);
```

这会将 `sizeof pl` 字节从文件复制到 `pl` 结构。同样的方法可用于不使用虚函数的类。在这种情况下，只保存数据成员，而不保存方法。如果类确实有虚方法，那么指向虚函数指针表的隐藏指针也会被复制。因为下次运行程序时，虚函数表可能位于不同的位置，从文件复制旧指针信息到对象中可能会造成破坏。（另请参阅编程练习 6 中的注释。）

> **提示**
>
> `read()` 和 `write()` 成员函数互为补充。你可以使用 `read()` 来恢复已通过 `write()` 写入文件的数据。

程序清单 17.19 使用这些方法创建和读取二进制文件。在形式上，该程序与程序清单 17.18 类似，但它使用 `write()` 和 `read()` 而不是插入运算符和 `get()` 方法。它还使用操纵符来格式化屏幕输出。

> **注意**
>
> 虽然二进制文件的概念是 ANSI C 的一部分，但一些 C 和 C++ 实现并不提供对二进制文件模式的支持。这种疏忽的原因是，一些系统首先只有一种文件类型，因此你可以在标准文件格式上使用 `read()` 和 `write()` 等二进制操作。因此，如果你的实现将 `ios_base::binary` 视为无效常量，你可以直接从程序中省略它。如果你的实现不支持 `fixed` 和 `right` 操纵符，可以使用 `cout.setf(ios_base::fixed, ios_base::floatfield)` 和 `cout.setf(ios_base::right, ios_base::adjustfield)`。此外，你可能需要用 `ios` 替换 `ios_base`。其他编译器，尤其是较旧的编译器，可能还有其他特性。

## 程序清单 17.19 binary.cpp

```cpp
// binary.cpp -- binary file I/O
#include <iostream> // not required by most systems
#include <fstream>
#include <iomanip>
#include <cstdlib> // for exit()

inline void eatline() { while (std::cin.get() != '\n') continue; }
struct planet
{
    char name[20];       // name of planet
    double population;   // its population
    double g;            // its acceleration of gravity
};

const char * file = "planets.dat";

int main()
{
    using namespace std;
    planet pl;
    cout << fixed << right;

// show initial contents
    ifstream fin;
    fin.open(file, ios_base::in | ios_base::binary);  // binary file
    //NOTE: some systems don't accept the ios_base::binary mode
    if (fin.is_open())
    {
        cout << "Here are the current contents of the "
             << file << " file:\n";
        while (fin.read((char *) &pl, sizeof pl))
        {
            cout << setw(20) << pl.name << ": "
                 << setprecision(0) << setw(12) << pl.population
                 << setprecision(2) << setw(6) << pl.g << endl;
        }
        fin.close();
    }

// add new data
    ofstream fout(file,
                  ios_base::out | ios_base::app | ios_base::binary);
    //NOTE: some systems don't accept the ios::binary mode
    if (!fout.is_open())
    {
```
