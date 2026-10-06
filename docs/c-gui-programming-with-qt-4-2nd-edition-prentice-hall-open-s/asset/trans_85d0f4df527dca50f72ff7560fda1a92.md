

## 11. 容器类

- 顺序性容器
- 关联型容器
- 通用算法
- 字符串、字节数组和变体

容器类是通用的模板类，用于在内存中存储某种类型的项。C++ 已经作为标准模板库（STL）的一部分提供了许多容器，STL 包含在标准 C++ 中。

Qt 提供了了自己的容器类，对于 Qt 程序，我们可以同时使用 Qt 容器和 STL 容器。Qt 容器的主要优势是它们在所有平台上的行为相同，并且它们是隐式共享的（implicitly shared）。共享或“写时复制”（copy on write）是一种优化，使得容器可以以值的形式传递，而不会产生显著的性能开销。Qt 容器还具有受 Java 启发的易用迭代器类，它们可以使用 QStream 进行流处理，并且通常在可执行文件中生成的代码比相应的 STL 容器更少。最后，在 Qt/嵌入式 Linux 支持的某些硬件平台上，Qt 容器是唯一可用的。

Qt 同时提供了顺序性容器（如 `QVector<T>`、`QLinkedList<T>` 和 `QList<T>`）和关联型容器（如 `QMap<K, T>` 和 `QHash<K, T>`）。从概念上讲，顺序性容器一个接一个存储存储，而关联型容器则存储键值对。

Qt 还提供了在任意容器上执行操作的通用算法。例如，`qSort()` 算法对顺序性容器进行排序，而 `qBinaryFind()` 对排序后的顺序性容器进行二分查找。这些算法与 STL 提供的算法相似。

如果你已经熟悉 STL 容器，并且在目标平台上可以使用 STL，那么你可能希望使用它们来替代 Qt 容器，或者与之结合使用。关于 STL 类和函数的更多信息，一个很好的起点是 SGI 的 STL 网站：http://www.sgi.com/tech/stl。

在本章中，我们还将会查看 `QString`、`QArray` 和 `QVariant`，因为它们与容器有许多共同点。`QString` 是一种贯穿 Qt API 的 16 位 Unicode 字符串。`QArray` 是一个 8 字节字符数组，常用于存储二进制数据。`QVariant` 是一种可以存储更多 C++ 和 Qt 值类型的类型。

## 顺序性容器

`QVector<T>` 是一种类似于数组的数据结构，它将项存储在内存的相邻位置，如图 11.1 所示。`vector` 与普通 C++ 数组的区别在于 `vector` 有自己的大小并且可以调整大小。在 vector 的末尾添加额外的项是高效的，而在 vector 的开头或中间插入项可能是昂贵的。

### 图 11.1. 双精度浮向量

![](img/5a524abdf0b0d58fa99d30abb4463611_437_0.png)

如果我们预先知道需要多少项，我们可以在定义 vector 时给它一个初始大小，并使用 `[]` 运算符为项赋值；否则，我们必须在稍后调整 vector 的大小或后添加项。这里有一个指定初始大小的示例：

```
QVector<double> vect(3);
vect[0] = 1.0;
vect[1] = 0.540302;
vect[2] = -0.416147;
```

这里是同样的示例，这次从空 vector 开始并使用 `append()` 函数在末尾添加项：

```
QVector<double> vect;
vect.append(1.0);
vect.append(0.540302);
vect.append(-0.416147);
```

我们也可以使用 `<<` 运算符代替 `append()`：

```
vect << 1.0 << 0.540302 << -0.416147;
```

遍历 vector  way的一种一种方法是使用 `[]` 和 `count()`：

```
double sum = 0.0;
for (int i = 0; i < vect.count(); ++i)
    sum += vect[i];
```

在 `QVector<T>` 的开头或中间插入项、从这些中删除项，对于大型 vector 来说可能是低效的。因此，使用了 `QLinkedList<T>`，这是一种数据结构，它将项存储在内存非相邻的位置，如图 11.2 所示。与 vector 不同，链表不支持随机访问，但它们提供了“常数时间”的插入和删除。

### 图 11.2. 双精度浮链表

![](img/5a524abdf0b0d58fa99d30abb4463611_438_0.png)

链表不支持 `[]` 运算符，因此必须使用迭代器来遍历它们的项。迭代器也用于指定项的位置。例如，下面的代码在 "Clash" 和 "Ramones" 之间插入字符串 "Tote Hosen"：

```
QLinkedList<QString> list;
list.append("Clash");
list.append("Ramones");
```

```
QLinkedList<QString>::iterator i = list.find("Ramones");
list.insert(i, "Tote Hosen");
```

我们将在本节稍后更详细查看迭代器。
`QList<T>` 顺序性容器是一个“数组列表”，它在单个类中结合了 `QVector<T>` 和 `QLinkedList<T>` 的大部分优点。它支持随机访问，接口像 `QVector` 一样基于索引。在 `QList<T>` 的两端插入或删除项非常快，对于最多约一千个项的列表，在中间插入也是快的。除非我们想在巨大的列表中间进行插入，或者需要列表的项在内存中占据连续地址，否则 `QList<T>` 通常是最适合使用的通用容器类。

`QStringList` 是 `QList<QString>` 的子类，在 Qt API 中被广泛使用。除了从基类继承的功能外，它还提供了一些额外功能，使得该类处理字符串时更加通用。我们将在章的最后一节讨论 `QStringList`（第 290 页）。

`QStack<T>` 和 `QQueue<T>` 是两个便利子类的示例。`QStack<T>` 提供了 `push()`、`pop()`、`top()`。`QQueue<T>` 提供了 `enqueue()`、`dequeue()`、`head()`。

对于目前为止的所有容器，值类型 `T` 可以基本类型（如 `int` 或 `double`）、指针，或者具有默认构造函数（不带参数的构造函数）、拷贝构造函数和赋值运算符的类。符合条件的类包括 `ByteArray`、`QDateTime`、`QRegExp`、`QString`，而派自 `QObject` 的类不符合条件，因为它们缺乏拷贝构造函数和赋值运算符。

