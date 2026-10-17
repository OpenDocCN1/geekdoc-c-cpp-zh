
| `IsSynchronized` | Retrieves a value specifying whether or not the access to the `ArrayList` object is synchronized |

| `Item` | Retrieves or sets the element at the specified index |

| `SyncRoot` | Retrieves an object that can be used to synchronize access to the `ArrayList` object |

表 32.2 列出了 `ArrayList` 类的重要方法：

| Method | Description |

|---|---|

| `Add()` | Adds an item at the end of the `ArrayList` object |

| `AddRange()` | Adds the items in an object implementing the `ICollection` interface at the end of the `ArrayList` object |

| `BinarySearch()` | Uses a binary search algorithm to locate a specific item in the sorted `ArrayList` object and returns the index of the item |

| `Clear()` | Removes all the items from the `ArrayList` object |

| `Clone()` | Creates a copy of the `ArrayList` object |

| `Contains()` | Returns true if the specified item is in the `ArrayList` object |

| `CopyTo()` | Copies some or the entire `ArrayList` object into a one-dimensional array |

| `GetRange()` | Returns an `ArrayList` object, which is a subset of the items in the source `ArrayList` object |

| `IndexOf()` | Returns the zero-based index of the first occurrence of a specified item in the `ArrayList` object |

| `Insert()` | Adds an item at a particular index in the `ArrayList` object |

| `InsertRange()` | Adds the items of a collection into the `ArrayList` object at a particular index |

| `LastIndexOf()` | Returns the zero-based index of the last occurrence of a specified item in the `ArrayList` object |

| `Remove()` | Removes the first occurrence of a specified item from the `ArrayList` object |

| `RemoveAt()` | Removes an item from the specified index of the `ArrayList` object |

| `RemoveRange()` | Removes a range of items from the `ArrayList` object |

| `Reverse()` | Reverses the order of the items in the `ArrayList` object |

| `SetRange()` | Copies the items of a collection over a range of items in the `ArrayList` object |

| `Sort()` | Sorts the items in the `ArrayList` object |

| `ToArray()` | Copies the items of the `ArrayList` object to a new array |

| `TrimToSize()` | Sets the capacity (to hold items) of the `ArrayList` object to the actual number of items stored in the `ArrayList` object |

## Hashtable 类

`Hashtable` 类与 `ArrayList` 类类似，但它允许你通过键访问项目。`Hashtable` 对象中的每个项目都有一个键/值对。键用于访问集合中的项目，每个键必须是唯一的；而值是存储在数组中的值。通常，键是短字符串或整数。使用 `Hashtable` 类，你可以向集合添加和检索项目。

**NOTE**  

键不能为空，但值可以为空。

`Hashtable` 类的类层次结构如下所示：

```
System.Object
    System.Collections.Hashtable
```

表 32.3 列出了 `Hashtable` 类的重要属性：

| Property | Description |

|---|---|

| `Count` | Retrieves the number of key/value pairs present in the `Hashtable` object |

| `EqualityComparer` | Retrieves an `EqualityComparer` object to use for the `Hashtable` object, which defines the methods to support the comparison of objects for equality |

| `IsFixedSize` | Retrieves a value specifying whether or not the `Hashtable` object has a fixed size |

| `IsReadOnly` | Retrieves a value specifying whether or not the `Hashtable` object is read-only |

| `IsSynchronized` | Retrieves a value specifying whether or not the access to the `Hashtable` object is synchronized |

| `Item` | Retrieves or sets the value associated with the specified key |

| `Keys` | Retrieves the collection of keys in the `Hashtable` object |

| `SyncRoot` | Retrieves an object that can be used to synchronize access to the `Hashtable` object |

| `Values` | Retrieves the collection of values in the `Hashtable` object |

表 32.4 列出了 `Hashtable` 类的重要方法：

| Method | Description |

|---|---|

| `Add()` | Adds an item with the specified key and value into the `Hashtable` object |

| `Clear()` | Removes all the items from the `Hashtable` object |

| `Clone()` | Creates a copy of the `Hashtable` object |

| `ContainsKey()` | Returns true if the specified key is in the `Hashtable` object |

| `ContainsValue()` | Returns true if the specified value is in the `Hashtable` object |

| `CopyTo()` | Copies the `Hashtable` object items into a one-dimensional array at the specified index |

| `GetEnumerator()` | Returns an `IDictionaryEnumerator` object that iterates through the `Hashtable` object |

| `GetObjectData()` | Implements the `ISerializable` interface and returns the data needed to serialize the `Hashtable` object |

| `OnDeserialization()` | Implements the `ISerializable` interface and raises the deserialization event when the deserialization is complete |

| `Remove()` | Removes an item with the specified key from the `Hashtable` object |

## SortedList 类

`SortedList` 类是 `Array` 和 `Hashtable` 类的组合。它包含一个项目列表，可以通过索引或键访问。当你使用索引访问项目时，`SortedList` 对象充当 `ArrayList` 对象；而当你使用键访问项目时，它充当 `Hashtable` 对象。`SortedList` 类的显著特点是，该集合类始终按键排序。项目中的

`SortedList` 对象始终根据其键的值进行排序，并且没有单独的方法来根据其中存储的值对集合进行排序。

`SortedList` 类的类层次结构如下：

```
System.Object
System.Collections.SortedList
```

### 表 32.5：SortedList 类的著名属性

| 属性 | 描述 |

|---|---|

| `Capacity` | 检索或设置 `SortedList` 对象可以容纳的元素数量 |

| `Count` | 检索 `SortedList` 对象中存在的元素数量 |

| `IsFixedSize` | 检索一个值，指定 `SortedList` 对象是否具有固定大小 |

| `IsReadOnly` | 检索一个值，指定 `SortedList` 对象是否为只读 |

| `IsSynchronized` | 检索一个值，指定对 `SortedList` 对象的访问是否同步 |

| `Item` | 检索或设置 `SortedList` 对象中与特定键关联的值 |

| `Keys` | 检索 `SortedList` 对象中的键集合 |

| `SyncRoot` | 检索一个用于同步访问 `SortedList` 对象的对象 |

| `Values` | 检索 `SortedList` 对象中的值集合 |

表 32.6 列出了 `SortedList` 类的重要方法：

### 表 32.6：SortedList 类的著名方法

| 方法 | 描述 |

|---|---|

| `Add()` | 将具有指定键和值的项添加到 `SortedList` 对象中 |

| `Clear()` | 从 `SortedList` 对象中移除所有项 |

| `Clone()` | 创建 `SortedList` 对象的副本 |

| `Contains()` | 如果指定的项在 `SortedList` 对象中，则返回 true |

| `ContainsKey()` | 如果指定的键在 `SortedList` 对象中，则返回 true |

| `ContainsValue()` | 如果指定的值在 `SortedList` 对象中，则返回 true |

| `CopyTo()` | 将 `SortedList` 对象中的项复制到指定索引处的一维数组中 |

| `GetByIndex()` | 检索 `SortedList` 对象中指定索引处的值 |

| `GetEnumerator()` | 返回遍历 `SortedList` 对象的 `IDictionaryEnumerator` |

| `GetKey()` | 检索 `SortedList` 对象中指定索引处的键 |

| `GetKeyList()` | 从 `SortedList` 对象中检索键列表 |

| `GetValueList()` | 从 `SortedList` 对象中检索值 |

| `IndexOfKey()` | 返回指定键在 `SortedList` 对象中的从零开始的索引 |

| `IndexOfValue()` | 返回指定值在 `SortedList` 对象中首次出现的从零开始的索引 |

| `Remove()` | 从 `SortedList` 对象中移除具有指定键的项 |

| `RemoveAt()` | 移除 `SortedList` 对象中指定索引处的项 |

| `SetByIndex()` | 替换 `SortedList` 对象中指定索引处的值 |

| `TrimToSize()` | 将 `SortedList` 对象的容量（用于容纳项）设置为 `SortedList` 对象中实际存储的项数 |

## Stack 类

`Stack` 类遵循后进先出（LIFO）顺序。最后添加到 `Stack` 对象的项将最先被读取。`Stack` 对象是一个 LIFO 容器。当您向 `Stack` 对象添加项时，称为将项推入（push）`Stack` 对象；当您从 `Stack` 对象移除项时，称为从 `Stack` 对象弹出（pop）该项。这些操作被称为 push 和 pop，因为 push 添加项，而 pop 移除项。

![](img/e073a4882197be4ab61103cbe0bcb394_1518_0.png)

`Stack` 类的类层次结构如下：

```
System.Object
System.Collections.Stack
```

### 表 32.7：Stack 类的著名属性

| 属性 | 描述 |

|---|---|

| `Count` | 检索 `Stack` 对象中存在的元素数量 |

| `IsSynchronized` | 检索一个值，指定对 `Stack` 对象的访问是否同步 |

| `SyncRoot` | 检索一个可用于同步访问 `Stack` 对象的对象 |

### 表 32.8：Stack 类的著名方法

| 方法 | 描述 |

|---|---|

| `Clear()` | 从 `Stack` 对象中移除所有项 |

| `Clone()` | 创建 `Stack` 对象的副本 |

| `Contains()` | 如果项在 `Stack` 对象中，则返回 true |

| `CopyTo()` | 将 `Stack` 对象中的项复制到指定索引处的一维数组中 |

| `GetEnumerator()` | 返回 `Stack` 对象的 `IEnumerator` 对象 |

| `Peek()` | 返回 `Stack` 对象顶部的项，但不将其移除 |

| `Pop()` | 移除并返回 `Stack` 对象顶部的项 |

## BitArray 类

`BitArray` 类用于管理使用值 1 和 0 的二进制表示数组，其中 1 代表 True，0 代表 False。`BitArray` 对象是可调整大小的，这在您事先不知道位数时非常有用。您可以使用整数索引从 `BitArray` 集合类中访问项。此集合中使用的索引从零开始。

`BitArray` 类的类层次结构如下：

```
System.Object
System.Collections.BitArray
```

表 32.11 列出了 `BitArray` 类的重要属性：

### 表 32.11：BitArray 类的著名属性

| 属性 | 描述 |

|---|---|

| `Count` | 检索 `BitArray` 对象中包含的元素数量 |

| `IsReadOnly` | 检索一个值，指定 `BitArray` 对象是否为只读 |

| `IsSynchronized` | 检索一个值，指定对 `BitArray` 对象的访问是否同步 |

| `Item` | 检索或设置 `BitArray` 对象中特定位置处的位值 |

| `Length` | 检索或设置 `BitArray` 对象中的元素数量 |

| `SyncRoot` | 检索一个可用于同步访问 `BitArray` 对象的对象 |

表 32.12 列出了 `BitArray` 类的重要方法：

### 表 32.12：BitArray 类的著名方法

| 方法 | 描述 |

|---|---|

| `And()` | 对当前 `BitArray` 对象中的项与指定 `BitArray` 对象中的对应项执行按位 AND 运算。 |

| `Clone()` | 创建 `BitArray` 对象的副本。 |

| `CopyTo()` | 将 `BitArray` 对象中的项复制到指定索引处的一维数组中。 |

| `Get()` | 检索 `BitArray` 对象中指定索引处的位值。 |

| `GetEnumerator()` | 返回遍历 `BitArray` 对象的枚举器。 |

| `Not()` | 反转当前 `BitArray` 对象中的所有位值，以便设置为 true 的元素变为 false，反之亦然。 |

| `Or()` | 对当前 `BitArray` 对象中的项与指定 `BitArray` 对象中的对应项执行按位 OR 运算。如果一个或两个操作数为 true，则返回 true；如果两个操作数均为 false，则返回 false。 |

| `Set()` | 将 `BitArray` 对象中指定位置的位设置为指定值。 |
