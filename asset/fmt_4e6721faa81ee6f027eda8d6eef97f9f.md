
| 成员 | 说明 |
| --- | --- |
| `Count` | 返回栈中的项数。 |
| `Push` | 将项添加到栈顶。 |
| `Pop` | 从栈顶移除并返回一项。如果栈为空，则抛出类型为 `InvalidOperationException` 的异常。 |
| `Peek` | 从栈顶返回一项，但不移除该项。 |
| `Contains` | 检查某项是否在栈中，如果是则返回 `true`。 |

在本例中，使用 `Push` 方法向栈中添加了三个项。通过 `foreach` 方法，使用 `IEnumerable` 接口迭代所有项。栈的枚举器不会移除项，只是逐项返回它们（代码文件 `StackSample/Program.cs`）：

```
var alphabet = new Stack<char>();
alphabet.Push('A');
alphabet.Push('B');
alphabet.Push('C');

foreach (char item in alphabet)
{
    Write(item);
}
WriteLine();
```

因为这些项按照从最后添加到最先添加的顺序读取，所以产生以下结果：

```
CBA
```

使用枚举器读取项不会改变项的状态。使用 `Pop` 方法，读取的每一项也会从栈中移除。这样，你可以使用 `while` 循环迭代集合，并通过 `Count` 属性检查是否还有项存在：

```
var alphabet = new Stack<char>();
alphabet.Push('A');
alphabet.Push('B');
alphabet.Push('C');

Write("First iteration:");
foreach (char item in alphabet)
{
    Write(item);
}
WriteLine();

Console.Write("Second iteration:");
while (alphabet.Count > 0)
{
    Write(alphabet.Pop());
}
WriteLine();
```

结果会给出两次 CBA——每次迭代一次。第二次迭代后，栈为空，因为第二次迭代使用了 `Pop` 方法：

```
First iteration: CBA
Second iteration: CBA
```

### 链表

`LinkedList<T>` 是一个双向链表，其中一个元素引用下一个元素和上一个元素，如图 11.3 所示。这样，你可以通过移动到下一个元素轻松地向前遍历整个列表，或者通过移动到上一个元素向后遍历。

![](img/3d365b72b289213a91ade7eb366b8f35_415_0.png)

#### 图 11.3

链表的好处是，如果项目被插入到列表中的任何位置，链表的速度非常快。插入项目时，只需更改前一个项目的 `Next` 引用和后一个项目的 `Previous` 引用，使其指向新插入的项目即可。而对于 `List<T>` 类，插入一个元素后，所有后续元素都必须移动位置。

当然，链表也有缺点。链表中的项目只能一个接一个地访问。要找到位于列表中间或末尾的项目需要花费很长时间。

链表不能只存储列表中的项目；每有一个项目，链表还必须包含关于下一个和上一个项目的信息。这就是为什么 `LinkedList<T>` 包含 `LinkedListNode<T>` 类型的项目。使用 `LinkedListNode<T>` 类，你可以访问列表中的下一个和上一个项目。`LinkedListNode<T>` 类定义了 `List`、`Next`、`Previous` 和 `Value` 属性。`List` 属性返回与该节点关联的 `LinkedList<T>` 对象。`Next` 和 `Previous` 用于遍历列表并访问下一个或上一个项目。`Value` 返回与该节点关联的项目，其类型为 `T`。

`LinkedList<T>` 类本身定义了成员，用于访问列表的第一个（`First`）和最后一个（`Last`）项目，在特定位置插入项目（`AddAfter`、`AddBefore`、`AddFirst`、`AddLast`），从特定位置移除项目（`Remove`、`RemoveFirst`、`RemoveLast`），以及从列表开头（`Find`）或末尾（`FindLast`）开始搜索元素。

演示链表的示例应用程序将链表和列表结合使用。链表包含文档，就像队列示例中那样，但这些文档还具有与之关联的额外优先级。链表中的文档将根据优先级进行排序。如果有多个文档具有相同的优先级，则元素按照文档插入的时间进行排序。

图 11.4 描述了示例应用程序的集合。`LinkedList<Document>` 是包含所有 `Document` 对象的链表。图中显示了文档的标题和优先级。标题表示文档何时添加到列表中：第一个添加的文档标题为“One”，第二个文档标题为“Two”，依此类推。你可以看到文档 One 和 Four 具有相同的优先级 8，但由于 One 在 Four 之前添加，所以它在列表中更早。

![](img/3d365b72b289213a91ade7eb366b8f35_416_0.png)

#### 图 11.4

当新文档添加到链表时，它们应被添加到具有相同优先级的最后一个文档之后。`LinkedList<Document>` 集合包含 `LinkedListNode<Document>` 类型的元素。`LinkedListNode<T>` 类添加了 `Next` 和 `Previous` 属性，用于从一个节点移动到下一个节点。为了引用这些元素，`List<T>` 被定义为 `List<LinkedListNode<Document>>`。为了快速访问每个优先级的最后一个文档，集合 `List<LinkedListNode>` 最多包含 10 个元素，每个元素引用每个优先级的最后一个文档。在接下来的讨论中，对每个优先级最后一个文档的引用被称为优先级节点。

使用前面的示例，`Document` 类被扩展为包含优先级，该优先级通过类的构造函数设置（代码文件 `LinkedListSample/Document.cs`）：

```csharp
public class Document
{
    public string Title { get; private set; }
    public string Content { get; private set; }
    public byte Priority { get; private set; }

    public Document(string title, string content, byte priority)
    {
        Title = title;
        Content = content;
        Priority = priority;
    }
}
```

解决方案的核心是 `PriorityDocumentManager` 类。这个类非常易于使用。通过该类的公共接口，可以添加新的 `Document` 元素到链表中，检索第一个文档，并且出于测试目的，它还有一个方法可以显示集合中所有元素在链表中是如何链接的。

`PriorityDocumentManager` 类包含两个集合。类型为 `LinkedList<Document>` 的集合包含所有文档。类型为 `List<LinkedListNode<Document>>` 的集合包含多达 10 个元素的引用，这些元素是添加特定优先级新文档的入口点。两个集合变量都在 `PriorityDocumentManager` 类的构造函数中初始化。列表集合也用 `null` 初始化（代码文件 `LinkedListSample/PriorityDocumentManager.cs`）：

```csharp
public class PriorityDocumentManager
{
    private readonly LinkedList<Document> _documentList;

    // priorities 0-9
    private readonly List<LinkedListNode<Document>> _priorityNodes;

    public PriorityDocumentManager()
    {
        _documentList = new LinkedList<Document>();

        _priorityNodes = new List<LinkedListNode<Document>>(10);
        for (int i = 0; i < 10; i++)
        {
            _priorityNodes.Add(new LinkedListNode<Document>(null));
        }
    }
}
```

该类的公共接口的一部分是 `AddDocument` 方法。`AddDocument` 只调用私有方法 `AddDocumentToPriorityNode`。将实现放在另一个方法中的原因是 `AddDocumentToPriorityNode` 可能会被递归调用，这一点你很快就会看到：

```csharp
public void AddDocument(Document d)
{
    if (d == null) throw new ArgumentNullException("d");

    AddDocumentToPriorityNode(d, d.Priority);
}
```

`AddDocumentToPriorityNode` 实现中首先要做的操作是检查优先级是否在允许的优先级范围内。这里允许的范围是 0 到 9。如果传入了错误的值，则会抛出 `ArgumentException` 类型的异常。

接下来，你需要检查是否已存在一个与传入优先级相同的优先级节点。如果列表集合中没有这样的优先级节点，则会以递减的优先级值递归调用 `AddDocumentToPriorityNode`，以检查下一个较低优先级的节点是否存在。

如果既不存在相同优先级的节点，也不存在任何较低优先级的节点，则可以通过调用 `AddLast` 方法安全地将文档添加到链表的末尾。此外，该链表节点会被负责该文档优先级的优先级节点引用。

如果已存在一个优先级节点，你可以获取文档应插入的链表位置。在下面的示例中，你必须确定是否已存在一个具有正确优先级的优先级节点，或者是否只是一个引用较低优先级文档的优先级节点。在第一种情况下，你可以在优先级节点引用的位置之后插入新文档。因为优先级节点必须始终引用具有特定优先级的最后一个文档，所以必须设置优先级节点的引用。如果只存在一个引用较低优先级文档的优先级节点，情况会更复杂。在这种情况下，必须在所有与优先级节点具有相同优先级的文档之前插入该文档。为了找到具有相同优先级的第一个文档，`while` 循环使用 `Previous` 属性遍历所有链表节点，直到到达一个具有不同优先级的链表节点。这样，你就知道了文档必须插入的位置，并且可以设置优先级节点：

```csharp
private void AddDocumentToPriorityNode(Document doc, int priority)
{
    if (priority > 9 || priority < 0)
        throw new ArgumentException("Priority must be between 0 and 9");
    if (_priorityNodes[priority].Value == null)
    {
        --priority;
        if (priority <= 0)
        {
            // check for the next lower priority
            AddDocumentToPriorityNode(doc, priority);
        }
        else // now no priority node exists with the same priority or lower
        {
            // add the new document to the end
            _documentList.AddLast(doc);
            _priorityNodes[doc.Priority] = _documentList.Last;
        }
        return;
    }
    else // a priority node exists
    {
        LinkedListNode<Document> prioNode = _priorityNodes[priority];
        if (priority == doc.Priority)
            // priority node with the same priority exists
        {
            _documentList.AddAfter(prioNode, doc);
            // set the priority node to the last document with the same priority
            _priorityNodes[doc.Priority] = prioNode.Next;
        }
        else // only priority node with a lower priority exists
        {
            // get the first node of the lower priority
            LinkedListNode<Document> firstPrioNode = prioNode;
            while (firstPrioNode.Previous != null &&
                firstPrioNode.Previous.Value.Priority ==
            prioNode.Value.Priority)
            {
                firstPrioNode = prioNode.Previous;
                prioNode = firstPrioNode;
            }
            _documentList.AddBefore(firstPrioNode, doc);
            // set the priority node to the new value
            _priorityNodes[doc.Priority] = firstPrioNode.Previous;
        }
    }
}
```

现在只剩下简单的方法需要讨论。`DisplayAllNodes` 使用 `foreach` 循环将每个文档的优先级和标题显示到控制台。

`GetDocument` 方法从链表中返回第一个文档（优先级最高的文档），并将其从列表中移除：

```
public void DisplayAllNodes()
{
    foreach (Document doc in documentList)
    {
        WriteLine($"priority: {doc.Priority}, title {doc.Title}");
    }
}

// returns the document with the highest priority
// (that's first in the linked list)
public Document GetDocument()
{
    Document doc = _documentList.First.Value;
    _documentList.RemoveFirst();
    return doc;
}
```

在 `Main` 方法中，使用 `PriorityDocumentManager` 来演示其功能。向链表中添加八个具有不同优先级的新文档，然后显示完整列表（代码文件 `LinkedListSample/Program.cs`）：

```
public static void Main()
{
    var pdm = new PriorityDocumentManager();
    pdm.AddDocument(new Document("one","Sample", 8));
    pdm.AddDocument(new Document("two","Sample", 3));
    pdm.AddDocument(new Document("three","Sample", 4));
    pdm.AddDocument(new Document("four","Sample", 8));
    pdm.AddDocument(new Document("five","Sample", 1));
    pdm.AddDocument(new Document("six","Sample", 9));
    pdm.AddDocument(new Document("seven","Sample", 1));
    pdm.AddDocument(new Document("eight","Sample", 1));

    pdm.DisplayAllNodes();
}
```

通过处理结果，您可以看到文档首先按优先级排序，其次按文档添加的时间排序：

```
priority: 9, title six
priority: 8, title one
priority: 8, title four
priority: 4, title three
priority: 3, title two
priority: 1, title five
priority: 1, title seven
priority: 1, title eight
```

### 排序列表
