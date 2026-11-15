

继续处理。当调用站点处的 foreach 语句终止时，迭代器的状态不再保存。由于生成的代码永远不会重置迭代器的状态，而是在需要时创建一个新的迭代器，因此再次调用迭代器始终是安全的。

图 16.8 显示了发生情况的高级序列图。请记住，MoveNext() 方法出现在 IEnumerable<T> 接口上。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_688_0.png)

图 16.8: 带 yield return 的序列图

## 更多迭代器示例

在修改 BinaryTree<T> 之前，必须使用迭代器修改 Pair<T> 以支持 IEnumerable<T> 接口。清单 16.14 是一个示例，用于生成 Pair<T> 中的每个元素。

## 清单 16.14: 使用 yield 实现 BinaryTree<T>

```csharp
public struct Pair<T>: IPair<T>,
    IEnumerable<T>
{
    public Pair(T first, T second)
    {
        _first = first;
        _second = second;
    }

    public T First
    {
        get { return _first; }
        private set { _first = value; }
    }

    private T _first;
    public T Second
    {
        get { return _second; }
        private set { _second = value; }
    }

    private T _second;

#region IEnumerable<T>
public IEnumerator<T> GetEnumerator()
{
    yield return First;
    yield return Second;
}
#endregion IEnumerable<T>

#region IEnumerable Members
System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator()
{
    return GetEnumerator();
}
#endregion
}
```

在清单 16.14 中，对 Pair<T> 数据类型的迭代循环两次：首先通过 yield return First，然后通过 yield return Second。每次在 GetEnumerator() 中遇到 yield return 语句时，状态都会被保存，执行似乎会“跳出” GetEnumerator() 方法上下文并进入调用站点上下文。当第二次迭代开始时，GetEnumerator() 将再次开始执行，使用 yield return Second 语句。

System.Collections.Generic.IEnumerable<T> 继承自 System.Collections.IEnumerable。因此，在实现 IEnumerable<T> 时，也有必要实现 IEnumerable。在清单 16.14 中，您是这样显式实现的，实现仅涉及对 IEnumerable<T> 的 GetEnumerator() 实现的调用。由于 IEnumerable<T> 和 IEnumerable 之间的类型兼容性（通过继承），从 IEnumerable.GetEnumerator() 到 IEnumerable<T>.GetEnumerator() 的调用始终有效。由于两个 GetEnumerator() 的签名相同（返回类型不区分签名），一个或两个实现必须是显式的。考虑到 IEnumerable<T> 版本提供的额外类型安全，您显式实现 IEnumerable 的实现。

清单 16.15 使用 Pair<T>.GetEnumerator() 方法，并在两行连续显示 "Inigo" 和 "Montoya"。

## 清单 16.15: 通过 foreach 使用 Pair<T>.GetEnumerator()

```csharp
Pair<string> fullname = new Pair<string>("Inigo", "Montoya");
foreach (string name in fullname)
{
    Console.WriteLine(name);
}
```

请注意，foreach 循环中对 GetEnumerator() 的调用是隐式的。

## 在循环中放置 yield return

无需像在 CSharpPrimitiveTypes 和 Pair<T> 中那样对每个 yield return 语句进行硬编码。使用 yield return 语句，您可以从循环构造内部返回值。清单 16.16 使用 foreach 循环。每次在 GetEnumerator() 中执行 foreach 时，它都会返回下一个值。

## 清单 16.16: 在循环中放置 yield return 语句

```csharp
public class BinaryTree<T>: IEnumerable<T>
{
    // ...

    #region IEnumerable<T>
    public IEnumerator<T> GetEnumerator()
    {
        // Return the item at this node.
        yield return Value;

        // Iterate through each of the elements in the pair.
        foreach (BinaryTree<T> tree in SubItems)
        {
            if (tree != null)
            {
                // Since each element in the pair is a tree,
                // traverse the tree and yield each
                // element.
                foreach (T item in tree)
                    yield return item;
            }
        }
    }

    #endregion IEnumerable<T>

#region IEnumerable Members
System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator()
{
    return GetEnumerator();
}
#endregion
}
```

在清单 16.16 中，第一次迭代返回二叉树中的根元素。在第二次迭代期间，您遍历子元素对。如果子元素对包含非 null 值，则您遍历到该子节点并生成其元素。请注意，foreach(T item in tree) 是对子节点的递归调用。

与 CSharpPrimitiveTypes 和 Pair<T> 观察到的一样，您现在可以使用 foreach 循环遍历 BinaryTree<T>。清单 16.17 演示了这一点，输出 16.6 显示了结果。

## 清单 16.17: 将 foreach 与 BinaryTree<string> 一起使用

```csharp
// JFK
jfkFamilyTree = new BinaryTree<string>(
    "John Fitzgerald Kennedy");
jfkFamilyTree.SubItems = new Pair<BinaryTree<string>>(
    new BinaryTree<string>("Joseph Patrick Kennedy"),
    new BinaryTree<string>("Rose Elizabeth Fitzgerald"));
// Grandparents (Father's side)
jfkFamilyTree.SubItems.First.SubItems =
    new Pair<BinaryTree<string>>(
        new BinaryTree<string>("Patrick Joseph Kennedy"),
        new BinaryTree<string>("Mary Augusta Hickey")));
// Grandparents (Mother's side)
jfkFamilyTree.SubItems.Second.SubItems =
    new Pair<BinaryTree<string>>(
        new BinaryTree<string>("John Francis Fitzgerald"),
        new BinaryTree<string>("Mary Josephine Hannon")));
foreach (string name in jfkFamilyTree)
    Console.WriteLine(name);
}
```

输出 16.6:
John Fitzgerald Kennedy
Joseph Patrick Kennedy
Patrick Joseph Kennedy
Mary Augusta Hickey
Rose Elizabeth Fitzgerald
John Francis Fitzgerald
Mary Josephine Hannon

## 初学者主题

### struct 与类

将 Pair<T> 定义为 struct 而不是 class 的一个有趣副作用是，SubItems.First 和 SubItems.Second 不能直接赋值。以下代码会产生编译错误，指出 SubItems 无法修改，“因为它不是变量”：

```csharp
jfkFamilyTree.SubItems.First =
    new BinaryTree<string>("Joseph Patrick Kennedy");
```

问题在于 SubItems 是 Pair<T> 类型（一个 struct）的属性。因此，当属性返回值时，会创建 _SubItems 的副本，在副本上赋值 First 而该副本在语句结束时立即丢失，这会产生误导。幸运的是，C# 编译器阻止了这种情况。

要解决此问题，请勿直接赋值（请参阅清单 16.17 中的方法），为 Pair<T> 使用 class 而不是 struct，不要创建 SubItems 属性而改用字段，或在 BinaryTree<T> 中提供直接访问 _SubItems 成员的属性。

### 取消进一步迭代：yield break

有时您可能希望取消进一步迭代。可以通过包含 if 语句来实现，以便不再执行代码中的任何后续语句。但是，您也可以跳回调用站点，导致 MoveNext() 返回 false。清单 16.18 显示了此类方法的示例。

