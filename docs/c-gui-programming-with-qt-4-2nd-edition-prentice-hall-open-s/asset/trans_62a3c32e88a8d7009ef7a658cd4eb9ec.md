
对于文件格式，可能需要一个完整的解析器。这种解析器可以通过 `>> QChar` 逐字符读取数据，或者通过 `QTextStream::readLine()` 逐行读取数据。在本节的末尾，我们展示了两个小示例：一个是逐行读取输入行，另一个是逐字符读取。对于处理文本的解析器，如果我们不担心内存使用，或者知道文件将会很，可以使用 `QTextStream::readAll()` 一次性读取整个文件。

默认情况下，`QTextStream` 使用系统的本地编码（例如，美国和欧洲大部分地区使用的 ISO 8859-1 或 ISO 8859-15）进行读取和写入。可以使用 `setCodec()` 如下所示进行更改：

```
stream.setCodec("UTF-8");
```

示例中使用的 UTF-8 编码是一种与 ASCII 兼容的编码，可以表示整个 Unicode 字符集。关于 Unicode 以及 `QTextStream` 对编码的支持更多信息，请参阅第 18 章。

`QTextStream` 有类似于 `<iostream>` 提供的各种选项。这些可以通过在流上传递特殊对象（称为流操纵符）来更改其状态，或者通过调用图 12.1 中列出的函数来设置。下面的示例在设置 `showcase`、`uppercasedigit` 和 `hex` 选项之前输出整数 12345678，产生文本 "0xBC614E"：

```
out << showcase << uppercasedigit << hex << 12345678;
```

## 图 12.1. 设置 QTextStream 选项的函数

| | 根据前缀自动检测（读取时） |
|---|---|
| 0 | |
| 2 | 二进制 |
| 8 | 八进制 |
| 10 | 十进制 |
| 16 | 十进制 |

| setNumberFlags(NumberFlags) |
|---|---|

## ShowBase

| | |
|---|---|
| 如果基数为 2 则显示前缀 ("0b") |

| | |
|---|---|
| setRealNumberNotation(RealNumberNotation) | |
| FixedNotation | 定点计数表示法（例如 "0.000123"） |
| ScientificNotation | 科学计数法（例如 "1.234568e-04"） |
| SmartNotation | 定点或科学计数法，以最紧凑的为准 |

| setRealNumberPrecision(int) |
设置应生成的最大位数（默认为 6） |

| setFieldWidth(int) |
设置字段的最小宽度（默认为 0） |

| | |
|---|---|
| setFieldAlignment(FieldAlignment) | |
| AlignLeft | 在字段右侧填充 |
| AlignRight | 在字段左侧填充 |
| AlignCenter | 在字段两侧均填充 |
| AlignAccountingStyle | 在符号和数字之间填充 |

| setPadChar(QChar) |
设置用于填充字段的字符（默认为空格） |

与 `QDataStream` 类似，`QTextStream` 作用于 `QIODevice` 子类，该类可以是 `File`、`QTemporaryFile`、`QBuffer`、`QProcess`、`QTcpSocket`、`QUdpSocket` 或 `QSSslSocket`。此外，它也可以直接用于 `QString`。例如：
```cpp
QString str;
QTextStream(&str) << oct << 31 << " " << dec << 25 << endl;
```

这使得 `str` 的内容变为 "37 25\n"，因为十进制 31 在八进制中表示为 37。在这种情况下，我们不需要在流上设置编码，因为 `QString` 始终是 Unicode。

让我们来看一个基于文本的文件格式简单示例。在第一部分描述的电子表格应用程序中，我们使用二进制格式来存储电子表格数据。数据由一系列 (行, 列, 公式式) 三元组组成，每个三元组对应一个非空单元格。直接写入数据是简单的；以下是 `Spreadsheet::writeFile()` 修订版本的一个片段：

```cpp
QTextStream out(&file);
for (int row = 0; row < RowCount; ++row) {
  for (int column = 0; column < ColumnCount; ++column) {
    QString str = formula(row, column);
    if (!str.isEmpty()) {
      out << row << " " << column << " " << endl;
    }
  }
}
```

我们使用了一种简单的格式，每行代表一个单元格，行与列之间、列与公式之间有空格。公式可以包含空格，但我们可以假设它不包含 '\n'（我们用它来结束行）。现在让我们来看对应的读取代码：

```cpp
QTextStream in(&file);
while (in.atEnd()) {
    QString line = in.readLine();
    QStringList fields = line.split(' ');
    if (fields.size() >= 3) {
        int row = fields.takeFirst().toInt();
        int column = fields.takeFirst().toInt();
        setFormula(row, column, fields.join(' '));
    }
}
```

我们一次逐行地读取电子表格数据。`readLine()` 函数会移除末尾的 '\n'。`QString::split()` 返回一个列表，在指定的分隔符处分割其字符串。例如，行 `5 19 Total value` 会导致产生包含四个项的列表 `["5", "19", "Total", "value"]`。

