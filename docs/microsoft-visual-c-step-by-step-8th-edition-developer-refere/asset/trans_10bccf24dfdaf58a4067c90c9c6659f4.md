

## 泛型与广义类

需要注意的是，使用类型参数的泛型类与设计为接受可强制转换为不同类型的参数的广义类是不同的。例如，前面所示的基于对象的 Queue 类版本就是一个广义类。该类的实现只有一个，其方法接受对象参数并返回对象类型。你可以用这个类处理 int、字符串以及许多其他类型，但在每种情况下你都使用的是同一个类的实例，并且你必须将使用的数据在对象类型之间进行强制转换。

将其与 Queue<T> 类进行比较。每次你使用此类并带上类型参数（如 Queue<int> 或 Queue<Horse>），都会导致编译器生成一个全新的类，该类恰好具有由泛型类定义的功能。这意味着 Queue<int> 与 Queue<Horse> 是完全不同的类型，但它们恰好具有相同的行为。你可以将泛型类视为定义了一个模板，然后编译器按需使用该模板生成新的特定类型类。泛型类的特定类型版本（Queue<int>、Queue<Horse> 等）被称为构造类型，你应该将它们视为截然不同的类型（尽管它们具有相似的一组方法和属性）。

## 泛型与约束

偶尔，你会希望确保泛型类使用的类型参数标识的类型提供了某些方法。例如，如果你正在定义一个 PrintableCollection 类，你可能希望确保存储在该类中的所有对象都有一个 Print 方法。你可以通过使用约束来指定此条件。

通过使用约束，你可以将泛型类的类型参数限制为实现特定接口集的类型，从而提供这些接口定义的方法。例如，如果 IPrintable 接口定义了 Print 方法，你可以这样创建 PrintableCollection 类：

Click here to view code image

```
public class PrintableCollection<T> where T : IPrintable
```

当你使用类型参数构建此类时，编译器会检查用于 T 的类型是否确实实现了 IPrintable 接口；如果没有，它将停止并出现编译错误。

## 创建泛型类

.NET Framework 类库中的 System.Collections.Generic 命名空间包含许多可供你使用的现成泛型类。你也可以定义自己的泛型类，这就是本节中你将要做的事情。在此之前，让我们先介绍一些背景理论。

## 二叉树的理论

在以下练习中，你将定义并使用一个表示二叉树的类。

*二叉树* 是一种有用的数据结构，你可以用它执行各种操作，包括非常快速地对数据进行排序和搜索。关于二叉树的细节已有很多著作，但本书的目的并不是详细涵盖这一主题。相反，你将只查看相关的事实。如果你有兴趣了解更多，请参阅 Donald E. Knuth 所著的 *《计算机程序设计艺术，第 3 卷：排序与查找，第 2 版》*（Addison-Wesley Professional，1998）。尽管年代久远，但它仍是排序和搜索算法公认的开创性著作。

二叉树是一种递归（自引用）数据结构，可以为空或包含三个元素：一个数据，通常称为 *节点*，以及两个子树，它们本身也是二叉树。这两个子树通常称为 *左子树* 和 *右子树*，因为它们通常分别描绘在节点的左侧和右侧。每个左子树或右子树要么为空，要么包含一个节点和其他子树。从理论上讲，整个结构可以无限延续。下面的图像显示了小型二叉树的结构。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_449_0.png)

二叉树的真正威力在你将其用于排序数据时变得明显。如果从同一类型的无序对象序列开始，你可以构建一个有序二叉树，然后遍历树以按顺序访问每个节点。将项目 I 插入有序二叉树 B 的算法如下所示：

Click here to view code image

```
If the tree, B, is empty
Then
    Construct a new tree B with the new item I as the node, and empty left and
    right subtrees
Else
    Examine the value of the current node, N, of the tree, B
    If the value of N is greater than that of the new item, I
    Then
        If the left subtree of B is empty
        Then
            Construct a new left subtree of B with the item I as the node, and
            empty left and right subtrees
        Else
            Insert I into the left subtree of B
        End If
    Else
        If the right subtree of B is empty
        Then
            Construct a new right subtree of B with the item I as the node, and
            empty left and right subtrees
        Else
            Insert I into the right subtree of B
        End If
    End If
End If
```

请注意，此算法是递归的，根据项目的值与树中当前节点的比较结果，调用自身将项目插入左子树或右子树。

### Note

表达式 greater than 的定义取决于项目和节点中数据的类型。对于数值数据，greater than 可以是简单的算术比较，对于文本数据，可以是字符串比较；然而，你必须为其他形式的数据提供它们自己的比较值的方法。你将在即将到来的“使用泛型构建二叉树类”部分实现二叉树时了解更多关于此的信息。

如果你从一个空的二叉树和一个无序的对象序列开始，你可以遍历无序序列，使用此算法将每个对象插入二叉树，从而得到一个有序树。下图显示了从一组五个整数构造树的步骤。

① Data: 1, 5, -2, 1, 6
Tree: (Empty)

② Data: 5, -2, 1, 6

③ Data: -2, 1, 6

④ Data: 1, 5, -2, 1, 6

⑤ Data: 6

⑥ Data:

在你构建了有序二叉树后，你可以通过依次访问每个节点并打印找到的值来按顺序显示其内容。实现此任务的算法也是递归的：

Click here to view code image

```
If the left subtree is not empty
Then
    Display the contents of the left subtree
End If
Display the value of the node
If the right subtree is not empty
Then
    Display the contents of the right subtree
End If
```

下图显示了输出树的步骤。请注意，整数现在按升序显示。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_452_0.png)

## 使用泛型构建二叉树类

在以下练习中，你将使用泛型定义一个二叉树类，能够容纳几乎任何类型的数据。唯一的限制是数据类型必须提供在不同实例之间比较值的方法。

二叉树类是你可能会在许多不同应用程序中发现有用的类。因此，你将把它实现为类库而不是作为独立的应用程序。这样你就可以在其他地方使用此类，而无需复制源代码并重新编译它。类库是一组编译后的类（以及其他类型，如结构和委托）存储在程序集中。程序集是一个通常具有 .dll 后缀的文件。其他项目和应用程序可以通过向其程序集添加引用，然后使用 using 指令将命名空间引入作用域来使用类库中的项目。你将在测试二叉树类时执行此操作。

## System.IComparable 和 System.IComparable<T> 接口

将节点插入二叉树的算法要求你比较要插入的节点的值与树中已有的节点。如果使用数值类型，如 int，你可以使用 <、> 和 == 运算符。然而，如果使用其他类型，如前面章节中描述的 Mammal 或 Circle，该如何比较对象呢？

如果需要创建一个需要能够根据某种自然（或可能不自然）的顺序比较值的类，你应该实现 IComparable 接口。此接口包含一个名为 CompareTo 的方法，它接受一个指定要与当前实例进行比较的对象的单个参数，并返回一个整数，表示比较结果，如下表所述。

| Value | Meaning |
|---|---|
| Less than 0 | The current instance is less than the value of the parameter. |
| 0 | The current instance is equal to the value of the parameter. |
| Greater than 0 | The current instance is greater than the value of the parameter. |

作为示例，考虑第 7 章中描述的 Circle 类。让我们在这里再次查看它：

Click here to view code image

```
class Circle
{
    public Circle(int initialRadius)
    {
        radius = initialRadius;
    }

    public double Area()
    {
        return Math.PI * radius * radius;
    }

    private double radius;
}
```

你可以通过实现
