
```csharp
// 实际实现中此处替换

return oldValue;

}

}

chain.Add(new KeyValuePair<K, V>(key, value));

size++;

if (size >= threshold) {

    Expand();

}

}

return default;

}

/// <summary>获取或设置由指定键标识的
/// 字典条目的值</summary>
/// <remarks>如果为当前不在字典中的键设置了值，
/// 将创建一个新条目</remarks>
/// <returns>由提供的键标识的字典中条目的的值</returns>
V this[K key] { 
    get {
        return Get(key);
    }
    set {
        Set(key, value);
    }
}

/// <summary>删除字典中由指定键标识的
/// 元素</summary>
/// <returns>元素是否被删除的布尔值</returns>
public bool Remove(K key)
{
    List<KeyValuePair<K, V>> chain = FindChain(key, false);
    if (chain != null) {
        for (int i = 0; i < chain.Count; i++) {
            if (chain[i].Key.Equals(key)) {
                chain.RemoveAt(i);
                size--;
                return true;
            }
        }
    }
    return false;
}

/// <summary>返回字典中条目的数量
/// </summary>
public int Count {
    get {
        return size;
    }
}

/// <summary>从字典删除所有元素
/// </summary>
public void Clear() {
    this.table = new List<KeyValuePair<K, V>>[initialCapacity];
    size = 0;
}

/// <summary>扩展底层哈希表。创建一个大 2 倍的表并将旧元素传输到其中。
/// 这是一个缓慢的（线性）操作</summary>
private void Expand() {
    int newCapacity = 2 * this.table.Length;
    List<KeyValuePair<K, V>>[] oldTable = this.table;
    this.table = new List<KeyValuePair<K, V>>[newCapacity];
    threshold = (int)(newCapacity * DEFAULT_LOAD_FACTOR);
    for (int i = 0; i < oldTable.Length; i++) {
        if (oldTable[i] != null) {
            foreach (KeyValuePair<K, V> entry in oldTable[i]) {
                int index = entry.Key.GetHashCode();
                index = index & 0xFFFFFF;
                index = index % this.table.Length;
                if (this.table[index] == null) {
                    this.table[index] = new List<KeyValuePair<K, V>>();
                }
                this.table[index].Add(entry);
            }
        }
    }
}
```

```csharp
this.threshold = (int)(newCapacity * this.loadFactor);
foreach (List<KeyValuePair<K, V>> oldChain)
{
    if (oldChain != null)
    {
        foreach (KeyValuePair<K, V> keyValuePair in oldChain)
        {
            List<KeyValuePair<K, V>> chain = FindChain(keyValuePair.Key, true);
            chain.Add(keyValuePair);
        }
    }
}
```

```csharp
// <summary>实现了 IEnumerable<KeyValuePair<K, V>> 以允许在 foreach 循环中遍历哈希表
// 表中的键值值对</summary>
IEnumerator<KeyValuePair<K, V>> IEnumerable<KeyValuePair<K, V>>.GetEnumerator()
{
    foreach (KeyValuePair<K, V> chain in this.table)
    {
        if (chain != null)
        {
            foreach (KeyValuePair<K, V> entry in chain)
            {
                yield return entry;
            }
        }
    }
}
```

```csharp
// <summary>实现了 IEnumerable (非泛型)
// 作为 IEnumerable<KeyValuePair<K, V>> 的部分</summary>
IEnumerator IEnumerable.GetEnumerator()
{
    return ((IEnumerable<KeyValuePair<K, V>>)this).GetEnumerator();
}
```

我们将关注这段代码中最重要的点。让我们从构造函数开始。内部的公共无参数构造函数本身会调用另一个构造函数，传递一些容量和负载因子的预定义值，这些值在创建哈希表时会被使用。

接下来，我们关注的是使用链链法的哈希表的实际实现。在实例化哈希表时，在构造函数内部我们初始化了一个列表数组，它将包含我们的任何类型为 `KeyValuePair<K,V>` 的对象。我们创建了一个私有方法 `FindChain()` 用于内部使用，它通过调用 `GetHashCode()` 方法计算键的哈希码，并寻找哈希值对索引长度的模，以确保结果始终为正数。通过这种方式，计算出当前键在内部表中的索引。所有具有相同哈希值的元素的列表都存储在内部表的该索引处。如果列表为空，则我们的值为 `null`。否则，在特定的索引位置上有一个指定键的元素列表。

一个特殊的参数被传递给 `FindChain()` 方法。该参数指示如果为特定键没有元素列表，是否创建一个空列表。它为添加元素和调整哈希表大小的方法提供了一种便利性。

我们关注的下一个点是 `Expand()` 方法，它在达到最大填充率时调整当前表的大小。为了这个目的，我们创建了一个新表（数组），其大小是当前表的两倍。然后我们计算一个新的最大填充值（填充阈值）。接下来是最关键的部分。我们已经扩展了表，并以这种方式改变了 `this.table.Length` 的值。如果我们搜索一个已经添加的元素，`FindChain(K key)` 方法将完全不会返回用于搜索它的链。这就是为什么我们需要转移旧表中的所有元素，但不是复制链，而是将所有的 `KeyValuePair<K,V>` 对象添加到新创建的内部链之链中。

为了实现在 `foreach` 循环对哈希表元素进行迭代的能力，我们实现了 `IEnumerable<KeyValuePair<K,V>>` 接口，该接口有一个 `GetEnumerator()` 方法，返回一个指向哈希表元素的 `IEnumerator`。我们简单地遍历内部表中的元素，并使用 C# 关键字 `yield return` 一次返回一个（这是一个复杂的概念，在 MSDN 中有详细解释）。

现在让我们通过例子说明我们如何使用我们的哈希表实现及其迭代器。我们想测试哈希表是否能正确处理冲突和扩容，因此在创建哈希表时特意地将初始容量设为 3，负载因子设为 0.9，以确保在放入几个元素后它很快就会调整大小。我们首先放入一个元素，然后读取它，添加一个引起冲突的元素，然后读取它，再读取第一个元素，添加一个导致哈希表扩展其内部数组的元素，等等。代码如下，强烈建议通过 Visual Studio 调试器进行跟踪，并在每一步检查哈希表的内部状态是如何变化的：

```csharp
class PlayWithHashDictionary {
    static void Main() {
        Dictionary<Point3D, int> dict =
            new Dictionary<Point3D, int>(3, 0.9f);
        dict[new Point3D(1, 2, 3)] = 1; // 放入一个键值对
        Console.WriteLine(dict[new Point3D(1, 2, 3)]); // 获取值
        // 覆盖相同键的先前值
        dict[new Point3D(1, 2, 3)] += 1;
        Console.WriteLine(dict[new Point3D(1, 2, 3)]);
        // 现在此点将与上一个产生冲突
        // 元素将成链
        dict[new Point3D(3, 2, 2)] = 42;
        Console.WriteLine(dict[new Point3D(3, 2, 2)]);
        // 测试链法是否按预期工作，即
        // 具有相同哈希值的元素不会被覆盖
        Console.WriteLine(dict[new Point3D(1, 2, 3)]);
        // 按键删除现有项
        dict.Remove(new Point3D(3, 2, 2));
        // 遍历字典并打印
        foreach (KeyValuePair<Point3D, int> entry in dict) {
            Console.WriteLine("Key: " + entry.Key + "; " + entry.Value);
        }
    }
}
```

第 18 章 字典、哈希表和集合 757

正如我们预期的，程序的输出如下：

| Key | Value |
| :--- | :--- |
| (1, 2, 3) | 1 |
| (1, 2, 3) | 2 |
| (3, 2, 2) | 42 |
| (1, 2, 3) | 2 |
| (4, 5, 6) | 1111 |

758 计算机程序基础

# 开放寻址

现在让我们来看看：

## 线性探测

线性探测是一种开放寻址的方法，当冲突发生时，我们检查下一个空槽。

```csharp
int newPosition = (oldPosition + i) % capacity;
```

线性探测的优点是实现简单。缺点是它会导致主聚集，即许多被占用槽聚集在一起。

## 二次探测

二次探测是一种开放寻址的方法，当冲突发生时，我们使用二次函数检查下一个槽。

```csharp
int newPosition = (oldPosition + i * i + i * i) % capacity;
```

二次探测的优点是减少了主聚集。然而，它会导致次聚集，即具有相同初始哈值的键遵循相同的探测序列。

## 双哈希

双哈希是通过两个不同的哈希函数来确定探测序列的开放寻址方法。双哈希的优点是它避免了主聚集和次聚集。

```csharp
int newPosition = (oldPosition + i * hash2(key)) % capacity;
```
