

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_648_0.png)

8. 在显示 Program.cs 文件的代码和文本编辑器窗口中，在 Program.cs 文件的顶部添加以下使用 us 指令：

```cs
using BinaryTree;
```

记住，此命名空间包含了 `Tree<TItem>` 类。

9. 在 Program 类的 `Main` 方法之后，添加名为 `InsertIntoTree` 的方法。该方法应声明为 `static void` 方法，接收一个 `Tree<TItem>` 参数和一个名为 `data` 的 `TItem` 元素 `params` 数组。由于后续步骤将描述的原因，tree 参数应该通过引用传递。

方法的定义应该如下：

点击此处查看代码图像

```csharp
static void InsertIntoTree<TItem>(ref Tree<TItem> tree, params TItem[] data)
{
```

10. 用于插入二叉树的元素 `TItem` 类型必须实现 `IComparable<TItem>` 接口。修改 `InsertIntoTree` 方法的定义，并在下面的代码中添加**加粗**所示的 `where` 子句：

点击此处查看图像

```csharp
static void InsertIntoTree<TItem>(ref Tree<TItem> tree, params TItem[] data)
    where TItem : IComparable<TItem>
{}
```

- 1. 将后续示例中**加粗**的语句添加到 `InsertIntoTree` 方法中。这些语句遍历 `params` 列表，使用 `Insert` 方法将每个项目添加到树中。如果 tree 参数指定的初始值是 `null`，则创建一个新的 `Tree<TItem>`；这就是为什么 tree 参数通过引用传递。

点击此处查看图像

```csharp
static void InsertIntoTree<TItem>(ref Tree<TItem> tree, params TItem[] data)
    where TItem : IComparable<TItem>
{
    foreach (TItem datum in data)
    {
        if (tree is null)
        {
            tree = new Tree<TItem>(datum);
        }
        else
        {
            tree.Insert(datum);
        }
    }
}
```

# 测试 InsertIntoTree 方法

- 1. 在 Program 类的 `Main` 方法中，替换现有代码并添加**加粗**的语句。此代码创建了一个用于存储字符数据的新 `Tree`，使用 `InsertIntoTree` 方法填充了一些示例数据，然后使用 `Tree` 的 `WalkTree` 方法显示它：

点击此处查看图像

```csharp
static void Main(string[] args)
{
    Tree<char> charTree = null;
    InsertIntoTree<char>(ref charTree, 'M', 'X', 'A', 'M', 'Z', 'Z', 'N');
    string sortedData = charTree.WalkTree();
    Console.WriteLine($"Sorted data is: {sortedData}");
}
```

- 2. 在 **Build**（生成）菜单上，选择 **Build Solution**（生成解决方案），验证解决方案已编译，并在必要时修正任何错误。
- 3. 在 **Debug**（调试）菜单上，选择 **Start Without Debugging**（不调试启动）。
- 4. 验证程序运行并按以下顺序显示字符值：A M M N X Z
- 5. 按 **Enter** 键返回 Visual Studio 2022。

# 重温指针和内存管理

如果你不是转向 C# 的 C 或 C++ 程序员，可以跳过此侧边栏！第 8 章包含一个侧边栏，描述如何编写直接使用指针而不是使用类型安全引用的 C# 代码。这种机制的原理是优化对数据的访问。这种方法的缺点是不安全的；你必须显式地将代码标记为 `unsafe`，以避免由于应用程序覆盖内存而可能产生的 .NET 问题。

自 C# 和 .NET 框架发布以来，微软在 .NET 库中添加了一些新类型，以消除编写不代码的需求。这些是泛型 `Span<T>` 和 `Memory<T>` 类型。`Span<T>` 表示连续的内存块。它类似于数组，但它是在栈上创建的 `ref struct` 类型。你可以像使用快速托管数组一样使用 `Span<T>` 对象。`Span<T>` 类型具有几个实用的扩展方法，允许你对项目进行排序和搜索。

考虑以下用于建模 `Person` 结构体的 struct。该结构体实现了 `IComparable<Person>` 接口，该接口提供了 `CompareTo` 方法，用于通过 `Name` 字段比较两个 `Person` 对象：

点击此处查看图像

```csharp
struct Person : IComparable<Person>
{
    public string Name;
    public int CompareTo(Person other)
    {
        return this.Name.CompareTo(other.Name);
    }
}
```

你可以这样创建并填充一个 `Person` 结构体的栈数组：

点击此处查看图像

```csharp
Span<Person> personList = stackalloc Person[10];
personList[0] = new Person { Name = "John" };
personList[1] = new Person { Name = "Diana" };
```

然后你可以像这样对数据进行排序和搜索：

点击此处查看图像

```csharp
personList.Sort(); // 对 Span<T> 对象中的数据进行就排序
int item = personList.BinarySearch(new Person { Name = "Diana" });
```

`item` 变量中的值将是 `Name` 字段中值为 "Diana" 的 `Person` 结构体的索引。`Sort` 和 `BinarySearch` 方法使用 `CompareTo` 方法执行工作。如果你有大量数据，使用 `Span<T>` 结构体进行排序和搜索数据比使用普通数组快得多。

除了基于特定数据类型（如 `Person`）创建 `Span<T>` 结构体，你还可以使用它创建一个安全的内存块——即在分配时防止你意外越界的内存。你可以使用 C# 的 `stackalloc` 运算符实现此。下面的示例在栈上分配了一块 1000 字节的内存：

点击此处查看图像

```csharp
Span<byte> chunk = stackalloc byte[1000];
```

如果你需要对此内存块中持有的字节值进行快速求和，可以编写如下方法：

点击此处查看图像

```csharp
public static int Sum(Span<byte> block)
{
    int sum = 0;
    foreach(byte b in block)
    {
        sum += b;
    }
    return sum;
}
```

此代码安全地遍历内存块。你无法在不抛出异常的情况下超出其边界。这种方法提供了使用不安全代码直接访问内存的许多优势，同时消除了许多缺点。

`Span<T>` 类型还有一个只读版本，称为 `ReadOnlySpan<T>`。你可以在创建 `ReadOnlySpan<T>` 对象时初始化数据，但之后无法修改它。

最后，还有 `Span<T>` 和 `ReadOnlySpan<T>` 的堆对应类型。这些类型被称为 `Memory<T>` 和 `ReadOnlyMemory<T>`。它们直接从托管堆分配内存。有关这些类型的更多信息，请参考 Visual Studio 2022 提供的文档。

# 泛型接口

第 8 章演示可以使用对象类型持有任何其他类型的值或引用。例如，以下代码是完全合法的：

```csharp
string myString = "Hello";
object gameObject = myString;
```

记住，从继承的角度来看，String 类派自 `Object` 类，因此所有字符串都是对象。

现在考虑以下泛型接口和类：

点击此处查看代码图像

```csharp
interface IWrapper<T>
{
    void SetData(T data);
    T GetData();
}

class Wrapper<T> : IWrapper<T>
{
    private T storedData;

    void IWrapper<T>.SetData(T data)
    {
        this.storedData = data;
    }

    IWrapper<T>.GetData()
    {
        return this.storedData;
    }
}
```

`Wrapper<T>` 类为指定类型提供了一个简单的封装。`IWrapper` 接口定义了 `Wrapper<T>` 类实现的 `SetData` 方法用于存储数据，以及 `Wrapper<T>` 类实现的 `GetData` 方法用于检索数据。你可以这样创建类的实例并使用它包装字符串：

点击此处查看代码图像

```csharp
Wrapper<string> stringWrapper = new Wrapper<string>();
IWrapper<string> storedStringWrapper = stringWrapper;
storedStringWrapper.SetData("Hello");
Console.WriteLine($"Stored value is {storedStringWrapper.GetData()}");
```

