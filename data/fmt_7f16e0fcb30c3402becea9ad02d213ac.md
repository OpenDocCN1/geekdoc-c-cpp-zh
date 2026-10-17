
Horse myHorse = new Horse();

queue.Enqueue(myHorse); // 现在合法 - Horse 是一个对象

...

```
Horse dequeuedHorse = (Horse)queue.Dequeue(); // 需要将对象强制转换回 Horse
```

如果你不对返回的值进行强制转换，将得到编译器错误“无法将类型 'object' 转换为 'Horse'”。

这种执行显式强制转换的要求削弱了 `object` 类型所提供的许多灵活性。此外，很容易编写出这样的代码：

点击此处查看代码图像

```csharp
Queue queue = new Queue();
Horse myHorse = new Horse();
queue.Enqueue(myHorse)
```

```csharp
Circle myCircle = (Circle)queue.Dequeue(); // 运行时错误
```

尽管这段代码可以编译，但它会在运行时抛出 `System.InvalidException` 异常。该错误是由于在出队时尝试将一个 `Horse` 对象的引用存储在 `Circle` 中，而这两个类型是不兼容的。这个错误直到运行时才被发现，因为编译器在编译时没有足够的信息来执行此检查。被出队的对象的真实类型只有在代码运行时才会变得明显。

使用 `object` 创建通用类和方法的另一个缺点是，如果运行时需要将对象转换为值类型并反之，可能会消耗额外的内存和处理器时间。考虑以下处理 `int` 队列的代码：

点击此处查看代码图像

```csharp
Queue queue = new Queue();
int myInt = 99;
queue.Enqueue(myInt); // 将 int 装箱为对象
```

```csharp
myInt = (int)queue.Dequeue(); // 将对象拆箱为 int
```

`Queue` 期望它持有的项是对象，而 `object` 是引用类型。入队值类型（如 `int`）需要将其装箱（boxing）以转换为引用类型。同样，出队 `int` 需要通过拆箱（unboxing）将其转换回值类型。（更多细节请参见第8章中的“装箱”和“拆箱”章节）。尽管装箱和拆箱是透明发生的，但它们会增加性能开销，因为它们涉及动态内存分配。对于每个项目来说，这种开销很小，但当程序创建大量值类型的队列时，这些开销就会累积。

# 泛型解决方案

C# 泛型（generics）消除了对强制转换的需求，提高了类型安全性，减少了所需的装箱，并更容易创建通用类和方法。泛型类和方法接受类型参数，这些参数指定了它们的操作对象的类型。在 C# 中，你通过在角括号中提供类型参数来指示类是泛型的，例如：

```csharp
class Queue<T>
{
  ...
}
```

此示例中的 `T` 在编译时作为实际类型的占位符。当你编写代码来实例化泛型 `Queue` 类时，你提供了应该替换 `T` 的类型（`Circle`、`Horse`、`int` 等）。当你在类定义字段和方法时，你使用相同的占位符来指示这些项目的类型，如下：

点击此处查看代码图像

```csharp
class Queue<T>
{
  private T[] data; // 数组类型为 'T'，'T' 是类型参数
  ...
  public Queue()
{
    this.data = new T[DEFAULTQUEUESIZE]; // 使用 'T' 作为数据类型
  }
  public Queue(int size)
{
    this.data = new T[size];
  ...
}
```

```csharp
public void Enqueue(T item) // 使用 'T' 作为方法的类型
{
  ...
}
public T Dequeue() // 使用 'T' 作为返回值的类型
{
  T queueItem = this.data[this.tail]; // 数组中的数据类型为 'T'
  ...
  return queueItem;
}
```

类型参数 `T` 可以是任何 C# 标识符，尽管通常使用单个字符 `T`。在创建 `Queue` 对象时，它会被你指定的类型所替换。以下示例创建了一个 `int` 队列和一个 `Horse` 队列：

点击此处查看代码图像

```csharp
Queue<int> intQueue = new Queue<int>();
Queue<Horse> horseQueue = new Queue<Horse>();
```

此外，编译器现在在构建应用程序时拥有足够的信息来执行严格类型。当你调用 `Dequeue` 方法时，不再需要对数据进行强制转换，编译器可以尽早发现任何类型不匹配错误。

点击此处查看代码图像

```csharp
intQueue.Enqueue(99);
int myInt = intQueue.Dequeue(); // 无需强制转换
Horse myHorse = intQueue.Dequeue(); // 编译器错误：无法将类型 'int' 隐转换为 'Horse'
```

你应该意识到，这种用 `T` 替换指定类型的操作并非简单的替换机制。相反，编译器执行的是完全替换，以便你可以指定任何有效类型。这里有更多示例：

点击此处查看图像（等等，OCR 文本在这里似乎碎片化了，让我们根据第626页重新对齐）

```csharp
struct Person
{
  ...
}
Queue<int> intQueue = new Queue<int>();
Queue<Horse> horseQueue = new Queue<Horse>();
```

第一个示例创建了一个整数队列，而第二个示例创建了一个 `Person` 队列。对于 `intQueue` 队列，这些方法看起来如下：

点击此处查看代码图像

```csharp
public void Enqueue(int item);
public int Dequeue();
```

对于 `personQueue` 队列，这些方法看起来如下：

点击此处查看代码图像

```csharp
public void Enqueue(Person item);
public Person Dequeue();
```

将这些定义与前节所示的基于对象的 `Queue` 版本进行对比。在泛型类中，项参数 `item` 是值类型，不需要装箱。同样，`Dequeue` 返回的值也是一个值类型，不需要拆箱。对于其他队列，也会生成一组类似的方法。

> 注意
> `System.Collections.Generic` 命名空间 .NET 类库为上述描述的类提供了实现。该命名空间还包括其他集合类。这些在第18章中会有更详细的描述。

> 注意
> 你还可以使用与泛型类相同的类型参数语法来定义泛型结构和接口。

# 泛型 vs 通用类

使用类型参数的泛型类与设计为接收可以强制转换为不同类型的参数的通用类不同。例如，之前所示基于对象的 `Queue` 类版本就是通用类。该类只有一个实现，它的方法接受 `object` 参数并返回 `object` 类型。你可以与 `int`、`string` 和许多其他类型配合使用，但在每个情况下，你使用的都是同一个类的实例，并且必须需要在对象和类型之间进行强制转换。

将此与 `Queue<T>` 进行对比。每当你使用参数使用该类（例如 `Queue<int>` 或 `Queue<Horse>`）时，编译器都会生成一个具有泛型类定义功能的全新类。这意味着 `Queue<int>` 与 `Queue<Horse>` 是完全不同的类型，但它们恰好具有相同的行为。

你可以将泛型类理解为定义了模板的类，编译器根据需要生成特定类型的类。泛型类的特定类型版本（`Queue<int>`、`Queue<Horse>` 等）被称为构造类型（constructed types），你应该将它们视为本质不同的类型（尽管它们具有相似的方法和属性）。

# 泛型与约束

有时，你希望确保泛型类使用的类型参数标识的是一个提供特定方法的类型。例如，如果你正在定义一个 `PrintableCollection` 类，你可能希望存储在类中的所有对象都具有 `Print` 方法。你可以通过使用约束（constraint）来指定此条件。

通过使用约束，你可以将泛类的类型参数限制为实现了特定接口集合的类型，从而提供这些接口定义的方法。例如，如果 `IPrintable` 接口定义了 `Print` 方法，你可以这样创建 `PrintableCollection` 类：

[点击此处查看代码图片]()

```
public class PrintableCollection<T> where T : IPrintable
```

当你使用此类型参数构建此类类时，编译器会检查用于 `T` 的类型是否实际上实现了 `IPrintable` 接口；如果没有实现，它将停止并报告编译错误。

你还可以通过 `struct` 约束强制类型参数为结构体值类型而不是类：

[点击此处查看代码图片]()

```
public class StructCollection<T> where T : struct
```

类约束与之类似，只不过它确保了类型参数是一个引用类型（类）。

# 创建泛型类

.NET 类库中的 `System.Collections.Generic` 命名空间包含一些现成的泛型类。你也可以定义自己的泛型类，这正是本节将要做的内容。在此之前，让我们先介绍背景理论。

# 二叉树理论

在接下来的练习中，你将定义并使用一个表示二叉树的类。二叉树是一种用于多种操作的数据结构，包括快速遍历树和搜索数据。

> 有许多专门关于二叉树细节的著作，但本书的目的并不是详细介绍这个主题。相反，你将看到相关的实。如果你感兴趣了解更多，请参考 Donald E. Knuth 写的《The Art of Computer Programming, Volume 3: Sorting and Searching, 2nd Edition》（Addison-Wesley Professional, 1998）。尽管年代久远，但这是排序和搜索算法领域公认的开创性著作。二叉树是一种递归（自引用）数据结构，可以是空的，也可以包含三个元素：一个数据（通常称为节点）和两个子树（子树本身也是二叉树）。这两个子树通常被称为左子树和右子树，因为它们通常被描绘在节点的左侧和右侧。每个左子树或右子树要么为空，要么包含一个节点和其他子树。理论上，整个结构可以无限持续。下面的图片显示了一个小型二叉树的结构：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_629_0.png)

当你使用二叉树进行数据排序时，它的真实威力就显而易见了。如果你从一个相同类型的无序对象序列开始，你可以构建一个有序二叉树，然后遍历树以按顺序访问每个节点。将项目 `I` 插入有序二叉树 `B` 的算法所示：

[点击此处查看代码图片]()

```
If 树 B, 是空的
Then
  构建一个新树 B，将新项目 I 作为节点，并保持左
  右子树为空
Else
  检查树 B 的当前节点 N 的值
  If N 的值大于新项目 I 的值
  Then
    If B 的左子树为空
    Then
      构建 B 的一个新的左子树，以项目 I 作为节点，
      并保持左和右子树为空
    Else
      将 I 插入 B 的左子树
  End If
Else
  If B 的右子树为空
  Then
    构建 B 的一个新的右子树，以项目 I 作为节点，
    并保持左和右子树为空
  Else
    将 I 插入 B 的右子树
  End If
End If
End If
```

注意，该算法是递归的，它根据项目值与树中当前节点的比较结果，调用自己将项目插入左子树或右子树。

> 注意
大于表达式的定义取决于项目和节点中数据的类型。对于数值数据，大于可以是简单的算术比较；对于文本数据，它可以是字符串比较。然而，你必须为其他形式的数据提供自己的比较值的方法。你将在下一节实现二叉树时学习更多相关内容。

如果你从一个空二叉树和一个无序对象序列开始，你可以遍历该无序序列，使用此算法将每个对象插入二叉树，从而生成一棵有序树。下一张图片显示了从五个整数构建树的步骤。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_631_0.png)

构建好有序二叉树后，你可以通过依次访问每个节点并打印找到的值来顺序显示其内容。实现此任务的算法也是递归的：

[点击此处查看代码图片]()

```
If 左子树不为空
Then
  显示子树的内容
End If
显示节点的值
If 右子树不为空
Then
  显示子树的内容
End If
```

下面的图片显示了输出树的步骤。注意整数现在是升序排列的。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_632_0.png)

# 使用泛型构建树类

在下面的练习中，你将使用泛型定义一个能够容几乎任何类型的类。唯一的限制是数据类型必须提供比较值的方法。你可能会发现这个类在许多应用程序中有用。通过实现 `IComparable` 接口并提供 `CompareTo` 方法，使 `Circle` 类变得“可比较的”。在这个示例中，`CompareTo` 方法根据面积比较 `Circle` 对象。面积较大的圆被认为大于面积较小的圆。（等等，OCR 文本在这里包含了一些重复和错乱的章节，让我们根据逻辑流重新对齐）。

如果你检查 `System.IComparable` 接口，你会发现它的参数被定义为 `object`。然而，这种方法并不是类型安全的。为了理解为什么，考虑如果你尝试向 `CompareTo` 方法传递非 `Circle` 对象的对象会发生什么。`System.IComparable` 接口

需要使用类型转换来访问 `Area` 方法。如果参数不是 `Circle` 而其他类型的对象，则此转换将失败。然而，System命名空间还定义了泛型 `IComparable<T>` 接口，它包含以下方法：

```
int CompareTo(T other);
```

注意，此方法接收一个类型参数 (T) 而不是对象，因此它比非泛型的接口安全得多。下面的代码显示了你如何在 `Circle` 类中实现此接口：

```
class Circle : System.IComparable<Circle>
{
    public int CompareTo(Circle other)
    {
        if (this.Area() == other.Area())
            return 0;
        if (this.Area() > other.Area())
            return 1;
        return -1;
    }
}
```

`CompareTo` 方法的参数必须与接口 `IComparable<Circle>` 中指定的类型匹配。通常，实现 `System.IComparable<T>` 接口比实现 `System.IComparable` 接口更好。你也可以实现两者，.NET 中的许多类型都是这样做。

## 创建 Tree<TItem> 类

1. 启动 Microsoft Visual Studio 2022，如果它尚未运行。
2. 在“文件”菜单上，指向“新建”，然后选择“项目”。
3. 在“创建新项目”对话框中，将“语言”下拉列表框设置为 C#，“平台”下拉列表框设置为 Windows，并将“项目类型”下拉列表框设置为“所有项目类型”。选择“类库”模板，然后选择“下一步”：

## 创建一个新项目

最近使用的项目模板

- 控制台应用程序
- 空应用（通用 Windows）
- 类库
- 类库（通用 Windows）

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_636_0.png)

4. 在“配置您的新项目”对话框中，在**项目名称**框中，输入 **BinaryTree**。在**位置**框中，在你的**文档**文件夹中指定 `\Microsoft Press\VCSB\Chapter 17`。然后选择“**下一步**”。

5. 在“其他信息”对话框中，将框架选择为 **.NET 6.0**，然后选择“**创建**”。

使用类库模板，你可以创建可以被不同应用程序重用的程序集。要在应用程序中使用类库中的类，必须先将包含类库编译代码的程序集复制到你的计算机上。

6. 在“解决方案管理器”中，右键点击 **Class.cs**，选择“**重命名**”，并将文件名更改为 **Tree.cs**。

7. 在“代码和编辑器”窗口中，将 *Class* 的定义更改为 `Tree<TItem>`，如下：

```
class Tree<TItem>
```

8. 在“代码和编辑器”窗口中，修改 `Tree<TItem>` 类的定义，指定类型参数 `TItem` 必须是实现了 `IComparable<T>` 接口的类型。修改后的 `Tree<TItem>` 定义所示（更改已高亮）：

```
class Tree<TItem>
>
```

9. 为 `Tree<TItem>` 类添加属性：一个名为 `NodeData` 的 `TItem` 属性以及名为 `LeftTree` 和 `RightTree` 的 `Tree<TItem>` 属性。注意 `LeftTree` 和 `RightTree` 都被声明为可空类型。

```
class Tree<TItem> where TItem : IComparable<TItem>
{
  public TItem NodeData { get; set; }
  public Tree<TItem>? LeftTree { get; set; }
  public Tree<TItem>? RightTree { get; set; }
```
