
# IList\<T> Members

```csharp
// 添加一个 IndexOf 方法，返回集合中项
// 第一次出现的索引。
public int IndexOf(T item)
{
    return items.IndexOf(item);
}
```

```csharp
// 添加一个 Insert 方法，在指定的索引
// 处向集合中添加项。
public void Insert(int index, T item)
{
    items.Insert(index, item);
}
```

```csharp
// 添加一个 RemoveAt 方法，从指定的索引
// 处从集合中删除项。
public void RemoveAt(int index)
{
    items.RemoveAt(index);
}
```

```csharp
// 添加一个索引器，允许根据指定的索引
// 对集合中的项进行读/写访问。
public T this[int index]
{
    get
    {
        return items[index];
    }
    set
    {
        items[index] = value;
    }
}
```

## 问题

你开发了一个应用程序，以自定义格式将数据存储在文件中。文件结构是预定义的，并使用与 XML 相似但并不相同的结构。存储在文件中的数据按指定顺序存储，应用程序需要同时对文件进行读取和写入。你如何使用自定义集合类来使应用程序中使用数据文件变得更容易？

## 实现 Dictionary 类

```csharp
class IntelligentDictionary<TKey, TValue> : IDictionary<TKey, TValue>
{
    public IntelligentDictionary()
    {
    }

    public void Add(TKey key, TValue value)
    {
    }

    public bool ContainsKey(TKey key)
    {
    }

    public ICollection<TKey> Keys
    {
        get { }
    }

    public bool Remove(TKey key)
    {
    }

    public bool TryGetValue(TKey key, out TValue value)
    {
    }

    public ICollection<TValue> Values
    {
        get { }
    }

    public TValue this[TKey key]
    {
        get { }
        set { }
    }

    public void Add(KeyValuePair<TKey, TValue> item)
    {
    }

    public void Clear()
    {
    }

    public bool Contains(KeyValuePair<TKey, TValue> item)
    {
    }

    public void CopyTo(KeyValuePair<TKey, TValue>[] array, int arrayIndex)
    {
    }

    public int Count { get; }

    public bool IsReadOnly { get; }

    public bool Remove(KeyValuePair<TKey, TValue> item)
    {
    }

    public IEnumerator<KeyValuePair<TKey, TValue>> GetEnumerator()
    {
    }

    public IEnumerator GetEnumerator()
    {
        return Inumerable.GetEnumerator();
    }
}
```

## 关键点

你实现字典集合类的方式与实现一个简单的集合类几乎相同——区别在于你应该实现 `IDictionary<TKey, TValue>` 而不是 `IList<T>` 接口。`IDictionary<TKey, TValue>` 继承自 `ICollection<T>` 接口，因此你也必须实现该接口。

下面的代码示例显示了一个使用 `Dictionary` 对象作为内部数据存储的字典集合类。

# 构建和枚举类

```csharp
class IntelligentDictionary<TKey, TValue> : IDictionary<TKey, TValue>
{
    // 定义一个 Dictionary<TKey, TValue> 对象，用于存储
    // 添加集合中的项。
    Dictionary<TKey, TValue> items;

    // 定义该类的构造函数。
    public IntelligentDictionary()
    {
        items = new Dictionary<TKey, TValue>();
    }

    // 定义一个将指定的键和值
    // 添加集合的 Add 方法。
    public void Add(TKey key, TValue value)
    {
        // 实现细节未显示
        ...
    }

    #region IDictionary<TKey, TValue> Members

    // 定义一个 ContainsKey 方法，返回集合包含
    // 特定键。
    public bool ContainsKey(TKey key)
    {
        return items.ContainsKey(key);
    }

    // 定义一个 Keys 属性，返回存储在集合
    // 中的键。
    public ICollection<TKey> Keys
    {
        get { return items.Keys; }
    }

    // 定义一个 Remove 方法，从集合中删除指定的
    // 键，并返回指示方法是否成功的。
    public bool Remove(TKey key)
    {
        return items.Remove(key);
    }

    #endregion
}
```

```csharp
// 定义一个 TryGetValue 方法，返回一个 bool 值
// 以指示方法是否成功，如果成功，则将
// 输出参数设置为与指定键对应的值。
public bool TryGetValue(TKey key, out TValue value)
{
    return items.TryGetValue(key, out value);
}
```

```csharp
// 定义一个 Values 属性，返回存储在
// 集合中的值的 ICollection 对象。
public ICollection<TValue> Values
{
    get { return items.Values; }
}
```

```csharp
// 定义一个索引器，根据指定的键
// 对集合中的项进行读/写值访问。
public TValue this[TKey key]
{
    get
    {
        return items[key];
    }
    set
    {
        items[key] = value;
    }
}
```

```csharp
#endregion

#region ICollection<KeyValuePair<TKey, TValue>> Members

// 重载 Add 方法以实现
// ICollection<T> 接口。使用 KeyValuePair<TKey, TValue> 
// 泛型类型作为类型参数。
public void Add(KeyValuePair<TKey, TValue> item)
{
    // 调用已定义的 Add 方法，使用
    // item 参数的属性作为 Add 方法的参数。
    Add(item.Key, item.Value);
}
```

```csharp
// 定义一个 Clear 方法，从集合中删除
// 所有项。
public void Clear()
{
    items.Clear();
}
```

```csharp
// 定义 Contains 方法的重载以实现
// ICollection<T> 接口。使用泛型类型 KeyValuePair<TKey, TValue>
// 作为类型参数。
public bool Contains(KeyValuePair<TKey, TValue> item)
{
    return ((ICollection<KeyValuePair<TKey, TValue>>)items).Contains(item);
}
```

```csharp
// 定义一个 CopyTo 方法，将集合中的项
// 复制到作为参数传递的数组。该数组
// 是一维的，存储 KeyValuePair<TKey, TValue> 类型的实例，而不是 TKey 或
// 集合的实例。
public void CopyTo(KeyValuePair<TKey, TValue>[] array, int arrayIndex)
{
    ((ICollection<KeyValuePair<TKey, TValue>>)items).CopyTo(array, arrayIndex);
}
```

```csharp
// 定义一个 Count 属性，返回集合中
// 项的数量。
public int Count
{
    get { return items.Count; }
}
```

```csharp
// 定义一个 IsReadOnly 属性，返回一个布尔值
// 表示集合是否为只读。
public bool IsReadOnly
{
    get { return false; }
}
```

```csharp
// 添加一个 Remove 方法，根据作为参数传递的
// KeyValuePair<TKey, TValue> 对象从集合中删除一个项。
public bool Remove(KeyValuePair<TKey, TValue> item)
{
    return items.Remove(item.Key);
}
```

```csharp
#endregion

#region IEnumerable<KeyValuePair<TKey, TValue>> Members

// 定义一个 GetEnumerator 方法，返回一个
// IEnumerable<KeyValuePair<TKey, TValue>> 对象。
public IEnumerator<KeyValuePair<TKey, TValue>> GetEnumerator()
{
    // 迭代器将在下节课中讨论。
    throw new NotImplementedException();
}

#endregion

#region IEnumerable Members

// 添加一个 GetEnumerator 方法以实现
// 非泛型的 IEnumerable.GetEnumerator()
IEnumerator IEnumerable.GetEnumerator()
{
    // 这应该始终返回调用泛型
    // GetEnumerator 方法的结果。
    return GetEnumerator();
}

#endregion
```

## 问题

你开发了一个字典集合类并实现了 `IDictionary<TKey, TValue>` 接口。你必须使用底层的 `Dictionary<TKey, TValue>` 类作为内部数据存储。当你实现接口要求的 `CopyTo` 方法时，你发现泛型字典类没有暴露公开的 `CopyTo` 方法。泛型字典类显式地实现了接口定义的 `CopyTo` 方法。显式实现接口可以避免在通过 `Dictionary<TKey, TValue>` 类型引用集合时暴露 `CopyTo` 方法。在你开发的集合中，你会在什么情况下使用这种方法？

# 第 2 节：在自定义集合类中添加迭代器

- 什么是迭代器？
- 什么是 `IEnumerable<T>` 接口？
- 什么是 `IEnumerator<T>` 接口？
- 手动实现迭代器
- 使用迭代器实现迭代器

C# 提供了 `foreach` 语句来允许你遍历集合的内容。`foreach` 语句为集合生成一个迭代器，该迭代器提供了依次从集合中获取每个项的方法。当你定义自定义集合类时，你必须提供一种 `foreach` 语句可以用来生成此迭代器的机制。

本节将向你介绍迭代器，并解释如何在自定义集合类中实现迭代器。

## 目标

完成本节后，你将能够：

- 解释迭代器的用途。
- 描述 `IEnumerable<T>` 接口。
- 描述 `IEnumerator<T>` 接口。
- 手动实现迭代器。
- 使用迭代器实现迭代器。

## 什么是迭代器？

![](img/3ef84844c6ac82b838cfffa6448b2346_286_0.png)

### 关键点

迭代器是一种类型，它提供一个方法，该方法以适用于集合的顺序返回集合中的每个项。对于某些集合，顺序并不重要。例如，对于 `List` 类，项添加到列表类中的顺序决定了它们的顺序。在其他集合类中，顺序更为重要。例如，在 `SortedList` 类中，项是根据项添加到集合时指定的键按升序返回的。

你可以将迭代器认为是指向集合中项的指针。当你实例化迭代器时，可以初始化它以指向集合中的第一个项。你可以通过此引用检索集合中找到的值，然后可以移动指针按顺序引用下一个项。

当你在应用程序中使用 `foreach` 语句时，`foreach` 语句将使用由你的类生成的迭代器来从集合中检索每个项。你可以实现迭代器，以最适合你集合类的顺序从你的集合类中返回项。

迭代器提供了对集合的单向只读访问。你可能希望允许应用程序以多种顺序遍历你集合类中的项。例如，你可能希望支持正向和反向遍历。当应用程序使用 `foreach` 语句时，它会自动使用你集合的默认迭代器。但是，你可以在你的类型中定义多个迭代器。

**问题：** 迭代器提供了对集合的单向只读访问。你可能希望允许应用程序以多种顺序遍历你集合类中的项。例如，你可能希望支持正向和反向遍历。当应用程序使用 `foreach` 语句时，它会自动使用你集合的默认迭代器。但是，你可以在你的类型中定义多个迭代器。

**问题：** 迭代器提供了对集合的单向只读访问。为什么通过迭代器允许写入访问是不合适的？

## 什么是 IEnumerable\<T> 接口？

| IEnumerable\<T> | CustomCollectionClass\<T> |
| :--- | :--- |
| 接口用于支持枚举的类。 | : IEnumerable\<T> |
| IEnumerable\<T> 接口定义了 GetEnumerator 方法。 | IEnumerator\<T> GetEnumerator() |

### 关键点

支持枚举的类必须实现 `IEnumerable<T>` 接口。`IEnumerable<T>` 接口定义了 `GetEnumerator` 方法。`GetEnumerator` 方法返回 `foreach` 语句要求的 `IEnumerator` 对象。

当你实现 `IEnumerable<T>` 接口时，`GetEnumerator` 方法暴露你集合的默认迭代器。你可以在你的类型中定义多个迭代器；但你必须在你的集合类中提供额外的方法或属性，以便调用程序访问这些迭代器。

`IEnumerable<T>` 接口继承自 `IEnumerable` 接口。`IEnumerable` 接口是 `IEnumerable<T>` 接口的非泛型版本，带有其非泛型的 `GetEnumerator` 方法。此接口和方法是为了与不使用泛型的旧应用程序向后兼容。但是，如果你不需要提供这种程度的支持，通常的做法是在接口的 `GetEnumerator` 方法中抛出 `NotImplementedException`，以确保应用程序使用泛型的、安全的 `GetEnumerator` 方法。

除了从你的类型暴露迭代器外，如果你的类型必须支持集合初始化器，你还必须实现 `IEnumerable` 接口。为了支持集合初始化器，你必须在你的类型中实现 `IEnumerable` 接口并定义 `Add` 方法。

下面的代码示例显示了 `IEnumerable<T>` 的实现。该集合类还实现了一个名为 `Backwards` 的方法，该方法生成一个用于反向遍历的迭代器。注意当你实现一个额外的迭代器时，返回的是一个 `IEnumerable<T>` 对象。该对象可以引用相同的数据，但必须实现 `GetEnumerator` 方法以生成按相应顺序返回数据的迭代器。

以下代码示例显示了你如何使用默认枚举器和反向（Backwards）枚举器。

```csharp
// CustomCollectionClass 类实现了 IEnumerable<T> 
// 接口。
```
