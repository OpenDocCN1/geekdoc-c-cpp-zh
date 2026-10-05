
替换现有的 `throw` 语句，如下例中的**粗体**部分所示：

点击此处查看代码图像

```
IEnumerable<TItem> IEnumerable<TItem>.GetEnumerator()
{
    return new TreeEnumerator<TItem>(this);
}
```

迭代 `GetEnumerator` 方法的目的是通过集合构造枚举器对象。在这种情况下，你只需要使用树中的数据构建一个新的 `TreeEnumerator<TItem>` 对象即可。

> 注意
> 确保你留了非泛型的 `GetEnumerator` 方法及其默认实现。

+   5. 生成解决方案。纠正报告的任何错误，并在时重新生成解决方案。

现在你将通过使用 `foreach` 语句遍历二叉树并显示其内容，来测试修改后的 `Tree<TItem>` 类。

测试枚举器

+   1. 在“解决方案管理器”中，右键点击 `BinaryTree` 解决方案，指向“添加”，然后选择“新建项目”。

+   2. 选择“控制台应用程序”模板，将项目命名为 `EnumeratorTest`，并将位置设置为文档文件夹中的 `\Microsoft Press\VCSBS\Chapter 19\BinaryTree`。然后选择 `.NET 6.0` 框架并选择“创建”。

+   3. 在“解决方案管理器”中右键点击 `EnumeratorTest` 项目，选择“设为启动项目”。

+   4. 在“项目”菜单上，选择“添加项目引用”。

+   5. 在“引用管理器 - EnumeratorTest”对话框的左侧窗格中，展开“项目”节点并选择`解决方案`。在中间窗格中，选择 `BinaryTree` 项目。然后点击“确定”。

`BinaryTree` 程序集将出现在解决方案管理器中 `EnumeratorTest` 项目的依赖列表中，位于“依赖项”节点下的“项目”文件夹中。

+   6. 在显示 `Program` 类的“代码和文本编辑器”窗口中，文件顶部添加以下 `using` 指令：

```
using BinaryTree;
```

+   7. 将后续代码所示的语句添加到 `Main` 方法中，以替换该方法中的现有代码。这些语句创建并填充了一个整数二叉树：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Tree<int> treel = new Tree<int>(10);
    treel.Insert(5);
    treel.Insert(11);
    treel.Insert(5);
    treel.Insert(-12);
    treel.Insert(15);
    treel.Insert(0);
    treel.Insert(14);
    treel.Insert(-8);
    treel.Insert(10);
}
```

+   8. 添加如下所示**粗体**的 `foreach` 语句，用于枚举树的内容并显示结果：

点击此处查看代码图像

```
static void Main(string[] args)
{
    foreach (int item in tree)
    {
        Console.WriteLine(item);
    }
}
```

+   9. 在“调试”菜单上，选择“开始执行不调试”。

程序运行并按以下顺序显示值：

点击此处查看代码图像

-12, -8, 0, 5, 5, 10, 11, 14, 15

+   10. 按回车键返回 Visual Studio 2022。

# 使用迭代器实现枚举器

如你所见，使集合变为可枚举的过程可能会变得复杂且容易出错。为了方便起，C# 提供了迭代器，可以自动处理此过程的大部分。

迭代器是一个产生有序值序列的代码块。迭代器实际上并不是枚举器类的成员；相反，它指定了枚举器在返回其值时应该使用的序列。换句话说，迭代器只是对枚举序列的描述，C# 编译器可以使用该描述来创建它自己的枚举器。这个概念需要稍微思考才能正确理解，因此请考虑下面的简单示例。

# 一个简单的迭代器

下面的 `BasicCollection<T>` 类说明了实现迭代器的原理。该类使用 `List<T>` 对象持有数据，并提供 `FillList` 方法来填充此列表。同样注意，`BasicCollection<T>` 类实现了 `IEnumerable<T>` 接口。`GetEnumerator` 方法是通过迭代器实现的：

```
using System;
using System.Collections.Generic;
using System.Collections;
class BasicCollection<T> : IEnumerable<T>
{
    private List<T> data = new List<T>();
    public void FillList(params T [] items)
    {
        foreach (var datum in items)
        {
            data.Add(datum);
        }
    }

IEnumerator<T> IEnumerable<T>.GetEnumerator()
{
    foreach (var datum in data)
    {
        yield return datum;
    }
}
IEnumerator IEnumerable.GetEnumerator()
{
    // 此示例中未实现
    throw new NotImplementedException();
}
```

`GetEnumerator` 方法看起来很简单，但值得仔细检查。要记住的第一点是，它似乎并没有返回 `Enumerator<T>` 类型。相反，它遍历 `data` 数组中的项，逐个返回每个项。关键在于使用了 `yield` 关键字。该关键字指示了每次迭代应该返回的值。如果有帮助，你可以将 `yield` 语句设为对方法调用了临时挂起，并将一个值传回给调用者。当调用者需要下一个值时，`GetEnumerator` 方法将从它离开的地方继续执行。最终，数据耗尽，循环结束，`GetEnumerator` 方法终止。

记住，这并不是通常意义上的普通方法。`GetEnumerator` 方法中的代码定义了一个迭代器。编译器使用此代码生成 `IEnumerator<T>` 类的实现，其中包含 `Current` 方法和 `MoveNext` 方法。你实际上看不到这些生成的代码（除非你反编译程序集），但为了方便和减少编写的代码，这是一个很小的代价。你可以按照通常的方式调用由迭代器生成的枚举器，如下刘易·卡罗尔的诗歌《梦游仙境》：

```
BasicCollection<string> bc = new BasicCollection<string>();
bc.FillList("Twas", "brillig", "and", "the", "slithy", "toves");
```

```
foreach (string word in bc)
{
  Console.WriteLine(word);
}
```

这段代码按此顺序输出的内容：

Twas, brillig, and, the, slithy, toves

如果你想提供替代的迭代机制以不同的顺序呈现数据，可以实现接口的其他属性并使用迭代器返回数据。例如，此处所示的 `BasicCollection<T>` 类的 `Reverse` 属性反向发射数据：

```cs
class BasicCollection<T> : IEnumerable<T>
{
  ...
  public IEnumerable<T> Reverse
  {
    get
    {
      for (int i = data.Count - 1; i >= 0; i--)
      {
        yield return data[i];
      }
    }
  }
}
```

你可以这样调用该属性：

```
BasicCollection<string> bc = new BasicCollection<string>();
bc.FillList("Twas", "brillig", "and", "the", "slithy", "toves");
foreach (string word in bc.Reverse)
{
  Console.WriteLine(word);
}
```

这段代码按反方向输出的内容：

toves, slithy, the, and, brillig, Twas

# 使用迭代器为 Tree<TItem> 类定义枚举器

在下一个练习中，你将使用迭代器为 `Tree<TItem>` 类实现枚举器。与之前的一组练习（需要 `MoveNext` 方法将树中的数据预处理为队列）不同，你可以定义一个迭代器，使用更自然的递归机制遍历树，类似于第 17 节讨论的 `WalkTree` 方法。

