
## 分隔路径名

每个人都想与众不同、独一无二。

编写 Microsoft 的 MS-DOS 操作系统的人，没有遵循使用 Unix 的 / 作为路径名分隔符的传统，而是决定使用 \ 字符，从而使“反斜杠”一词进入数百万人的词汇。所以今天，在 Windows 上，你会看到这样的路径名：`C:\MyDataFolder\MyMessyPath\DifficultToType\LetterToEditor.doc`。但在 Unix 上，你会看到正斜杠，如 `/usr/something/letterToEditor.doc`。如果这个差异还不够糟糕，想想反斜杠在 C++ 字符串中的含义。它表示后面跟着一个字母，编译器会把这两个字符一起解释为其他东西。例如，`\t` 表示制表符，`\n` 表示换行符。那么如何把反斜杠放入字符串呢？你要放两个反斜杠。唉！这意味着，如果你在 C++ 应用程序中使用前面那种 MS-DOS 风格的字符串（里面带有 Windows 的那个，比尔·盖茨先生！），它必须看起来像这样：

`C:\\MyDataFolder\\MyMessyPath\\DifficultToType\\LetterToEditor.doc`

是的，如果你想让编译器得到正确的字符串，就必须把每个反斜杠输入两次。但与其这样做，我们想提出一个更好的解决方案！完全不要使用反斜杠，即使你是在为 Windows（或者，我们猜，MS-DOS）编程。是的，没错！停止印刷！打电话给电台脱口秀节目！向全世界宣布！当你在 Windows 上编写 C++ 应用程序时，库足够智能，知道正斜杠可以代替反斜杠！因此你可以使用这个字符串：

`C:/MyDataFolder/MyMessyPath/DifficultToType/LetterToEditor.doc`

在本书中，你会看到我们使用正斜杠路径。这样，我们的示例在 Unix 和 Windows 上都能工作。

清单1-1中的 FileOutput01 示例代码展示了如何打开一个全新文件、向其中写入一些信息，然后关闭它。（但是等等，还有更多：无论你使用的是较新的符合 ANSI 的编译器还是较旧的编译器，这个版本都能工作！）

### 清单1-1：使用打开文件并向其中写入的代码

```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    ofstream outfile("../MyFile.txt");
    outfile << "Hi" << endl;
    outfile.close();

    return 0;
}
```

### 查找你的文件

每当你打开一个新文件时，都必须知道文件在哪里，而不仅仅是文件叫什么。换句话说，你需要同时提供路径和文件名，而不只是文件名。你可以根据应用程序的不同，用不同方式获取文件路径。例如，你可能把所有文件都保存在某个特定目录中；那么你就要在文件名前加上该目录（即路径）名。string 类让这变得很容易，如下代码所示：

```cpp
const string MyPath = "c:\\GreatSoftware";
string Filename = MyPath + "\\" + "MyFile.txt";
ofstream outfile(Filename.c_str());
```

我们之所以必须对 string 调用 `c_str`，是因为 `ofstream` 类没有接受 string 实例的构造函数，只有接受 C 风格字符串的构造函数。`c_str` 函数返回一个指针，指向与该 string 等价的 C 风格字符串。另外，使用 `string` 类时记得添加 `#include <string>`！还有，当你像本例中这样使用常量路径时，也可以改为把路径名存储在你用户计算机某处的某个初始化文件中，而不是像本例中这样在应用程序中*硬编码*它。你还可以加入一个选项窗口，让用户更改这个路径的值。

清单1-1中的简短应用程序打开一个名为 `MyFile.txt` 的文件。（文件路径中的“`../`”部分会把文件放到示例的父目录中，也就是 Chapter01 文件夹——详情参见“查找你的文件”侧栏。）它通过创建 `ofstream` 的新实例来完成这一点，`ofstream` 是用于向文件写入的类。下一行代码把字符串 `"Hi"` 写入文件。它使用插入运算符 `<<`，就像 `cout` 那样。事实上，`ofstream` 正是派生自 `cout` 作为实例的那个类，所以这意味着你能对 `cout` 做的所有事情，也都能对你的文件做！哇！我们知道我们很兴奋！

写完文件后，我们通过调用 `close` 成员函数来关闭它。这很重要！

如果你想打开一个已有文件并向其追加内容，可以稍微修改清单1-1。你只需如下更改传递给构造函数的参数：

```cpp
ofstream outfile("../MyFile.txt", ios_base::app);
```

`ios::app` 项是名为 `ios` 的类中的枚举，而 `ios_base::app` 项是名为 `ios_base` 的类中的枚举。

`ios` 类是 `ofstream` 类派生自的基类。`ios` 类也是 `ifstream` 的基类，`ifstream` 用于读取文件。

第 V 卷  
第 1 章  
使用流库归档信息

对于较新的编译器，`ios_base` 类是 `ostream` 和 `ifstream` 的基类。（中间还有几个类。`ofstream` 是一个模板类，派生自名为 `basic_ofstream` 的模板类，后者派生自名为 `basic_ios` 的模板类，后者又派生自 `ios_base` 类。你可以在 `http://www.cplusplus.com/reference/iostream/` 查看这些类的简化图。）

你也可以从已有文件读取。这就像 `cin` 对象一样工作。清单1-2中所示的 FileRead01 示例打开清单1-1创建的文件，并把字符串读回来。这个示例再次使用父目录作为创建、更新和读取文件的常见位置。

### 清单1-2：使用代码打开文件并从中读取

```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

int main()
{
    string word;
    ifstream infile("../MyFile.txt");
    infile >> word;
    cout << word << endl;
    infile.close();

    return 0;
}
```

运行此应用程序时，之前在第1-1号清单中写入文件的字符串——“Hi,”——会出现在屏幕上。成功了！它从文件中读入了该字符串！

## 打开文件时处理错误

打开文件时，各种事情都可能出错。文件存在于物理设备上——例如固定磁盘，或者可能在闪存盘或 SD 卡上——而在使用物理设备时，你可能会遇到问题。例如，磁盘的一部分可能损坏，导致现有文件损坏。或者，没那么严重，你可能用完磁盘空间。或者，更没那么严重，你可能尝试打开某个不存在目录中的文件。

![](img/6ba99460b0feb3585671a4612ff5fabb_642_0.png)

如果你尝试通过指定完整路径和文件名来打开文件进行写入，但目录不存在，计算机的响应会有所不同，具体取决于你使用的操作系统。如果你不确定自己的操作系统会如何响应，可以尝试编写一个简单的测试应用程序，尝试创建并打开类似 /abc/def/ghi/jkl/abc.txt 的东西。（当然，你要确保使用一个不存在的目录；我们假设你的硬盘上不存在 /abc/def/ghi/jkl。）然后会发生两种情况之一：要么目录和文件会被创建，要么什么也不会发生。

例如，在 Windows 系统上，如果我们尝试在不存在的目录中创建文件，系统不会创建该目录。这是因为在底层，应用程序最终会调用一个操作系统函数来执行创建文件的脏活。而这个特定的操作系统函数（如果你在乎的话，它叫 CreateFile()）有一条规则：它不会为你创建目录。

如果你想判断 ofstream 类是否无法创建文件，可以调用它的 fail() 成员函数。如果对象无法创建文件，该函数会返回 true。目录不存在时就会发生这种情况。清单1-3中所示的 DirectoryCheck01 示例演示了这一点。

### 清单1-3：当 ofstream 无法创建文件时返回 true

```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    ofstream outfile("/abc/def/ghi/MyFile.txt");
    if (outfile.fail()) {
        cout << "Couldn't open the file!" << endl;
        return 0;
    }
    outfile << "Hi" << endl;
    outfile.close();

    return 0;
}
```

运行这段代码时，假设你的系统上没有名为 /abc/def/ghi 的目录，你应该会看到消息 Couldn't open the file! 我们还假设你的操作系统在这种情况下不会创建目录；如果它会创建，那么你的计算机会打开文件，向其中写入 Hi，并在收尾关闭后继续过它的快乐生活。
