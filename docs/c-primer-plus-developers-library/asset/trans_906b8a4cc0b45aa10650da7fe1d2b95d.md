
第一条语句将 int 值 65 转换为 char 值，然后显示以 65 作为其 ASCII 码的字符。类似地，第二条语句将 double 类型的值 66.3 转换为 char 类型的值 66，并显示相应的字符。

这种行为在 C++ 2.0 版之前的版本中很方便；在这些版本中，语言用 int 类型值表示字符常量。因此，像下面这样的语句会将 'W' 解释为 int 值，从而将其显示为整数 87，即该字符的 ASCII 值：

```cpp
cout << 'W';
```

但下面的语句可以正常工作：

```cpp
cout.put('W');
```

由于当前的 C++ 将 char 常量表示为 char 类型，所以现在两种方法都可以使用。

有些编译器错误地为三种参数类型重载 put()：char、unsigned char 和 signed char。这会使以 int 参数使用 put() 产生歧义，因为 int 可以转换为这三种类型中的任意一种。

write() 方法写入整个字符串，并具有以下模板原型：

```cpp
basic_ostream<charT,traits>& write(const char_type* s, streamsize n);
```

write() 的第一个参数提供要显示的字符串的地址，第二个参数指明要显示多少个字符。使用 cout 调用 write() 会调用 char 特化，因此返回类型为 ostream &。程序清单 17.1 展示了 write() 方法如何工作。

### 程序清单 17.1 write.cpp

```cpp
// write.cpp -- using cout.write()
#include <iostream>
#include <cstring> // or else string.h

int main()
{
    using std::cout;
    using std::endl;
    const char * state1 = "Florida";
    const char * state2 = "Kansas";
    const char * state3 = "Euphoria";
    int len = std::strlen(state2);
    cout << "Increasing loop index:\n";
    int i;
    for (i = 1; i <= len; i++)
    {
        cout.write(state2,i);
        cout << endl;
    }

    // concatenate output
    cout << "Decreasing loop index:\n";
    for (i = len; i > 0; i--)
        cout.write(state2,i) << endl;

    // exceed string length
    cout << "Exceeding string length:\n";
    cout.write(state2, len + 5) << endl;

    return 0;
}
```

有些编译器可能会注意到，该程序定义了数组 `state1` 和 `state3`，但没有使用它们。这没关系，因为这两个数组只是为了在 `state2` 数组前后提供数据，以便你看到程序错误计算对 `state2` 的访问时会发生什么。下面是程序清单 17.1 中程序的输出：

```text
Increasing loop index:
K
Ka
Kan
Kans
Kansa
Kansas
Decreasing loop index:
Kansas
Kansa
Kans
Kan
Ka
K
Exceeding string length:
Kansas Euph
```

注意，`cout.write()` 调用返回 `cout` 对象。这是因为 `write()` 方法返回调用它的对象的引用，而在本例中，是 `cout` 对象调用它。这使得连接输出成为可能，因为 `cout.write()` 被其返回值 `cout` 替换：

```cpp
cout.write(state2,i) << endl;
```

另外，注意 `write()` 方法在到达空字符时不会自动停止打印字符。它只是打印你告诉它要打印的字符数，即使这超出了某个特定字符串的边界！在本例中，程序用两个其他字符串把字符串 "Kansas" 夹在中间，以便相邻内存位置会包含数据。编译器在内存中存储数据的顺序以及对齐内存的方式上有所不同。例如，"Kansas" 占用 6 字节，但这个特定编译器似乎通过使用 4 字节的倍数来对齐字符串，因此 "Kansas" 被填充到 8 字节。有些编译器将 "Florida" 存储在 "Kansas" 之后。因此，由于编译器的差异，输出的最后一行可能会得到不同的结果。

write() 方法也可以用于数值数据。你会向它传递一个数字的地址，并类型转换为 char *：

```cpp
long val = 560031841;
cout.write( (char *) &val, sizeof (long));
```

这不会把数字转换为正确的字符；相反，它传输的是内存中存储的位表示。例如，像 560031841 这样的 4 字节 long 值会作为 4 个独立字节传输。然后，像显示器这样的输出设备会尝试把每个字节解释为 ASCII（或其他）码。因此，560031841 会在屏幕上显示为某种 4 字符组合，很可能是乱码。（但也许不是；试一试看看。）然而，write() 确实提供了一种紧凑、准确的方式将数值数据存储到文件中。本章后面我们会回到这种可能性。

## 刷新输出缓冲区

考虑一下程序使用 cout 将字节发送到标准输出时会发生什么。由于 ostream 类对由 cout 对象处理的输出进行缓冲，输出不会立即发送到其目的地。相反，它会累积在缓冲区中，直到缓冲区满。然后程序刷新缓冲区，将内容发送出去，并清空缓冲区以接收新数据。通常，缓冲区是 512 字节或其整数倍。当标准输出连接到硬盘上的文件时，缓冲是一种很好的省时手段。毕竟，你不会希望程序为了发送 512 字节而访问硬盘 512 次。在缓冲区中收集 512 字节，并在一次磁盘操作中把它们写入硬盘，要高效得多。

然而，对于屏幕输出，先填满缓冲区就没那么重要。实际上，如果你必须改写消息“按任意键继续”，使其消耗所需的 512 字节来填满缓冲区，那会很不方便。幸运的是，在屏幕输出的情况下，程序不一定非要等到缓冲区满。例如，向缓冲区发送换行符通常会刷新缓冲区。此外，如前所述，大多数 C++ 实现会在有输入等待时刷新缓冲区。也就是说，假设你有以下代码：

```cpp
cout << "Enter a number: ";
float num;
cin >> num;
```

程序等待输入这一事实会促使它立即显示 cout 消息（也就是刷新“请输入一个数字：”消息），即使输出字符串缺少换行符。如果没有此特性，程序会等待输入，而不会用 cout 消息提示用户。

如果你的实现没有在你希望的时候刷新输出，你可以使用两种操纵符之一来强制刷新。flush 操纵符刷新缓冲区，endl 操纵符刷新缓冲区并插入一个换行符。你可以像使用变量名一样使用这些操纵符：

```cpp
cout << "Hello, good-looking! " << flush;
cout << "Wait just a moment, please." << endl;
```

事实上，操纵符是函数。例如，你可以直接调用 `flush()` 函数来刷新 cout 缓冲区：

```cpp
flush(cout);
```

然而，ostream 类以这样一种方式重载了 `<<` 插入运算符：下面的表达式会被替换为 `flush(cout)` 函数调用：

```cpp
cout << flush
```

因此，你可以使用更方便的插入表示法成功刷新。

## 使用 cout 格式化

ostream 插入运算符将值转换为文本形式。默认情况下，它们按如下方式格式化值：

- char 类型的值如果表示可打印字符，就在一个字符宽的字段中显示为该字符。
- 数值整数类型显示为十进制整数，字段宽度刚好足以容纳该数字以及可能存在的负号。
- 字符串显示在宽度等于字符串长度的字段中。

浮点类型的默认行为已经改变。以下是早期和当前 C++ 实现之间的差异：

- **新式**——浮点类型总共显示六位数字，但不显示末尾零。（注意，显示的数字位数与数字存储的精度无关。）数字按定点记数法或 E 记数法（见第 3 章“处理数据”）显示，具体取决于数字的值。特别地，如果指数为 6 或更大，或为 −5 或更小，则使用 E 记数法。同样，字段宽度刚好足以容纳该数字以及可能存在的负号。默认行为对应于使用标准 C 库函数 `printf()` 并带有 `%g` 说明符。
- **旧式**——浮点类型在小数点右边显示六位，但不显示末尾零。（注意，显示的数字位数与数字存储的精度无关。）数字按定点记数法或 E 记数法（见第 3 章）显示，具体取决于数字的值。同样，字段宽度刚好足以容纳该数字以及可能存在的负号。

因为每个值都显示在与其大小相等的字段中，所以必须显式地在值之间提供空格；否则，连续的值会连在一起。
