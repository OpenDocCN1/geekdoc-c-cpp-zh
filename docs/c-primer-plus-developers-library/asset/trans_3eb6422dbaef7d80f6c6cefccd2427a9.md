
下面是程序清单 17.20 中程序的一次示例运行，它基于一个 planets.dat 文件，该文件自你上次看到以来又添加了几个条目：

```text
Here are the current contents of the planets.dat file:
0:          Earth: 6928198253 9.81
1:          Jenny's World: 32155648 8.93
2:          Tranter: 8900000000 15.03
3:          Trellan: 5214000 9.62
4:          Preestone: 3945851000 8.68
5:          Taanagoot: 361000004 10.23
6:          Marin: 252409 9.79
Enter the record number you wish to change: 2
Your selection:
        Tranter: 8900000000 15.03
Enter planet name: Tranter
Enter planetary population: 89521844777
Enter planet's acceleration of gravity: 10.53
Here are the new contents of the planets.dat file:
0:          Earth: 6928198253 9.81
1:          Jenny's World: 32155648 8.93
2:          Tranter: 89521844777 10.53
3:          Trellan: 5214000 9.62
4:          Preestone: 3945851000 8.68
5:          Taanagoot: 361000004 10.23
6:          Marin: 252409 9.79
Done.
```

通过使用本程序中的技术，你可以扩展它，使其允许添加新资料和删除记录。如果要扩展该程序，最好使用类和函数重新组织它。例如，你可以将 planet 结构体转换为类定义；然后可以重载 << 插入运算符，使 cout << pl 按示例中的格式显示类的数据成员。此外，该示例没有费心验证输入，因此你可以添加代码，在适当的地方检查数值输入。

## 使用临时文件

开发应用程序时经常需要使用临时文件，这些文件的生命周期短暂，必须由程序控制。你是否想过在 C++ 中如何做到这一点？创建临时文件、复制另一个文件的内容并删除该文件其实非常简单。首先，你需要为临时文件想出一个命名方案。但是等等……如何确保每个文件都被分配唯一的名称？在 cstdio 中声明的 tmpnam() 标准函数（你已经学过了）：

```cpp
char* tmpnam( char* pszName );
```

tmpnam() 函数创建一个临时名称，并将其放入 pszName 所指向的 C 风格字符串中。常量 L_tmpnam 和 TMP_MAX（二者都定义在 cstdio 中）限制文件名的字符数，以及 tmpnam() 在不于当前目录中生成重复文件名的情况下可被调用的最大次数。下面的示例生成 10 个临时名称：

```cpp
#include <cstdio>
#include <iostream>

int main()
{
    using namespace std;
    cout << "This system can generate up to " << TMP_MAX
         << " temporary names of up to " << L_tmpnam
         << " characters.\n";
    char pszName[ L_tmpnam ] = {'\0'};
    cout << "Here are ten names:\n";
    for( int i=0; 10 > i; i++ )
    {
        tmpnam( pszName );
        cout << pszName << endl;
    }
    return 0;
}
```

更一般地说，通过使用 `tmpnam()`，你现在可以生成 TMP_MAX 个唯一文件名，每个名称最多包含 `L_tmpnam` 个字符。名称本身取决于编译器。你可以运行这个程序，看看你的编译器会生成什么名称。

## 内存内格式化

iostream 家族支持程序与终端之间的 I/O。fstream 家族使用相同的接口提供程序与文件之间的 I/O。C++ 库还提供了 sstream 家族，它使用相同的接口提供程序与 string 对象之间的 I/O。也就是说，你可以使用与 cout 搭配使用过的相同 ostream 方法，将格式化信息写入 string 对象，也可以使用诸如 getline() 之类的 istream 方法从 string 对象读取信息。从 string 对象读取格式化信息或将格式化信息写入 string 对象的过程称为内存内格式化。让我们简要看看这些设施。（sstream 字符串支持家族取代了 strstream.h 字符数组支持家族。）

sstream 头文件定义了一个 ostringstream 类，它派生自 ostream 类。（还有一个基于 wostream 的 wostringstream 类，用于宽字符集。）如果创建一个 ostringstream 对象，就可以向其中写入信息，它会存储这些信息。你可以对 ostringstream 对象使用与 cout 相同的方法。也就是说，你可以像下面这样做：

```cpp
ostringstream outstr;
double price = 380.0;
char * ps = " for a copy of the ISO/IEC C++ standard!";
outstr.precision(2);
outstr << fixed;
outstr << "Pay only CHF " << price << ps << endl;
```

格式化后的文本进入缓冲区，该对象使用动态内存分配按需扩大缓冲区大小。ostringstream 类有一个名为 str() 的成员函数，它返回一个初始化为缓冲区内容的 string 对象：

```cpp
string msg = outstr.str();    // returns string with formatted information
```

使用 str() 方法会“冻结”该对象，你不能再向它写入内容。程序清单 17.21 提供了一个内存内格式化的简短示例。

### 程序清单 17.21 strout.cpp

```cpp
// strout.cpp -- incore formatting (output)
#include <iostream>
#include <sstream>
#include <string>
int main()
{
    using namespace std;
    ostringstream outstr;      // manages a string stream

    string hdisk;
    cout << "What's the name of your hard disk? ";
    getline(cin, hdisk);
    int cap;
    cout << "What's its capacity in GB? ";
    cin >> cap;
    // write formatted information to string stream
    outstr << "The hard disk " << hdisk << " has a capacity of "
           << cap << " gigabytes.\n";
    string result = outstr.str();   // save result
    cout << result;                 // show contents

    return 0;
}
```

下面是程序清单 17.21 中程序的一次示例运行：

```text
What's the name of your hard disk? Datarapture
What's its capacity in GB? 2000
The hard disk Datarapture has a capacity of 2000 gigabytes.
```

istringstream 类允许你使用 istream 家族的方法，从 istringstream 对象读取数据，而该对象可以由 string 对象初始化。

假设 `facts` 是一个 string 对象。要创建一个与此字符串关联的 `istringstream` 对象，可以使用以下代码：

```cpp
istringstream instr(facts);    // use facts to initialize stream
```

然后使用 istream 方法从 `instr` 读取数据。例如，如果 `instr` 包含一组字符格式的整数，可以按如下方式读取它们：

```cpp
int n;
int sum = 0;
while (instr >> n)
    sum += n;
```

程序清单 17.22 使用重载的 `>>` 运算符，一次一个单词地读取 string 的内容。

### 程序清单 17.22 strin.cpp

```cpp
// strin.cpp -- formatted reading from a char array
#include <iostream>
#include <sstream>
#include <string>
int main()
{
    using namespace std;
    string lit = "It was a dark and stormy day, and"
                 " the full moon glowed brilliantly. ";
    istringstream instr(lit);   // use lit for input
    string word;
    while (instr >> word)       // read a word at a time
        cout << word << endl;
    return 0;
}
```

下面是程序清单 17.22 中程序的输出：

```text
It
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

*简而言之，iostream 和 ostringstream 类使你能够利用 istream 和 ostream 类方法的能力，来管理存储在字符串中的字符数据。*

## 总结

流是字节流入或流出程序的流动。缓冲区是内存中的临时存放区，充当程序与文件或其他 I/O 设备之间的中介。信息可以在缓冲区与文件之间传输，使用诸如磁盘驱动器之类的设备能够最有效处理的大块数据。信息也可以以逐字节的流动在缓冲区与程序之间传输，这种流动通常对程序中的处理更方便。C++ 通过将有缓冲的流连接到程序及其输入源来处理输入。类似地，C++ 通过将有缓冲的流连接到程序及其输出目标来处理输出。iostream 和 fstream 类构成了一个 I/O 类库，它定义了一组丰富的类来管理流。包含 iostream 文件的 C++ 程序会自动打开八个流，并用八个对象管理它们。cin 对象管理标准输入流，默认情况下它连接到标准输入设备，通常是键盘。cout 对象管理标准输出流，默认情况下它连接到标准输出设备，通常是显示器。cerr 和 clog 对象管理连接到标准错误设备的无缓冲流和有缓冲流，标准错误设备通常是显示器。这四个对象有四个宽字符对应对象，名为 wcin、wcout、wcerr 和 wclog。

I/O 类库提供了各种有用的方法。stream 类定义了提取运算符（>>）的多个版本，它们能识别所有基本 C++ 类型，并将字符输入转换为这些类型。get() 方法家族和 getline() 方法为单字符输入和字符串输入提供进一步支持。类似地，ostream 类定义了插入运算符（<<）的多个版本，它们能识别所有基本 C++ 类型，并将其转换为合适的字符输出。put() 方法为单字符输出提供进一步支持。wistream 和 wostream 类为宽字符提供类似支持。

你可以通过使用 ios_base 类方法，以及使用定义在 iostream 和 iomanip 文件中的操纵符（可与插入运算符连接使用的函数），来控制程序格式化输出的方式。这些方法和操纵符让你能够控制数制、字段宽度、显示的小数位数、用于显示浮点值的系统以及其他元素。

fstream 文件提供了类定义，将 iostream 方法扩展到文件 I/O。ifstream 类派生自 istream 类。通过将 ifstream 对象与文件关联，你可以使用所有 istream 方法来读取该文件。类似地，将 ofstream 对象与文件关联，让你可以使用 ostream 方法写入文件。而将 fstream 对象与文件关联，让你可以对该文件同时使用输入和输出方法。

要将文件与流关联，你可以在初始化文件流对象时提供文件名，也可以先创建文件流对象，然后使用 open() 方法将该流与文件关联。close() 方法终止连接。
