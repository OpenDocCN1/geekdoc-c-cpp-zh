

```csharp
{
    // Create the writer
    using (BinaryWriter wr = new BinaryWriter(fs))
    {
        // Write data to Fifth.txt
        for (int cnt = 1; cnt < 15; cnt++)
        {
            wr.Write(cnt);
        }
    }
}
// Create the reader
using (FileStream fs = new FileStream(FILE_NAME, FileMode.Open, FileAccess.Read))
{
    using (BinaryReader rb = new BinaryReader(fs))
    {
        // Read data from Fifth.txt
        for (int cnt = 1; cnt < 20; cnt++)
        {
            Console.WriteLine(rb.ReadInt32());
        }
    }
}
}
```

## 11.2.4 从控制台读取和写入

- 1. 为了允许在监视器屏幕上显示内容，.NET Framework 提供了一个名为 **Console** 的类。**Console** 类定义在 **System** 命名空间中。
- 2. **System** 命名空间是 **mscorlib.dll** 库的一部分。当创建 C# 应用程序时，**mscorlib.dll** 库可直接使用；这意味着无需直接导入。
- 3. **Console** 类是静态的。这意味着可以直接使用它，而无需声明它的变量。
- 4. **Console.Write()** 方法用于在屏幕上显示内容，**Console** 类提供 **Read()** 方法以从用户处获取值。
- 5. 要使用它，可以将变量名称赋值给它。使用的语法是：

```csharp
VariableName = Console.Read();
```

这仅仅意味着，当用户输入内容并按回车键时，用户输入的内容将被*赋值*给赋值运算符左侧指定的变量。

## 两分题及答案

### 问：C# 中的 I/O 类有哪些？请列举一些最常用的类。

答：C# 中的 System.IO 命名空间包含多个用于执行各种文件操作的类，例如创建、删除、关闭和打开。C# 中一些最常用的 I/O 类是：

- File - 操作文件
- Path - 执行与路径信息相关的操作
- StreamReader - 从流中读取字符
- StreamWriter - 向流中写入字符
- StringReader - 读取字符串缓冲区
- StringWriter - 写入字符串缓冲区

### 问：什么是 StreamReader/StreamWriter 类？

答：StreamReader 和 StreamWriter 是 System.IO 命名空间中的类。当我们需要读取或写入基于字符（Reader）的数据时，分别使用它们。

StreamReader 的一些成员包括：Close()、Read()、ReadLine()。
StreamWriter 的成员包括：Close()、Write()、WriteLine()。

### 问：在 C#.NET 中，哪个类提供从控制台读取和写入的操作？

答：在 C#.NET 中，读写控制台的方法由 System.Console 类提供。该类允许我们访问标准输入、标准输出和标准错误流。

### 问：当 Read() 从控制台读取时产生错误条件，会返回什么？

答：Read() 在出错时返回 -1。该方法在失败时还会抛出 IOException。

### 问：使用文件操作有哪些优点和缺点？

答：文件的主要优点是它们是持久的，并且随时可供应用程序使用；缺点是如果多个用户访问同一个文件，会降低应用程序的性能。

### 问：文件操作中的流是什么？

答：流是字节序列，通过通信路径从源传输到目的地。

### 问：Dispose() 和 Flush() 有什么区别？

答：Dispose() 用于释放当前实例使用的所有资源，而 Flush() 用于清除当前流的所有缓冲区。

### 问：BinaryWriter 和 BinaryReader 类有什么用途？

答：BinaryWriter 类负责将原始数据类型以二进制形式写入流，BinaryReader 类负责将原始数据类型作为二进制值读取。

### 问：Peek() 和 Seek() 有什么区别？

答：Peek() 用于返回下一个可用字符，但不消耗它；而 Seek() 用于设置当前流中的位置。

## 长答题

- 问：讨论 C# 中的 IO 流类。（参考 11.2 节）
- 问：在 C# 中，哪些类可用于方便地读写文件？（参考 11.2 节）
- 问：如何从控制台读取和写入数据？（参考 11.2 节）
- 问：如何处理二进制数据？（参考 11.2 节）
- 问：打开文件时使用哪些文件模式？（参考 11.1 节）

## 第二单元

## 第 12 章

## C# 高级特性 III - 集合

大纲：集合。

| 节号 | 主题名称 | 页码 |
|---|---|---|
| 12.1 | 集合 | 12 - 2 |
| 12.2 | C# 中的不同集合类 | 12 - 2 |
| 12.3 | 使用集合 | 12 - 3 |
| 12.4 | ArrayList 类 | 12 - 5 |
| 12.5 | Hashtable 类 | 12 - 8 |
| 12.6 | SortedList 类 | 12 - 10 |
| 12.7 | Stack 类 | 12 - 12 |
| 12.8 | Queue 类 | 12 - 14 |
| 12.9 | BitArray 类 | 12 - 16 |
|  | 两分题及答案 | 12 - 19 |
|  | 长答题 | 12 - 19 |

## 12.1 集合

### 概念

- 1. 集合（collection）是一个组，也称为列表，是将许多同类项组合成一个实体。

### 说明

- 2. 集合可以基于任何数据类型的项，如简单的数字、基本符号、日期、字符串、时间等。
- 3. 集合可以是对象的集合，每个对象由自身的内部值组成。
- 4. 基本规则是，集合中包含的所有项都必须使用相同的特征来描述。

## 12.2 C# 中的不同集合类

常用的集合类位于 System.Collections 命名空间中。

| 类 | 描述 |
|---|---|
| ArrayList | 表示可以单独索引的对象的排序集合。它是数组的替代品。但与数组不同，可以使用索引在指定位置添加和删除列表中的项，并且数组会自动调整大小。此外，它还允许动态内存分配、添加、搜索和排序列表中的项。它使用键来访问集合中的元素。 |
| Hashtable | 当需要通过键访问元素并识别有用的键值时，使用哈希表。哈希表中的每个项都有一个键/值对。键用于访问集合中的项。键和索引都用于访问列表中的项。 |
| SortedList | 有序列表是数组和哈希表的组合。它包含一个项列表，可以使用键或索引访问这些项。如果使用索引访问，它是 ArrayList；如果使用键访问，它是 Hashtable。项集合始终按键值排序。 |

```csharp
// This represents the number of items in the collection
public int Count
{
    get { return this.size; }
}

public class Demo
{
    static int Main(string[] args)
    {
        var list = new Collection();

        Console.WriteLine("Number of Items: {0}", list.Count);
        return 0;
    }
}
```

**输入**

无

### 输出

Number of Items: 0

## 12.4 ArrayList 类

### ArrayList 类的属性

| 属性 | 描述 |
|---|---|
| Capacity | 获取或设置 ArrayList 可以包含的元素数。 |
| Count | 获取 ArrayList 中实际包含的元素数。 |
| IsFixedSize | 获取一个值，该值指示 ArrayList 是否具有固定大小。 |
| IsReadOnly | 获取一个值，该值指示 ArrayList 是否为只读。 |
| Item | 获取或设置指定索引处的元素。 |

### ArrayList 类的方法

| 序号 | 方法 |
|---|---|
| 1 | **public virtual int Add(object value);**<br>将对象添加到 ArrayList 的末尾。 |
| 2 | **public virtual void AddRange(ICollection c);**<br>将 ICollection 的元素添加到 ArrayList 的末尾。 |
| 3 | **public virtual void Clear();**<br>从 ArrayList 中移除所有元素。 |
| 4 | **public virtual bool Contains(object item);**<br>确定某个元素是否在 ArrayList 中。 |
| 5 | **public virtual ArrayList GetRange(int index, int count);**<br>返回一个 ArrayList，它表示源 ArrayList 中元素的子集。 |
| 6 | **public virtual int IndexOf(object);**<br>返回 ArrayList 或其一部分中某个值第一次出现的从零开始的索引。 |
| 7 | **public virtual void Insert(int index, object value);**<br>在指定索引处将元素插入 ArrayList。 |
| 8 | **public virtual void InsertRange(int index, ICollection c);**<br>在指定索引处将集合的元素插入 ArrayList。 |
| 9 | **public virtual void Remove(object obj);**<br>从 ArrayList 中移除特定对象的第一个匹配项。 |
| 10 | **public virtual void RemoveAt(int index);**<br>移除 ArrayList 中指定索引处的元素。 |
| 11 | **public virtual void RemoveRange(int index, int count);**<br>从 ArrayList 中移除一定范围的元素。 |
| 12 | **public virtual void Reverse();**<br>反转 ArrayList 中元素的顺序。 |
| 13 | **public virtual void SetRange(int index, ICollection c);**<br>将集合的元素复制到 ArrayList 中的一定范围的元素上。 |
| 14 | **public virtual void Sort();**<br>对 ArrayList 中的元素进行排序。 |
| 15 | **public virtual void TrimToSize();**<br>将容量设置为 ArrayList 中实际元素的数量。 |

