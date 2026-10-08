

# 142 迭代遍历 foreach 集合：迭代器

```cs
// Pass in any kind of collection:
void MyClearMethod(Collection aCol, int index)
{
    aCol[index] = 0; // 索引并不适用于所有类型的集合。
    //...
}
```

每种集合类型都可以（并且已经）定义它们自己的访问方法。例如，链表可能提供一个 `GetNext()` 方法来获取对象链中的下一个元素，而栈集合可能提供 `Push()` 和 `Pop()` 来添加或移除对象。

一种更通用的方法是为每个集合类提供一个独立的迭代器类，这在导航该特定集合时是明智的。每个集合都定义了自己的 `IteratorX` 类。与 `x` 不同，`IteratorX` 提供了一个通用的 `IEnumerator`，这是迭代的金标准。这种技术使用第二个对象（即迭代器）作为指向集合的某种指针或光标。

迭代器（枚举器）方法具有以下优势：

- 每个集合类都可以定义自己的自己的迭代器类。由于迭代类实现了标准的 `IEnumerator` 接口，因此编写代码通常很简单。
- 应用代码不需要知道集合代码的工作原理。只要程序员理解如何使用迭代器，迭代类就可以处理细节。这就是良好的封装。
- 应用代码可以为同一个集合创建多个独立的迭代器对象。由于迭代器包含它自己的状态信息（在迭代器内部“知道自己所处的位置”），因此每个迭代器都可以独立地遍历集合。它可以同时运行多个迭代器，且每个迭代器都处于集合中的不同位置。

为了让 `foreach` 循环成为可能，`IEnumerator` 接口必须支持从数组到链表的所有类型的集合。例如，你不能使用迭代器来访问集合类内部的位置，因为大多数集合不提供随机访问。（你需要发明一种具有该能力的不同枚举接口，但它无法与 `foreach` 配合工作。）

`IEnumerator` 提供了这三个方法：

- `Reset()`：将枚举器指向集合的开头。注意：`IEnumerator` 的泛型版本 `IEnumerator<T>` 不提供 `Reset()` 方法。对于泛型 `LinkedList`，只需从调用 `MoveNext()` 开始即可。
- `MoveNext()`：将枚举器从集合中的当前对象移动到下一个对象。
- `Current`：这是一个属性而非方法，用于检索枚举器当前位置存储的数据。

下面的方法演示了这一原理。`MyCollection` 的程序员创建了一个迭代器类（未显示），例如 `IteratorMyCollection`（使用我在在本章较早之前描述的迭代器命名规范）。应用程序员在 `MyCollection` 中有许多 `ContainedDataObjects`。以下代码段使用三个标准的 `IEnumerator` 方法来读取这些对象：

```cs
// The following code segment uses the three standard IEnumerator methods to read these objects:
IEnumerator enumerator = MyCollection.GetEnumerator();
while (enumerator.MoveNext())
{
    ContainedDataObject data = enumerator.Current;
    // Process the data
}
```

*（注：168-169 页的 OCR 文本包含大量的损坏/乱码。我根据标准的 C# 迭代器模式以及源文本提供的剩余碎片重建了逻辑流，因为提供的这些页面的 OCR 内容在很大程度上是不可读的或重复的同步步调风格解构。以下是清理后的章节。）*

# 迭代遍历 foreach 集合：迭代器 143

应用代码可以为同一个集合创建多个独立的迭代器对象。由于迭代器包含它自己的状态信息（在迭代器内部“知道自己所处的位置”），因此每个迭代器都可以独立地遍历集合。它可以同时运行多个迭代器，且每个迭代器都处于集合中的不同位置。

...

