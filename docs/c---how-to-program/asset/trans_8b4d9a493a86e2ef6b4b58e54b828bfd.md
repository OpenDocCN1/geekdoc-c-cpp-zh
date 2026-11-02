
## 良好的编程实践 21.1

显示布尔值时使用 true 或 false，而不是非零或 0，分别表示，能使程序输出更清晰。

```cpp
// Fig. 21.20: fig21_20.cpp
// Stream manipulators boolalpha and noboolalpha.
#include <iostream>
using namespace std;

int main()
{
    bool booleanValue = true;

    // display default true booleanValue
    cout << "booleanValue is " << booleanValue << endl;

    // display booleanValue after using boolalpha
    cout << "booleanValue (after using boolalpha) is "
         << boolalpha << booleanValue << endl << endl;

    cout << "switch booleanValue and use noboolalpha" << endl;
    booleanValue = false; // change booleanValue
    cout << noboolalpha << endl; // use noboolalpha

    // display default false booleanValue after using noboolalpha
    cout << "booleanValue is " << booleanValue << endl;

    // display booleanValue after using boolalpha again
    cout << "booleanValue (after using boolalpha) is "
         << boolalpha << booleanValue << endl;
} // end main
```

```text
booleanValue is 1
booleanValue (after using boolalpha) is true

switch booleanValue and use noboolalpha

booleanValue is 0
booleanValue (after using boolalpha) is false
```

**Fig. 21.20** | 流操纵符 boolalpha 和 noboolalpha.

## 21.7.8 通过成员函数 flags 设置和重置格式状态

在整个第 21.7 节中，我们一直使用流操纵符来更改输出格式特性。现在我们讨论在应用了多个操纵之后如何将输出流的格式恢复到其默认状态。无参数的成员函数 flags 将当前格式设置作为一个 fmtflags 数据类型（属于类 ios_base）返回，该类型表示格式状态。带有一个 fmtflags 参数的成员函数 flags 根据参数指定的方式设置格式状态，并返回先前的状态设置。flags 返回的值的初始设置在不同系统之间可能有所不同。图 21.21 的程序使用成员函数 flags 保存流的原始格式状态（第 17 行），然后恢复原始格式设置（第 25 行）。

```cpp
// Fig. 21.21: fig21_21.cpp
// flags member function.
#include <iostream>
using namespace std;
int main()
{
    int integerValue = 1000;
    double doubleValue = 0.0947628;

    // display flags value, int and double values (original format)
    cout << "The value of the flags variable is: " << cout.flags()
         << "\nPrint int and double in original format:\n";
    cout << integerValue << '\t' << doubleValue << endl;

    // use cout flags function to save original format
    ios_base::fmtflags originalFormat = cout.flags();
    cout << showbase << oct << scientific; // change format

    // display flags value, int and double values (new format)
    cout << "The value of the flags variable is: " << cout.flags()
         << "\nPrint int and double in a new format:\n";
    cout << integerValue << '\t' << doubleValue << endl;

    cout.flags( originalFormat ); // restore format

    // display flags value, int and double values (original format)
    cout << "The restored value of the flags variable is: "
         << cout.flags()
         << "\nPrint values in original format again:\n";
    cout << integerValue << '\t' << doubleValue << endl;
} // end main
```

```text
The value of the flags variable is: 513
Print int and double in original format:
1000 0.0947628
The value of the flags variable is: 012011
Print int and double in a new format:
01750 9.47628e-002
The restored value of the flags variable is: 513
Print values in original format again:
1000 0.0947628
```

**Fig. 21.21** | flags 成员函数.

## 21.8 流错误状态

流的状态可以通过类 ios_base 中的位来测试。在本书前面，我们指出例如可以测试输入是否成功。图 21.22 显示了如何测试这些状态位。在工业级代码中，您希望对 I/O 操作执行类似的测试。

```cpp
// Fig. 21.22: fig21_22.cpp
// Testing error states.
#include <iostream>
using namespace std;

int main()
{
   int integerValue;

   // display results of cin functions
   cout << "Before a bad input operation:"
        << "\n   cin.rdstate(): " << cin.rdstate()
        << "\n      cin.eof(): " << cin.eof()
        << "\n     cin.fail(): " << cin.fail()
        << "\n      cin.bad(): " << cin.bad()
        << "\n     cin.good(): " << cin.good()
        << "\n\nExpects an integer, but enter a character: ";

   cin >> integerValue; // enter character value
   cout << endl;

   // display results of cin functions after bad input
   cout << "After a bad input operation:"
        << "\n   cin.rdstate(): " << cin.rdstate()
        << "\n      cin.eof(): " << cin.eof()
        << "\n     cin.fail(): " << cin.fail()
        << "\n      cin.bad(): " << cin.bad()
        << "\n     cin.good(): " << cin.good() << endl << endl;

   cin.clear(); // clear stream

   // display results of cin functions after clearing cin
   cout << "After cin.clear()" << "\ncin.fail(): " << cin.fail()
        << "\ncin.good(): " << cin.good() << endl;
} // end main
```

```text
Before a bad input operation:
   cin.rdstate(): 0
      cin.eof(): 0
     cin.fail(): 0
      cin.bad(): 0
     cin.good(): 1

Expects an integer, but enter a character: A

After a bad input operation:
   cin.rdstate(): 2
      cin.eof(): 0
     cin.fail(): 1
      cin.bad(): 0
     cin.good(): 0

After cin.clear()
cin.fail(): 0
cin.good(): 1
```

**Fig. 21.22** | 测试错误状态.

`eofbit` 在遇到 *文件结束* 后为输入流设置。程序可以使用成员函数 `eof` 来确定在尝试从流中提取数据 *超出* 流末尾后是否已遇到文件结束。调用 `cin.eof()` 如果在 `cin` 上遇到文件结束则返回 `true`，否则返回 `false`。

`failbit` 当流上发生 *格式错误* 且未输入任何字符时为流设置（例如，当您尝试读取一个 *数字* 而用户输入一个 *字符串* 时）。当此类错误发生时，字符 *不会* 丢失。`fail` 成员函数报告流操作是否失败。通常可以从此类错误中恢复。

`badbit` 当发生导致 *数据丢失* 的错误时为流设置。`bad` 成员函数报告流操作是否 *失败*。通常，此类严重故障无法恢复。

`goodbit` 如果流的 `eofbit`、`failbit` 或 `badbit` 位 *无* 一个被设置，则为流设置。

`good` 成员函数如果 `bad`、`fail` 和 `eof` 函数 *全部* 返回 `false` 则返回 `true`。I/O 操作应仅在“good”流上执行。

`rdstate` 成员函数返回流的 *错误状态*。例如，调用 `cout.rdstate` 将返回流的状态，然后可以通过检查 `eofbit`、`badbit`、`failbit` 和 `goodbit` 的 `switch` 语句来测试该状态。测试流状态的 *首选* 方法是使用成员函数 `eof`、`bad`、`fail` 和 `good`——使用这些函数不需要您熟悉特定的状态位。

`clear` 成员函数用于将流的状态 *恢复* 为“good”，以便可以在该流上进行 I/O。`clear` 的默认参数是 `goodbit`，因此语句 `cin.clear();` 清除 `cin` 并为流设置 `goodbit`。语句 `cin.clear( ios::failbit )` 设置 `failbit`。当使用用户定义类型对 `cin` 执行输入并遇到问题时，您可能希望这样做。名称 `clear` 在这种情况下可能显得不合适，但它是正确的。

图 21.22 的程序演示了成员函数 `rdstate`、`eof`、`fail`、`bad`、`good` 和 `clear`。实际输出的值在不同编译器之间可能有所不同。

`basic_ios` 的 `operator!` 成员函数如果设置了 `badbit`、设置了 `failbit` 或 *两者都* 设置，则返回 `true`。`operator void *` 成员函数如果设置了 `badbit`、设置了 `failbit` 或两者都设置，则返回 `false` (0)。当在选择语句或重复语句的控制下测试 `true`/`false` 条件时，这些函数在文件处理中很有用。
