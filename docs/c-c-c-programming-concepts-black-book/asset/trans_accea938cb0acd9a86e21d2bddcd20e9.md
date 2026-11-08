
在前面的示例中，我们检查了流对象的错误状态，以判断是否已到达文件末尾，如下所示：

```cpp
while (infile)
{
    // ... Processing of File
}
```

在前面的代码片段中，当到达文件末尾时，infile 变为零。

如果文件不存在，ios::nocreate 标志会在打开文件时报告错误。修改后的 diskin() 函数如下：

```cpp
void Medicine_File::diskin(void)
{
    ifstream ifile("MEDICINE.TXT", ios::nocreate);
    if (ifile)
    {
        ifile.read((char *) &buffer, sizeof(buffer));
        while (ifile)
        {
            buffer.showdata();
            ifile.read((char *) &buffer, sizeof(buffer));
        }
    }
    else
    {
        cout<< "The file does not exist!";
    }
}
```

如果 MEDICINE.TXT 不存在，ifile 的值将变为零，屏幕上会出现错误消息“文件不存在！”。

## 流状态位

C++ I/O 系统维护关于每次 I/O 操作结果的状态信息。状态由一组位的设置（0 或 1）来表示，这些位由 ios 类中声明的 io_state 变量定义。表 15.2 列出了流状态位：

**表 15.2：流状态位**

| 状态位 | 描述 |
| --- | --- |
| eofbit | 当输入流到达末尾时置位。它表示没有更多字符可供提取。 |
| failbit | 当上一次插入或提取失败时置位。这是可恢复错误。流仍处于可用状态。 |
| badbit | 当尝试非法插入或提取时置位。该流不适合继续使用。通常，在打开不存在的文件或在已越过 EOF 后执行定位时置位。 |
| hardfail | 当发生硬件故障时置位。导致 hardfail 置位的错误通常不可恢复。 |

下一节说明用于访问流状态位的成员函数。

### 用于访问流状态位的成员函数

本节将提供用于访问流状态位的成员函数列表。表 15.3 提供了成员函数列表及其说明：

**表 15.3：成员函数**

| **成员函数** | **描述** |
| --- | --- |
| `int good()` | 如果流正常，返回非零值；否则返回零 |
| `int bad()` | 如果 badbit 或 hardfail 位被置位，返回非零值；否则返回零 |
| `int eof()` | 如果 eofbit 被置位，返回非零值；否则返回零 |
| `int fail()` | 如果 failbit、badbit 或 hardfail 位被置位，返回非零值 |
| `int rdstate()` | 返回 iostate 变量的当前值 |
| `void clear(int ef=0)` | 将错误标志设置为 ef；默认情况下，ef 等于零，这会重置所有错误位 |

接下来，让我们学习随机访问。

## 随机访问

C++ I/O 程序为文件管理两个整数值。一个是 get 指针，它指定文件中下一次输入或读取操作将发生的位置。另一个是 put 指针，它指定文件中输出或创建操作将发生的位置。这两个指针分别表示实际读取和创建操作的当前位置。每次发生输入或输出操作时，这些指针通常会按读取或写入的字节数依次向前推进。此上下文中的指针一词不应与用作地址参数的普通 C++ 指针混淆，而应理解为当前偏移位置，即下一次输入或输出操作将发生的位置。通常，我们可能需要从文件开头开始读取当前文件，并依次继续到最终结果。写入时，我们可能想从开头开始，删除任何当前内容，或追加到末尾。这些将是默认活动；因此，无需对文件指针进行任何关键操作。然而，有些情况下，我们必须直接管理文件指针，以便从特定文件内的任意位置读取和写入。

`seekg()` 和 `tellg()` 函数允许我们设置和检查 get 指针；而 `seekp()` 和 `tellp()` 函数允许我们设置和检查 put 指针。因此，我们可以使用这些函数以随机访问模式访问文件。iostream 类的所有对象都可以使用 seekg() 函数或 seekp() 函数进行操作。这些函数将 get 和 put 指针移动到文件内的绝对偏移位置，或相对于某个位置的特定字节数处。tellg() 和 tellp() 函数可用于查明文件中 get 或 put 指针的当前位置。

seekg() 函数接受两个参数。第一个参数可以是一个长整数，指定将指针定位到多少字节处（也称为偏移量）。第二个参数可以是参考点。例如，`file.seekg(10, ios::beg)` 将指针定位到相对于文件开头 10 字节处。该类中定义的三个参考点如表 15.4 所示：

**表 15.4：参考点**

| **参考点** | **描述** |
| --- | --- |
| `ios::beg` | 表示文件开头 |
| `ios::cur` | 表示文件指针的当前位置 |
| `ios::end` | 表示文件末尾 |

seekg() 函数的第一个参数也可以指定负值。它有助于相对于文件末尾向后移动文件指针。例如，以下语句将文件指针相对于文件末尾向后移动 20 字节：

```cpp
file.seekg(-20, ios::end);
```

如果只提供一个参数，则默认假定为 ios::beg。例如，考虑以下语句：

```cpp
file.seekg(16);
```

在前面的语句中，ios::beg 将是默认参考点。另一方面，tellg() 函数没有任何参数。它返回 get 指针相对于文件开头的现有字节位置。考虑以下语句：

```cpp
long position = file.tellg();
```

这将使 position 变量取得 get 指针当前位置的值。seekp() 和 tellp() 函数在功能上与 seekg() 和 tellg() 函数相同，只是它们与 put 指针相关。seekg() 和 tellg() 函数定义在 istream 类中，seekp() 和 tellp() 函数定义在 ostream 类中。

### 随机访问示例

在 C++ 中打开文件后，我们可以在文件内的任何位置（包括文件末尾）放置两个文件指针——一个用于读取，另一个用于写入——以从中读取或写入数据。然而，在随机访问中，可以完全自由地从文件内的任何位置读取或写入数据。本节说明如何随机查询文件以访问其中的信息。考虑以下示例，从 MEDICINE.TXT 文件中检索特定记录：

```cpp
void main()
{
    medicine medobj;
    fstream ifile("MEDICINE.TXT",ios::in);
    ifile.seekg(0, ios::end);
    long endpos = ifile.tellg();
    cout<< "\n the size of the file is:" << endpos;
    cout<< "\n the size of a medicine record is:" << sizeof(medicine);
    int n = endpos/sizeof(medicine);
    cout<< "\n" << n << "medicine records exists in the file";
    cout<< "\nmedicine record query:";
    cout<< "\nwhich record do you want to query?";
    cout<< "\nPlease enter the record number";
    int num;
    cin>> num;
    int seekpos = (num - 1)*sizeof(medicine);
    ifile.seekg(seekpos);
    ifile.read((char *) &medobj, sizeof(medicine));
    medobj.showdata();
}
```

在前面的示例中，查询将基于用户希望查询的记录号。如果用户希望查看第 15 条记录，那么 seekg(15*sizeof(medicine), ios::beg) 就足以将我们带到第 15 条记录的开头。

## 格式化 I/O——ios 格式函数

C++ I/O 系统使我们能够格式化 I/O 过程。例如，我们能够设置区域宽度、指定数字基数，或确定小数点后将显示多少位数字。我们可以使用两种相关但在概念上不同的方式来格式化数据。首先，我们可以访问
