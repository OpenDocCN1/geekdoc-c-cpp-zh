
## 动手试一试

### 派生自定义集合

若要派生一个具体的（封闭的）整数集合，请遵循以下步骤。如果你已关闭 Visual Studio，请先重复上次的练习。

1. 添加一个名为 Int32Collection 的新类，该类派生自 Collection<int> 并重写 InsertItem 方法。重写的 InsertItem 方法的主体应如下所示：

```csharp
protected override void InsertItem(int index, int item)
{
    Console.WriteLine("Inserting item {0} at position {1}", item, index);
    base.InsertItem(index, item);
}
```

2. 将 list 的声明类型从 Collection<int> 更改为 Int32Collection。

3. 使用 Ctrl+F5 运行应用程序，观察输出与图 9.6 中所示内容一致。如果你向上滚动控制台窗口，应该能看到重写的 InsertItem 方法的输出，如 图 9.7 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_228_0.png)

与 Collection<T> 相关的是 ReadOnlyCollection<T>，它可以立即像使用 Collection<T> 一样使用，也可以用于创建你自己的只读集合。也可以从 List<T> 的实例创建只读集合。最常用成员如表 9.5 所示。

### 表 9.5 ReadOnlyCollection<T> 的常用成员

| 名称 | 描述 |
|---|---|
| Count | 获取集合中实际包含的元素数量 |
| Contains | 确定某元素是否在集合中 |
| IndexOf | 搜索指定元素并返回第一次出现的索引 |

**ReadOnlyCollection<T>**

你可以将 ReadOnlyCollection<T> 视为围绕现有可变集合的包装器，如果试图更改它，它会抛出异常。底层集合仍然是可变的。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_229_0.png)

## 字典

List<T> 和 Collection<T> 对于通用集合非常有用，但有时需要一个集合，它可以在一组键和一组值之间提供映射，且不允许重复的键。

Dictionary<TKey, TValue> 类提供这种映射，并允许使用键而不是数字索引进行访问。要向 Dictionary<TKey, TValue> 实例添加元素，必须提供键和值。键必须是唯一的且不能为 null，但如果 TValue 是引用类型，值可以为 null。Dictionary<TKey, TValue> 类的常用成员如表 9.6 所示。

### 表 9.6 Dictionary<TKey, TValue> 的常用成员

| 名称 | 描述 |
|---|---|
| Count | 获取字典中包含的键/值对的数量 |
| Keys | 获取包含字典中键的集合 |
| Values | 获取包含字典中值的集合 |
| Add | 将指定的键和值添加到字典中 |
| Clear | 从字典中移除所有键和值 |
| ContainsKey | 确定字典是否包含指定的键 |
| ContainsValue | 确定字典是否包含特定的值 |
| Remove | 从字典中移除具有指定键的值 |

与 List<T> 和 Collection<T> 不同，当枚举字典的元素时，字典返回表示键及其关联值的 KeyValuePair<TKey, TValue> 结构。因此，在使用 foreach 语句遍历字典元素时，var 关键字非常有用。

通常，字典不会为其包含的元素提供排序，这些元素在枚举期间按任意顺序返回。虽然 List<T> 提供 Sort 方法来对列表元素进行排序，但字典不提供。如果你需要一个在添加或删除元素时保持排序的集合，实际上你有两种选择：SortedList<TKey, TValue> 或 SortedDictionary<TKey, TValue>。这两个类很相似，在检索元素时提供相同的性能，但在内存使用和元素插入/删除性能方面有所不同：

- SortedList<TKey, TValue> 使用更少的内存。
- SortedDictionary<TKey, TValue> 对未排序数据提供更快的插入和删除速度。
- SortedList<TKey, TValue> 在从已排序数据一次性填充列表时更快。
- SortedList<TKey, TValue> 在通过索引检索键和值时更高效。

SortedList<TKey, TValue> 和 SortedDictionary<TKey, TValue> 的常用成员如表 9.7 所示。

### 表 9.7 SortedList 和 SortedDictionary 的常用成员

| 名称 | 描述 |
| :--- | :--- |
| Capacity | (仅在 SortedList<TKey, TValue> 中可用。) 获取或设置列表可包含的元素数量。 |
| Count | 获取列表中键/值对的数量。 |
| Add | 将指定的键和值添加到列表中。 |
| Clear | 从列表中移除所有键和值。 |
| ContainsKey | 确定列表是否包含指定的键。 |
| ContainsValue | 确定列表是否包含特定的值。 |
| Remove | 从列表中移除具有指定键的值。 |
| TrimExcess | 如果存储的元素实际数量少于当前容量的 90%，则将容量设置为该数量。 |
| TryGetValue | 获取与指定键关联的值。 |

## 动手试一试

### 使用字典

若要使用 Dictionary<TKey, TValue> 和 SortedDictionary<TKey, TValue> 通过任意键存储和检索数据，请遵循以下步骤。

1. 创建一个新的控制台应用程序。

2. 在 Program.cs 文件的 Main 方法中，声明一个名为 dictionary 的新 Dictionary<string, double>。

3. 添加以下行以初始化字典：

```csharp
dictionary.Add("Speed Of Light", 2.997924580e+8F);
dictionary.Add("Gravitational Constant", 6.67428e-11F);
dictionary.Add("Planck’s Constant", 6.62606896e-34F);
dictionary.Add("Atomic Mass Constant", 1.660538782e-27F);
dictionary.Add("Avogadro’s number", 6.02214179e+23F);
dictionary.Add("Faraday Constant", 9.64853399e+4F);
dictionary.Add("Electron Volt", 1.602176487e-19F);
```

4. 编写一个 foreach 语句，打印键的名称及其关联的值。你可以使用 var 或 KeyValuePair<string, double> 作为迭代变量的类型。

5. 使用 Ctrl+F5 运行应用程序，观察输出与图 9.8 中所示内容一致。注意，输出按照值在字典中的输入顺序显示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_231_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_231_1.png)

6. 将 `dictionary` 的声明更改为 `SortedDictionary<string, Double>`。

7. 使用 Ctrl+F5 运行应用程序，观察输出与图 9.9 中所示内容一致。注意，仅通过更改声明，输出就按键的字母顺序排序显示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_232_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_232_1.png)

## 集合（Set）

在数学中，集合是一个不包含重复元素的集合，这些元素以随机顺序存储和访问。除了标准的插入和删除操作外，集合还支持超集、子集、交集和并集操作。

.NET 中的集合可通过 `HashSet<T>` 和 `SortedSet<T>` 类提供。`HashSet<T>` 等同于数学集合，而 `SortedSet<T>` 在插入和删除元素时维护排序顺序，且不影响性能。这两个类都不允许重复元素。这些类共享几乎相同的公共接口，如表 9.8 所示。

### 表 9.8 HashSet<T> 和 SortedSet<T> 的常用成员

| 名称 | 描述 |
| :--- | :--- |
| Count | 获取集合中包含的元素数量。 |
| Max | 获取集合中的最大值。(仅适用于 SortedSet<T>。) |
| Min | 获取集合中的最小值。(仅适用于 SortedSet<T>。) |
| Add | 将指定元素添加到集合中。 |
| Clear | 从集合中移除所有元素。 |
| Contains | 确定集合是否包含指定元素。 |
| ExceptWith | 从集合中移除指定集合中的所有元素。 |
| IntersectWith | 修改当前集合，使其仅包含在集合和指定集合中都存在的元素。 |

