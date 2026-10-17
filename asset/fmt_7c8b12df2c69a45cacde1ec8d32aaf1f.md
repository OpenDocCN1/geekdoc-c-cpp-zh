
第一个参数 `Path.Combine(pathname, filename)` 将路径名和文件名结合起来形成一个单一参数。默认情况下，如果你没有为文件提供路径名，C# 会假设你希望将文件放置在程序可执行文件相同的目录中。如果你将此内容存储在 C 盘上名为 `TestCode` 的文件夹中，并将项目命名为 `ErrorLogger`，则应向代码提供默认路径：

```c
C:\TestCode\ErrorLogger\Debug\ErrorLog.txt
```

第二个参数是一个布尔值，值为 `true`。如果第二个参数为 `true`，则所有新文本将追加到文件末尾。如果文件不存在，则创建它。如果第二个参数为 `false` 且文件存在，则文件中的当前数据将被覆盖。如果文件不存在且第二个参数为 `false`，则会创建文件，并向文件中写入新数据。

你已经为该类重载了 `WriteErrorLog()` 方法。这两个方法的签名如下：

```c
public int WriteErrorLog()
public int WriteErrorLog(string msg)
```

### 在 `Main` 中，你将错误消息传递给了构造函数。该错误消息随后赋值给类成员 `errorMessage`。然而，如果 `clsError` 已经实例化且你想向文件写入另一个错误消息，可以使用接受字符串作为参数的 `WriteErrorLog()` 方法。该版本的代码显示错误消息被赋值给 `errorMessage`，并调用了无参数版本的 `WriteErrorLog()`。在两种情况下，都保留了相应的返回值。

```csharp
public int WriteErrorLog(string msg)
{
    errorMessage = msg; // 复制消息
    errorFlag = WriteErrorLog(); // 现在调用原始方法
    return errorFlag;
}
```

执行实际操作的 `WriteErrorLog()` 代码嵌入在一个 `try-catch` 块中。这个代码块是一个好主意，因为电机械设备是计算机系统的致命弱点。使用 `StreamWriter` 对象的 `WriteLine()` 方法将错误消息写入文件。`WriteLine()` 方法与 `Write()` 方法的区别在于，`WriteLine()` 会当前保存的字符串末尾追加一个新字符。语句如下：

```c
sw.WriteLine(currentDT.ToShortDateString() + " "," + "*");
             currentDT.ToShortTimeString() + " : " + errorMessage);
sw.WriteLine("--------------------");
sw.Close();
```

第一次调用 `WriteLine()` 通过传递给类的错误消息将当前日期和时间写入文件。第二次调用 `WriteLine()` 只是写入一串连字符，以便每条错误消息的结尾更容易区分。最后一条语句通过调用 `StreamWriter` 对象的 `Close()` 方法关闭文件。

## 读取数据

在数据写入磁盘后，控制权最终返回到语句：

```csharp
txtErrorMsgs.Text = myErrorLog.ReadErrorLog();
```

该语句使用 `ReadErrorLog()` 方法读取错误日志文件的内容（当然，你可以使用记事本或某些等程序来读取文件）。读取文件的代码为：

```csharp
public string ReadErrorLog()
{
    string buff;
    try
    {
        string pfn = Path.Combine(pathName, fileName);
        if (File.Exists(pfn) == true)
        {
            sr = new StreamReader(pfn);
            buff = sr.ReadToEnd();
            sr.Close();
            return buff;
        }
    }
    catch (Exception ex)
    {
        return ex.Message;
    }
    return "";
```

再次，代码被一个 `try-catch` 块包围以防止程序非正常退出。代码随后构建路径和文件名并将它们赋值给变量 `pfn`。代码随后使用 `File` 对象确定其是否存在（无需显式实例化，因为它是一个静态方法）。假设文件确实存在，你实例化了一个名为 `sr` 的 `StreamReader` 对象。`StreamReader` 类的 `ReadToEnd()` 方法读取文件中所有的字符串数据并将其赋值给 `buff`，然后返回调用者。在代码中，你只需将字符串复制到 listbox 对象。

## 使用 clsErrorLog

与你之前的程序不同，`clsErrorLog` 类本身实际上是有用的。如果你在代码中使用 `try-catch` 块或使用 `use` 语句来感知 `except` 以外的错误状况，当发生错误时，其内容可以根据你的信息需求而变化。如果是在商业产品中有人要求支持，你可以让调用者用记事本读取 `ErrorLog.txt` 文件，至少对哪里出了问题有一个大致的概念。

诚然，程序很简单，但如果你需要，可以随时添加功能。这就是面向对象编程（OOP）的优点之一——你可以随时扩展类以适应你的特定需求。

## 顺序访问与随机访问文件

列表 13-3 和 13-4 所示的错误日志程序将文本数据写入名为 `ErrorLog.txt` 的磁盘文件。如果日志文件不存在，则创建它并将新数据写入文件。如果文件存在且已存储了信息，则新数据将追加到现有文件的末尾。随着多年推移，如果错误不断添加，此文件可能会变得很大。通常，在读取文本文件时，读取程序从文件开始并读取数据。

当前位置以及你想要读取的记录。`Seek()` 方法的通用语法如下：

```
Seek( (desiredRecord - 1) * RECORDSIZE, SeekOrigin.Begin);
```

与编程中的几乎所有情况一样，随机访问文件中的第一条记录实际上是第 0 条记录。因此，如果每个 `RECORDSIZE` 为 300 字节，而你想读取第 5 条记录，你必须将文件指针（File Pointer）置在从 BOF（文件开头）起量 1,200 字节的位置。目标记录号是 5，文件中的实际位置计算方式如下：

```
Seek( (desiredRecord - 1) * RECORDSIZE, SeekOrigin.Begin);
Seek( (5 - 1) * 300, SeekOrigin.Begin);
Seek( 1200, BOF);
```

你可以将最后这条语句理解为：“使用 `Seek()` 方法将文件指针移动到相对于文件偏移 1,200 字节的位置。”这如图 13-7 所示。

EOF

| 1 | 2 | 3 | 4 | 5 | 6 | 525 | 526 |

|---|---|---|---|---|---|---|---|

| 0 | 300 | 900 | 1200 | 1500 | | | |

BOF

 Seek() File Pointer

图 13-7: 使用 Seek()

`Seek()` 方法的第一个参数是文件指针要移动的字节偏移量，用 `long` 数据类型表示。`Seek()` 的第二个参数是文件指针移动的相对位置。`Seek()` 方法的第二个参数为移动文件指针提供了三个相对点。

第一个 `SeekOrigin.Begin` 通过相对于 BOF 的字节偏移量来确定文件指针的位置。如图 13-7 所示：文件指针相对于 BOF 为 1,200 字节。

其次，`SeekOrigin.Current` 相对于文件指针的当前位置移动文件指针。例如，如果你已经读取了第 5 条记录，文件指针的当前位置将位于第 6 条记录的开头（相对于 BOF 的字节偏移量为 1,500）。如果你想读取第 4 条记录，可以使用

```
Seek(-600, SeekOrigin.Current);
```

因为字节偏移量是负数，文件指针将从当前位置回移 600 字节，即到达第 4 条记录的开头。（图 13-7 中的字节偏移量 = 900。）因此，负偏移量意味着你想将文件指针向 BOF 移动。

文件指针的第三个相对点是 `End` 语句

```
Seek(0, SeekOrigin.End);
```

将文件指针置在文件末尾 EOF。`Seek (-300, SeekOrigin.End)` 将文件指针置在什么位置？根据图 13-7，你的代码将准备好读取第 526 条记录。

想一一下，在使用 `SeekOrigin.End` 读文件时使用正偏移量是一个错误。正字节偏移量意味着你正尝试读取文件的末尾。同样，在用 `SeekOrigin.Begin` 时使用负字节偏移量也是错误的。这会意味着文件指针放置在文件开头“之前”的位置。

## 随机访问文件的优缺点

随机访问文件最大的优势是你可以比使用顺序文件快地访问特定记录。在文件中使用客户记录的位置来存储与该客户相关的唯一信息是非常常见的。例如，想象一个客户的名字是 Smith。字母 S 的 ASCII 代码是 300 字节。因此，你可以将该客户写入文件的记录位置 83。如果每个记录是 300 字节，那么该人的信息将存储在相对于 BOF 偏移量 24,900 字节处。这种使用一条信息（S）来推导出第二条信息（记录 83）的方法被称为哈希（hashing）。在随机访问文件的记录位置使用哈希算法可以定位单个记录。显然，如果文件中添加了第二个 Smith，就会产生哈希冲突，哈希算法必须处理这种情况。请参考在线帮助获取更多详情：一个可以在程序中使用的 `HashAlgorithm` 类。

随机访问文件不仅在查找特定信息方面更好，更新信息方面也更快。由于随机访问文件中的每条记录大小完全相同，你可以轻松地更新特定记录并进行重写，而不需要复制整个文件。使用随机访问文件更新记录快得多，因为你只需要重写已更改的那条记录。

随机访问文件的坏处是，你必须根据最坏的情况来设计记录大小。尽管你知道大多数人的名字不会超过 10 个字符，但你仍需要为客户的名字留出的字节数设计为 15 字节，因为那对古怪的父母认为给儿子起名叫 Guyfrontanza 很有酷。记录中的所有信息也是如此。显然，设计每条数据大小的秘诀在于浪费空间和记录必要信息之间取得平衡。
