
除了 Java 风格迭代器外，每个顺序容器类 `C<T>` 都有 STL 风格的类型：`C<T>::iterator` 和 `C<T>::const_iterator`。两者的区别在于 `const_iterator` 不修改数据。

容器的 `begin()` 返回一个 STL 风格的迭代器，指向容器中的第一个项（例如 `list[0]`），而 `end()` 返回指向“最后一个项之后”的项（例如，大小为 5 的列表对应的 `list[5]`）。图 11.5 显示了 STL 风格迭代器的有效位置。如果容器是空的，可以使用 `begin()` 等于 `end()` 来检查容器是否有项，尽管通常为此目的调用 `isEmpty()` 往往更方便。

> 在多线程程序中，数据共享通常被视为一个选项，因为引用计数中存在竞态条件。在 Qt 中，这不是问题。内部，容器-ner 类使用汇编语言指令来执行原子计数。这种技术通过 Qt 中的 `QSharedData` 和 `QSharedDataPointer` 类提供。

程序支持 `break` 和 `continue` 循环语句。如果循环体只包含一条语句，则不需要大括号。就像 `for` 语句一样，迭代变量可以在循环外定义，如下所示：

```
QLinkedList<Movie> list;
Movie movie;
...
foreach (movie, list) {
    if (movie.title() == "Citizen Kane") {
        std::cout << "Found Citizen Kane" << std::endl;
        break;
    }
}
```

对于持有包含逗号的数据类型（例如 `QPair<QString, int>`）的容器，将迭代变量定义在循环之外是唯一的选择。

## 关联容器

关联容器存储任意数量的相同类型的项，并通过键（key）进行索引。Qt 提供了两个关联容器类：`QMap<K, T>` 和 `QHash<K, T>`。

`QMap<K, T>` 是一种按升序存储键值对的数据结构，如图 11.6 所示。这种排列使得提供良好的查找和插入性能，以及按键顺序迭代成为可能。内部，`QMap<K, T>` 实现为跳跃表（skip-list）。

### 图 11.6. 从 QString 到 int 的映射

![](img/5a524abdf0b0d58fa99d30abb4463611_448_0.png)

```
QMap<QString, int> map;
map.insert("eins", 1);
map.insert("sieben", 7);
map.insert("dreindundzwanzig", 23);
```

或者，我们可以按照如下方式直接为给定的键赋值：

```
map["eins"] = 1;
map["sieben"] = 7;
map["dreindundzwanzig"] = 23;
```

`[]` 运算符可用于插入也可用于检索。如果在非 const map 中对不存在的键使用 `[]` 检索值，则将使用给键和一个空值创建一个新项。为了避免意外创建空值，我们可以使用 `value()` 函数来检索项而不是 `[]`：

```
int val = map.value("dreindundzwanzig");
```

如果键不存在，则将使用值类型的构造函数返回一个默认值，且不会创建新项。对于基本类型和指针类型，返回 0。我们可以将另一个默认值作为 `value()` 的第二个参数，例如：

```
int seconds = map.value("delay", 30);
```

`QMap<K, T>` 的 K 和 T 数据类型可以是像 `int` 和 `double` 这样的基本数据类型、指针类型，或者是具有默认构造函数、拷贝构造函数和赋值运算符的类。此外，K 类型必须提供 `operator<()` 运算符，因为 `QMap<K, T>` 使用该运算符按升序顺序存储项。

`QMap<K, T>` 有两个方便函数：`keys()` 和 `values()`，它们在处理小型数据集时特别有用。它们返回 map 的键和值的 `QList`。

映射大多是单值的：如果为现有键分配一个新值，该值将由新值替换，确保没有两个项共享相同的键。使用 `insert()` 函数或 `QMultiMap<K, T>` 方便子类可以拥有具有相同键的多个键值对。`QMap<K, T>` 有一个 `values(const K &)` 重载，返回给定键的所有值的 `QList`。例如：

```cpp
QMultiMap<int, QString> multiMap;
multiMap.insert(1, "one");
multiMap.insert(1, "eins");
multiMap.insert(1, "uno");
```

```
QList<QString> vals = multiMap.values(1);
```

`QHash<K, T>` 是一种在哈希表中存储键值对的数据结构。它的接口与 `QMap<K, T>` 几乎相同，但它对 K 类型有不同要求，并且通常提供比 `QMap<K, T>` 能实现的快的查找速度。另一个区别是 `QHash<K, T>` 是无序的。除了对存储在容器中的任何值类型的标准要求外，`QHash<K, T>` 的 K 类型需要提供 `operator==()` 运算符和一个全局 `qHash()` 函数，该函数返回键的哈希值。对于整数类型、指针类型、`QString` 和 `QByteArray`，`QHash<K, T>` 自动为其哈希表分配桶，并在插入或删除项时调整其大小。还可以通过调用 `reserve()` 指定预期的项数量，并调用 `squeeze()` 在项少于预期时最小化内存使用来微调性能。

哈希是无名的，但可以使用 `insert()` 函数或 `QMultiHash<K, T>` 方便子类为同一个键分配多个值。除了 `QHash<K, T>` 之外，Qt 还提供了一个 `QCache<K, T>` 类，用于缓存与键关联的对象，以及一个只存储键的 `QSet<T>` 容器。遍历关联容器中存储的所有键值对的最简单方法是使用 Java 风格的迭代器。

`Copy()` 也可以用于复制同一个容器内的值，只要源范围和目标范围不重叠。在下一个代码段中，我们使用它将列表的最后两个项替换为前两个项：

```
qCopy(list.begin(), list.begin() + 2, list.end() - 2);
```

`qSort()` 算法将容器中的项按升序排序：

```
qSort(list.begin(), list.end());
```

默认情况下，`qSort()` 使用 `<` 运算符来比较项。要按降序排序项，请将 `qGreater<T>()` 作为第三参数（其中 T 是容器的数值类型），如下：

```cpp
qSort(list.begin(), list.end(), qGreater<int>());
```

我们可以使用第三个参数定义自定义排序标准。例如，这里有一个“小于”比较，它以不区分大小的方式比较 QString：

```cpp
bool insensitiveLessThan(const QString &str1, const QString &str2) {
  return str1.toLower() < str2.toLower();
}
```

对 `qSort()` 的调用随后变为

```cpp
QStringList list;
...
qSort(list.begin(), list.end(), insensitiveLessThan);
```

`qStableSort()` 算法与 `qSort()` 类似，但它保证比较相同的项将保持原来的顺序出现。如果排序标准只考虑值的一部分且结果对用户可见，那么这将非常有用。我们在第 4 章使用了 `qStableSort()` 来实现表格应用程序中的排序（第 92 页）。

`qDeleteAll()` 算法对每个指针类型的指针调用 `delete`。在容器中，该调用仅对值类型为指针类型的容器有意义。调用之后，这些项仍然以悬空指针的形式存在于容器中，因此通常我们还会在对容器调用 `clear()`。例如：

```
qDeleteAll(list);
list.clear();
```

`qSwap()` 算法交换两个变量的值。例如：

```cpp
int x1 = line.x1();
int x2 = line.x2();
if (x1 > x2)
    qSwap(x1, x2);
```

最后，`<QtGlobal>` 头文件（被其他每个 Qt 头文件包含）提供了几个实用的定义，包括返回参数绝对值的 `qAbs()` 函数，以及返回两个值最小值或最大值的 `qMin()` 和 `qMax()` 函数。

## 字符串、字节数组和变体

`QString`、`QByteArray` 和 `QVariant` 是三个类，它们在容器中具有许多特性，在某些情况下可以作为容器的替代方案。同样与容器一样，这些类使用隐式共享来优化内存和速度。

我们将从 `QString` 开始。每个 GUI 程序都使用字符串，不仅用于用户界面，还作为数据结构。C++ 原生提供两种字符串：传统的 C 风格以 `\0` 终止的字符数组和 `std::string` 类。与这些不同，`QString` 持有 16 位 Unicode 字符。Unicode 包含 ASCII 和 Latin-1 作为子集，但自 16 位以来，它代表了数千其他字符，用于编写世界上大多数的语言。有关 Unicode 的更多信息，请参见第 18 章。

使用 `QString` 时，我们不需要担心分配内存的晦涩细节或确保数据以 `\0` 结尾。从概念上讲，`QString` 可以被视为 `QChar` 的向量。`QString` 可以轻松地嵌入 `\0` 字符。`length()` 函数返回整个字符串的大小，包括嵌入的 `\0` 字符。

`QString` 提供了一个二进制 `+` 来连接两个字符串，以及一个 `+=` 运算符将一个字符串附加另一个字符串。由于 `QString` 会自动在字符串数据的末尾预分配内存，因此通过重复追加字符来构建字符串非常快。这里有一个结合 `+` 和 `+=` 的示例：

```cpp
QString str = "User: ";
str += userName + "\n";
```

还有一个 `QString::append()` 函数，其作用与 `+=` 运算符相同：

```cpp
str = "User: ";
str.append(userName);
str.append("\n");
```

另一种完全不同的字符串字符串是使用 `QString` 的 `sprintf()` 函数：

```cpp
str.sprintf("%s %.1f%%", "perfect competition", 100.0);
```

该函数支持与 C++ 库中的 `sprintf()` 函数相同的格式说明符。在前面的示例中，str 被赋值为 "perfect competition 100.0%%"。

另一种从其他字符串或数字构建字符串的方法是使用 `arg()`：

```cpp
str = QString("%1 %2 (%3s-%4s)")
.arg("permissive").arg("society").arg(1950).arg(1970);
```

在这个示例中，"%1" 被替换为 "permissive"，"%2" 被替换为 "society"，"%3" 被替换为 "1950"，"%4" 被替换为 "1970"。结果是 "permissive society (1950s-1970s)"。存在多种重载来处理各种数据类型。某些重载带有额外的参数来控制字段宽度、数值基数或浮点精度。通常，`arg()` 是比 `sprintf()` 好得多的解决方案，因为它是类型安全的，完全支持 Unicode，并允许翻译人员重新排列 "%n" 参数。

`QString` 可以使用 `QString::number()` 静态函数将数字转换为字符串：

```cpp
str = QString::number(59.6);
```

或者使用 `setNum()` 函数：

```cpp
str.setNum(59.6);
```

使用 `toInt()`、`toLong()`、`toDouble()` 等函数可以将字符串转换为数字。例如：

```cpp
bool ok;
int i = str.toInt(&ok);
```

这些函数接受一个布尔值指针来指示是否成功。如果失败，则返回 0。

如果我们想从字符串中提取部分，可以使用 `mid()` 函数。起始位置。例如：

```cpp
bool ok;
double d = str.toDouble(&ok);
```

如果我们想知道字符串是否包含某个字符、子字符串或正则表达式，可以使用 `QString` 的 `indexOf()` 函数：

```cpp
QString str = "the middle bit";
int i = str.indexOf("middle");
```

这将设置 i 为 4。`indexOf()` 函数在失败时返回 -1，并接受可选的起始位置和大小写敏感标志。

如果我们只是想检查字符串是否以某个内容开头或结尾，可以使用 `startsWith()` 和 `endsWith()` 函数：

```cpp
if (url.startsWith("http:") && url.endsWith(".png"))
...
```

前面的代码比下面的代码更简单且快速：

```cpp
if (url.left(5) == "http:" && url.right(4) == ".png")
...
```

使用 `==` 运算符进行字符串比较是区分大小写的。如果是比较用户字符串，通常使用 `localeAwareCompare()`，如果我们想让比较不区分大小写，可以使用 `toUpper()` 和 `toLower()`。例如：

```cpp
if (fileName.toLowerCase() == "readme.txt")
...
```

如果我们想用另一个字符串替换字符串的某，可以使用 `replace()`：

```cpp
QString str = "a cloudy day";
str.replace(2, 6, "sunny");
```

结果是 "a sunny day"。代码可以重写为 `remove()` 和 `insert()`：
