
也就是说，*end* 指向最后一个要使用的值之后的位置。考虑下面的语句：

```cpp
string six(alls + 6, alls + 10);    // ctor #6
```

因为数组名是指针，所以 `alls + 6` 和 `alls + 10` 都是 `char *` 类型，因此使用该模板时其 `iter` 被替换为 `char *` 类型。第一个参数指向 `alls` 数组中的第一个 `w`，第二个参数指向第一个 `well` 后面的空格。因此，`six` 被初始化为字符串 `"well"`。图16.1 展示了该构造函数如何工作。

```cpp
char alls[] = "All's well that ends well";
string six(alls + 6, alls + 10);
range = [alls + 6, alls + 10);
```

![](img/9afc44517b591d64e2e19f623c9308ef_970_0.png)

图16.1 使用范围的 string 构造函数。

现在假设你想用这个构造函数将一个对象初始化为另一个 string 对象的一部分——比如对象 `five`。下面的做法行不通：

```cpp
string seven(five + 6, five + 10);
```

原因在于，对象名与数组名不同，不会被当作对象的地址；因此 `five` 不是指针，`five + 6` 没有意义。不过，`five[6]` 是一个 `char` 值，所以 `&five[6]` 是一个地址，可以作为构造函数的参数：

```cpp
string seven(&five[6], &five[10]); // ctor #6 again
```

第七个构造函数将一个 string 对象的一部分复制到所构造的对象中：

```cpp
string eight(four, 7, 16);       // ctor #7
```

这条语句从 `four` 中位置 7（第 8 个字符）开始，将 16 个字符复制到 `eight`。

## C++11 构造函数

`string(string && str) noexcept` 构造函数与复制构造函数相似，因为新 string 是 `str` 的副本。然而，与复制构造函数不同，它不保证 `str` 会被当作 `const` 处理。这种形式的构造函数称为*移动构造函数*。编译器可以在某些情况下用它代替复制构造函数来优化性能。第18章“使用新的C++标准”在“移动语义与右值引用”一节中讨论了这一主题。

`string(initializer_list<char> il)` 构造函数为 `string` 类启用了列表初始化。也就是说，它使下面这样的声明成为可能：

```cpp
string piano_man = {'L', 'i', 's', 'z', 't'};
string comp_lang {'L', 'i', 's', 'p'};
```

这对 string 类可能没有那么有用，因为使用 C 风格字符串更容易，但它确实满足了使列表初始化语法通用的意图。本章稍后将进一步讨论 `initializer_list` 模板。

## string 类的输入

关于一个类，另一件需要了解的有用事情是它有哪些可用的输入选项。回想一下，对于 C 风格字符串，有三种选择：

```cpp
char info[100];
cin >> info;             // read a word
cin.getline(info, 100);  // read a line, discard \n
cin.get(info, 100);      // read a line, leave \n in queue
```

回想一下，对于 string 对象，有两种选择：

```cpp
string stuff;
cin >> stuff;             // read a word
getline(cin, stuff);      // read a line, discard \n
```

两个版本的 `getline()` 都允许一个可选参数，用于指定使用哪个字符来分隔输入：

```cpp
cin.getline(info, 100, ':');   // read up to :, discard :
getline(cin, stuff, ':');      // read up to :, discard :
```

主要的操作差异在于，string 版本会自动调整目标 string 对象的大小以容纳输入字符：

```cpp
char fname[10];
string lname;
cin >> fname;             // could be a problem if input size > 9 characters
cin >> lname;             // can read a very, very long word
cin.getline(fname, 10);   // may truncate input
getline(cin, lname);      // no truncation
```

自动调整大小的特性使 string 版本的 `getline()` 无需使用限制读取输入字符数的数值参数。

一个设计上的差异是，C 风格字符串输入设施是 `istream` 类的方法，而 string 版本是独立函数。这就是为什么对于 C 风格字符串输入，`cin` 是调用对象，而对于 string 对象输入，`cin` 是函数参数。这也适用于 `>>` 形式，如果把代码写成函数形式就很明显：

```cpp
cin.operator>>(fname);    // istream class method
operator>>(cin, lname);   // regular function
```

让我们更仔细地检查 string 输入函数。如前所述，两者都会调整目标 string 的大小以适合输入。但存在限制。第一个限制因素是 string 允许的最大大小，由常量 `string::npos` 表示。这通常是 unsigned int 的最大值，因此对普通的交互式输入并不构成实际限制。不过，如果你试图将整个文件的内容读入单个 string 对象，它可能成为一个因素。第二个限制因素是程序可用的内存量。

string 类的 `getline()` 函数从输入中读取字符并将它们存储到 string 对象中，直到发生以下三种情况之一：

- 遇到文件结尾，此时输入流的 `eofbit` 被设置，这意味着 `fail()` 和 `eof()` 方法都将返回 true。
- 遇到分隔字符（默认是 `\n`），此时该字符会从输入流中移除，但不会被存储。
- 读取到最大可能字符数（`string::npos` 与可用于分配的内存字节数中的较小者），此时输入流的 `failbit` 被设置，这意味着 `fail()` 方法将返回 true。

（输入流对象有一个记录系统来跟踪流的错误状态。在该系统中，设置 `eofbit` 表示检测到文件结尾；设置 `failbit` 表示检测到输入错误；设置 `badbit` 表示发生了某种无法识别的失败，例如硬件故障；设置 `goodbit` 表示一切正常。第17章“输入、输出和文件”将进一步讨论这一点。）

string 类的 `operator>>()` 函数行为类似，区别在于它不是读取到分隔字符并将其丢弃，而是读取到空白字符为止，并将该字符留在输入队列中。空白字符是空格、换行符或制表符，或者更一般地说，是任何使 `isspace()` 返回 true 的字符。

到目前为止，在本书中你已经见过几个控制台字符串输入的例子。由于 string 对象的输入函数可与流一起工作并能识别文件结尾，你也可以将它们用于文件输入。程序清单16.2 展示了一个从文件中读取字符串的简短示例。它假设文件包含用冒号字符分隔的字符串，并使用 `getline()` 方法指定分隔符。然后它对字符串编号并显示它们，每个字符串输出到一行。

## 程序清单 16.2 `strfile.cpp`

```cpp
// strfile.cpp -- read strings from a file
#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>

int main()
{
    using namespace std;
    ifstream fin;
    fin.open("tobuy.txt");
    if (fin.is_open() == false)
    {
        cerr << "Can't open file. Bye.\n";
        exit(EXIT_FAILURE);
    }
    string item;
    int count = 0;
    getline(fin, item, ',');
    while (fin)  // while input is good
    {
        ++count;
        cout << count << ": " << item << endl;
        getline(fin, item, ',');
    }
    cout << "Done\n";
    fin.close();
    return 0;
}
```

下面是一个示例 `tobuy.txt` 文件：

```text
sardines:chocolate ice cream:pop corn:leeks:
cottage cheese:olive oil:butter:tofu:
```

通常，为了让程序找到该文本文件，文本文件应位于可执行程序所在的目录中，有时也应位于项目文件所在的目录中。或者你可以提供完整路径名。在 Windows 系统上，请记住，在 C 风格字符串中，转义序列 `\\` 表示单个反斜杠：

```cpp
fin.open("C:\\CPP\\Progs\\tobuy.txt"); // file = C:\CPP\Progs\tobuy.txt
```

下面是程序清单16.2 中程序的输出：

```text
1: sardines
2: chocolate ice cream
3: pop corn
4: leeks
5: cottage cheese
6: olive oil
7: butter
8: tofu
9: Done
```

