
```
cout << "Enter the name of the input file: ";
string inputFileName;
getline(cin, inputFileName);

inStream.open(inputFileName.data());

if (inStream.is_open()) break;

cerr << "\n***Unable to open " << inputFileName
     << "\nTry again (Y or N)? ";
cin >> response;
}
while (response != 'N' && response != 'n');
}
```

这个函数给用户提供了不止一次输入正确文件名的机会，也符合许多程序员采用的设计策略：*在可能的情况下从错误中恢复，在无法恢复时优雅退出。*

## 11.2.2.3 输入和输出运算符

C++ 的一个吸引人之处在于其一致性——使用同一批运算符来执行功能相似的任务。例如，从文件输入可以与从键盘输入一样使用 `>>`，并且两种情形下的行为相同：跳过前导空白字符；当遇到一个不属于所读取类型值的字符时停止读取；将字符串转换为数字；使用 `eof()` 检查输入是否结束；等等。

输出也有同样的一致性。一旦 `ofstream` 对象连接到文件，它就能像屏幕输出一样使用——可以用输出运算符 `<<` 和格式操纵符（如 `endl`、`showpoint`、`setprecision()` 和 `setw()`）来执行输出（参见第 7.3 节）。

## 11.2.2.4 关闭文件流

我们已经看到，通过 `open()` 函数或在声明中初始化文件流对象，可以建立程序与文件之间的连接。在某个时刻，必须断开这个文件流，以便文件本身可以被访问，并被操作系统命令使用——例如，将文件内容输出到打印机。由于文件流对象是一个变量，当执行离开其作用域时，它会像其他任何变量一样自动断开。特别是，在函数内声明的文件流会在执行离开该函数时（如果此前没有断开）被断开。

可以通过向其发送 `close()` 消息来显式断开文件流，其形式为：

```
stream_name.close();
```

其中 `stream_name` 是任意一种文件流的名称。例如，示例 11.1 程序中的语句

```
inStream.close();
```

切断了程序与输入文件之间的连接，`istream` 变量 `inStream` 变为未定义，因此在不重新连接到文件的情况下再尝试从中读取将是一个错误。

对于输出流，`close()` 消息的作用稍有不同。为了看到这种差异，请考虑示例 11.1 中的语句

```
outStream.close();
```

在程序与输出文件的连接被切断之前，`outStream` 中的任何内容都会先被复制到输出文件中。之后，连接断开，`ostream` 变量 `outStream` 变为未定义。举例说明，在示例 11.2 的第一次执行中，`outStream` 的内容

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_439_0.png)

会被写入输出文件 `out1.txt`，我们可以将其形象地表示如下：

```
Average pressure reading: 55.5
Minimum pressure reading: 11.1 on day 1
Maximum pressure reading: 99.9 on day 9
```

虽然文件流在到达其作用域末尾时会自动断开，但有时有必要提前断开它。例如，我们的程序可能向某个文件写入值，然后我们想打开该文件并从中读取。在这种情况下，必须先使用 `close()` 断开到该文件的输出流，然后才能重新打开它。不过，即使不是这种情况，当不再需要某个文件流时，用 `close()` 将其断开也被认为是良好的编程实践。

这一点在涉及许多不同文件的程序中尤其重要，因为操作系统可能会限制一个程序同时打开的文件数量。这意味着，如果程序试图打开超过允许数量的文件，操作系统将异常终止该程序。通过总是在程序使用完文件后使用 `close()` 消息切断程序与文件的连接，可以避免此问题。这样就能使与该程序关联的打开文件数不超过操作系统允许的上限。

## 11.2.2.5 文件流作为参数

本节前面给出了一个函数示例，该函数允许用户反复输入输入文件名，直到找到并打开该文件：

```
void getInputFile(ifstream & inStream)
{
    char response;
    do
    {
        cout << "Enter the name of the input file: ";
        string inputFileName;
        getline(cin, inputFileName);

        inStream.open(inputFileName.data());

        if (inStream.is_open()) break;

        cerr << "\n***Unable to open " << inputFileName
             << "\nTry again (Y or N)? ";
        cin >> response;
    }
    while (response != 'N' && response != 'n');
}
```

请注意，参数 `inStream` 的类型是 `ifstream`，并且是一个引用参数；这一点必须始终如此。与文件流实参对应的参数必须是引用参数，因为：

- 从 `ifstream` 对象读取会改变其读取位置；并且
- 写入 `ofstream` 对象会改变其写入位置。

如果文件流参数不是引用参数，这些变化就不会传回 `main()` 或其他调用此函数的函数。

## 11.2.3 小结

以下几点总结了 C++ 中文件 I/O 的一些要点。

- 文本文件将字符存储在辅助存储设备上。
- 程序对文件的输入或输出只能通过文件流间接完成——文件流是程序与文件之间的抽象通道。
- 可以使用 `open()` 或声明时初始化机制将文件流连接到文件。
- 打开到某个文件的 `ifstream` 会用该文件的内容初始化文件流，并将读取位置置于文件流中的第一个字符处。
- 打开到某个文件的 `ofstream` 会将文件流初始化为空（只包含文件结束标记），并将写入位置置于文件结束标记处。文件原先的任何内容都会被销毁。
- 如果使用 `ios::app` 打开到某个文件的 `ofstream`，则流会用该文件的内容初始化，并将写入位置置于文件末尾。
- 跳过前导空白字符后，输入运算符（`>>`）会提取 `ifstream` 中读取位置之后的第一个值，并将读取位置推进到该输入值之后的第一个字符。数值由非数字字符分隔。
- `getline()` 函数提取从 `ifstream` 中读取位置开始的那一行输入，并将提取的字符存储到 `string` 变量中，遇到换行符时停止。它会把读取位置留在该换行符之后的第一个字符处。混用 `getline()` 和输入运算符时必须小心。
- 输出运算符（`<<`）将一个值插入 `ofstream` 的当前写入位置，并将其推进到紧随该值之后的位置。
- 当输入/输出完成后，应通过调用 `close()` 来断开文件流与文件的连接。

## 11.3 其他流特性

我们已经了解了 `open()`、`is_open()`、`<<`、`>>`、`getline()`、`eof()` 和 `close()` 等基本文件流操作，但还有许多其他操作。其中，我们在前面的章节中讨论过：使用 `get()` 从流中读取一个字符而不跳过空白字符；使用 `good()`、`bad()` 和 `fail()` 检查流的状态；使用 `clear()` 重置流的状态位；使用 `ignore()` 跳过字符；以及各种流操纵符。下表列出了可以发送给 `istream` 和 `ifstream` 对象，或发送给 `ostream` 和 `ofstream` 对象的一些流消息。但这并不是一份详尽的列表；`iostream` 和 `fstream` 库非常庞大，此表仅展示了其中一小部分功能。

| 成员函数 | 说明 |
|---|---|
| `good()` | 若 `good` 位被置位（1）则为 true，否则为 false |
| `fail()` | 若 `fail` 位被置位（1）则为 true，否则为 false |
| `bad()` | 若 `bad` 位被置位（1）则为 true，否则为 false |
| `eof()` | 若 `eof` 位被置位（1）则为 true，否则为 false |
| `clear()` | 将 `good` 位重置为 1，将所有其他状态位重置为 0 |
| `setstate(sBit)` | 将状态位 `sBit` 置为 1，其中 `sBit` 是 `ios::badbit`、`ios::failbit`、`ios::eofbit` 中的一个或多个 |
| `get(ch)` | 将下一个字符（包括空白字符）读入 `ch` |

