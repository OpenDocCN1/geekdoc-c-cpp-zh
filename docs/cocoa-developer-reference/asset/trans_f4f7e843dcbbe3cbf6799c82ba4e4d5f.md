
数据集合对象可以分组和嵌套。用字典填充数组并不罕见，键值路径也可能变得复杂。绘制类图来展示对象如何链接以及如何解释键值组合，可能非常有用。

## 介绍数据集合对象

Cocoa 的数据集合对象具有许多不寻常的特性：

- **它们实现自己的磁盘访问方法。** 你可以将任何数据对象的内容保存到磁盘并从磁盘加载。还可以将来自 URL 的数据加载到对象中。
- **默认情况下，数据在初始化时定义并且是只读的。** 如果需要更改集合的内容，请使用*可变*子类。
- **数据集合存储对象。** 简单的 C 类型必须被“对象化”。通常这意味着将 int、float 和其他类型转换为 `NSNumber` 的实例，或者使用 `NSValue` 作为其他数据类型的包装器。字符串必须是 `NSString` 的实例。
- **数据集合支持隐式枚举方法。** 你可以用一行代码对集合中的每个对象运行方法。
- **修改可变数据集合不会触发键值观察（KVO）消息，也不会修改集合中某个对象的值。** 如果你想要一个能触发 KVO 响应的集合，需要添加一些变通代码。

表 12.1 介绍了每个对象的关键特性。

**表 12.1  Cocoa 数据对象**

| 数据对象 | 描述 |
|---|---|
| `NSArray` | 在索引列表中存储对象。支持枚举、谓词搜索和排序。 |
| `NSMutableArray` | 支持插入和移除对象。插入一个对象会自动增加其后对象的索引。 |
| `NSDictionary` | 以键值对形式存储对象。支持键和值列表、键枚举、对象枚举和谓词搜索。 |
| `NSMutableDictionary` | 允许插入和删除键值对，并允许修改与某个键关联的对象的值。 |
| `NSSet` | 存储无索引的无序对象集合。当你需要测试某个对象是否在集合中时，`NSSet` 比 `NSArray` 更快。 |
| `NSMutableSet` | 支持插入和删除对象，并支持集合之间的并集、交集和差集运算。 |
| `NSValue` | 通常用作集合中的数据元素。它可作为常规 C 或其他 Objective-C 数据类型的包装器。将其对象化，并提供用于访问、复制和比较它们的标准接口。还支持指针、NSRange，以及图形中使用的 NSPoint、NSRect 和 NSSize 类型。 |
| `NSNumber` | NSNumber 是 NSValue 的子类，用于数值。 |
| `NSIndexSet` | 一组数组索引。用于多个数组操作。NSMutableIndexSet 可以动态修改。 |

## 使用对象、键和值

键值配对是数据集合对象的基本特性。但很容易误解键、对象和值之间的关系。

### 理解对象和值

你可能认为值用于访问对象的内容。如图 12.1 所示，并非如此。

代码创建一个可变字典，并向其中添加各种对象和值。控制台输出显示，`valueForKey:` 和 `objectForKey:` 方法返回同一个对象。

当你使用字符串键时，这两个方法是同义的。对象和值之间的关键差异更加微妙，并且不是直观明显的。

- 当你使用 `valueForKey:` 时，键必须是 `NSString`。
- 当你使用 `objectForKey:` 时，键可以是任意类中的任意对象。

`objectForKey:` 极其灵活且强大。你可以使用任何数据类型或类作为键来搜索、枚举和组织对象。你可以利用此特性来搜索和组织任何对象的集合——指针、图形数据、游戏令牌等等——并以有用的方式配对对象。

`valueForKey:` 则相形见绌。它强制你将对象与字符串配对。一些 Cocoa 框架在其类定义中专门使用 `valueForKey:`，因此你常常不得不使用它。

### 使用 `setValue:forKey`

`NSArray` 和 `NSSet` 实现了 `setValue:forKey:` 方法。它会枚举数组或集合中的项，并依次对每一项运行 `setValue:forKey:`。

尽管这些类名义上是只读的，但你可以使用此方法来修改存储在非可变对象内部的可变集合中的值。

**图 12.1**

说明 `valueForKey:` 和 `objectForKey:` 如何返回同一个对象。
这些方法之间的差异在于键，而不在于对象/值。

![](img/2b293e29fc15b0797f113b85dd429b6e_309_0.png)

图 12.2 展示了一个示例。一个 NSArray 保存了一系列 NSMutableDictionary 项。对数组运行 setValue:forKey: 方法会修改每个字典中匹配键的值。

你可以使用此技术实现快速重置功能。例如，数组可能包含游戏中玩家信息的数组。你可以用一行代码为每位玩家重置任意一个键值。

## 实现键值观察

数据集合对象不可观察。添加、移除、计数和搜索项不会触发键值观察（KVO）。要实现 KVO，必须手动添加。通常你会将更改包装在一个或多个编辑方法中。每个方法可以指定一个通知，告知 KVO 有关编辑的信息。例如：

```objective-c
- (void) editMethod: (id) objectsToReplace
             atIndexes: (NSIndexSet *) indexes {
    [self willChange: NSKeyValueChangeReplacement
              atIndexes: indexes
                forKey: @"key"];
    // Add code to replace some of the objects in the collection
    [self didChange: NSKeyValueChangeReplacement
      valuesAtIndexes: indexes forKey: @"these objects"];
}
```

支持的常量包括：

- NSKeyValueChangeReplacement
- NSKeyValueChangeRemoval
- NSKeyValueChangeInsertion

**图 12.2**

setValue: forKey: 可以更改可变对象内部的值——即使它们存储在一个非可变集合中。

![](img/2b293e29fc15b0797f113b85dd429b6e_310_0.png)

如果你的代码不需要知道项何时被更改、移除或插入，你可以在编辑后通过一个虚拟赋值触发 KVO。

```
self.dataCollectionObject = dataCollectionObject;
```

这会告诉 KVO 对象已被访问，但不会说明集合是否或如何被更改。这是一个小方案，但在某些应用中可能足够。

## 使用 NSNumber 和 NSValue

你可以向任何数据集合添加任何对象。你也可以在同一集合中混合使用对象，这也是数据集合对象如此强大的原因之一。默认情况下，你可以用任何类填充任何数据对象中的任何数据槽。

![](img/2b293e29fc15b0797f113b85dd429b6e_311_0.png)

> **注意**
> 
> Cocoa 没有类型化数组或集合的概念。如果需要强制类型，可以手动实现。

因为数据集合存储对象而不是裸值，所以你经常需要使用 NSNumber 和 NSValue 来“对象化”现有值。

NSNumber 相对容易使用。要创建 NSNumber 对象，请使用

```
NSNumber *aNumber = [NSNumber numberWith<Type>: rawValue];
```

NSNumber 类参考列出了支持的类型。有 long 和无符号变体可用。

要将 NSNumber 转换回数值 C 类型，请使用

```
<a type> rawValue = [aNumber <type>Value];
```

例如，要转换为 float 以及从 float 转换，请使用

```
NSNumber *aNumber = [NSNumber numberWithFloat: 2.71828];
float theNumber = [aNumber floatValue];
```

你可以使用 stringValue 方法将数字转换为字符串。格式是任意的，因此最好使用 NSString stringWithFormat: 方法进行转换，因为你可以应用标准 C 格式说明符。详细信息请参见第 15 章。

NSValue 更加开放，它支持少数非对象的 Cocoa 数据类型，例如 NSRange、NSRect、NSPoint 等。你还可以使用它来“对象化”自定义 C 数据结构。最有用的内置类型包括：

- 指针
- 几何点（NSPoint）
