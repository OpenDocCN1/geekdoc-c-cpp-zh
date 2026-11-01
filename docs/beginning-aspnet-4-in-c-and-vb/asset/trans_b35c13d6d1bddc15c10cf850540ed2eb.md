
DocumentManager 类是 Queue<T> 类的薄封装层。DocumentManager 类定义了如何处理文档：通过 AddDocument() 方法将文档添加到队列，通过 GetDocument() 方法从队列获取文档。

在 AddDocument() 方法内部，使用 Enqueue() 方法将文档添加到队列末尾。在 GetDocument() 内部，使用 Dequeue() 方法从队列中读取第一个文档。由于多个线程可以并发访问 DocumentManager，因此使用 lock 语句锁定对队列的访问。

> 关于线程和 lock 语句将在第 20 章“线程、任务和同步”中讨论。

IsDocumentAvailable 是一个只读布尔属性，如果队列中有文档则返回 true，否则返回 false：

```csharp
public class DocumentManager
{
    private readonly Queue<Document> documentQueue = new Queue<Document>();

    public void AddDocument(Document doc)
    {
        lock (this)
        {
            documentQueue.Enqueue(doc);
        }
    }

    public Document GetDocument()
    {
        Document doc = null;
        lock (this)
        {
            doc = documentQueue.Dequeue();
        }
        return doc;
    }

    public bool IsDocumentAvailable
    {
        get
        {
            return documentQueue.Count > 0;
        }
    }
}
```

代码片段 QueueSample/DocumentManager.cs

ProcessDocuments 类在单独的线程中处理队列中的文档。唯一可以从外部访问的方法是 Start()。在 Start() 方法中，实例化一个新线程。为了启动线程，创建一个 ProcessDocuments 对象，并将 Run() 方法定义为线程的启动方法。ThreadStart 是一个委托，它引用要由线程启动的方法。创建 Thread 对象后，通过调用 Thread.Start() 方法启动线程。

使用 ProcessDocuments 类的 Run() 方法定义了一个无限循环。在此循环中，使用 IsDocumentAvailable 属性来查看队列中是否有文档。如果队列中有一个文档

```csharp
{
    Console.Write(item);
}
Console.WriteLine();
```

因为项的顺序是从最后添加的读取到最先添加的，所以产生了以下结果：

CBA

使用枚举器读取项不会更改项的状态。使用 Pop() 方法时，每个被读取的项也会从堆栈中移除。这样，您可以使用 while 循环遍历集合，并通过 Count 属性验证是否仍有项存在：

```csharp
var alphabet = new Stack<char>();
alphabet.Push('A');
alphabet.Push('B');
alphabet.Push('C');

Console.Write("First iteration: ");
foreach (char item in alphabet)
{
    Console.Write(item);
}
Console.WriteLine();

Console.Write("Second iteration: ");
while (alphabet.Count > 0)
{
    Console.Write(alphabet.Pop());
}
Console.WriteLine();
```

结果两次给出 CBA，每次迭代一次。第二次迭代后，堆栈为空，因为第二次迭代使用了 Pop() 方法：

First iteration: CBA
Second iteration: CBA

## 链表

LinkedList<T> 是一个双向链表，其中一个元素引用下一个元素和前一个元素，如图 10-3 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_302_0.png)

图 10-3

链表的一个优点是，如果项插入到列表中间，链表的速度非常快。插入项时，只需更改前一项的 Next 引用和下一项的 Previous 引用，使其引用插入的项。对于 List<T> 类，当插入元素时，所有后续元素都必须移动。

当然，链表也有缺点。链表的项只能一个接一个地访问。要找到列表中位于中间或末尾的某个项需要很长时间。

链表不能只存储列表中的项；连同每一项，链表还必须具有关于下一个和前一个项的信息。这就是为什么 LinkedList<T> 包含类型为 LinkedListNode<T> 的项。使用 LinkedListNode<T> 类，您可以访问列表中的下一个和前一个项。LinkedListNode<T> 类定义了属性 List、Next、Previous 和 Value。List 属性返回与该节点关联的 LinkedList<T> 对象。Next 和 Previous 用于遍历列表并访问下一个或前一个项。Value 的类型为 T。

LinkedList<T> 类本身定义了一些成员，用于访问列表的第一个（First）和最后一个（Last）项，在特定位置插入项（AddAfter()、AddBefore()、AddFirst()、AddLast()），从特定位置移除项（Remove()、RemoveFirst()、RemoveLast()），以及查找元素（搜索可以从列表的开头（Find()）或末尾（FindLast()）开始）。

用于演示链表的示例应用程序将链表与列表一起使用。链表包含与队列示例中相同的文档，但这些文档具有与之关联的额外优先级。文档将根据优先级在链表内排序。如果多个文档具有相同的优先级，则元素根据文档插入的时间进行排序。

图 10-4 描述了示例应用程序的集合。LinkedList<Document> 是包含所有 Document 对象的链表。该图显示了文档的标题和优先级。标题指示文档添加到列表的时间：第一个添加的文档的标题为“One”，第二个文档的标题为“Two”，依此类推。您可以看到文档 One 和 Four 具有相同的优先级 8，但由于 One 在 Four 之前添加，因此它在列表中更靠前。

当向链表添加新文档时，应将其添加到具有相同优先级的最后一个文档之后。LinkedList<Document> 集合包含类型为 LinkedListNode<Document> 的元素。LinkedListNode<Document> 类添加了 Next 和 Previous 属性，以便从一个节点遍历到下一个节点。为了引用此类元素，List<T> 被定义为 List<LinkedListNode<Document>>。为了快速访问每个优先级的最后一个文档，集合 List<LinkedListNode<Document>> 最多包含 10 个元素，每个元素引用每个优先级的最后一个文档。在接下来的讨论中，对每个优先级的最后一个文档的引用称为优先级节点。

在前面的示例中，Document 类被扩展为包含优先级。优先级通过类的构造函数设置：

```csharp
public class Document
{
    public string Title { get; private set; }
    public string Content { get; private set; }
    public byte Priority { get; private set; }

    public Document(string title, string content, byte priority = 0)
    {
        this.Title = title;
        this.Content = content;
        this.Priority = priority;
    }
}
```

![](img/d7d2ffa0a76feaab821930e95daace93_304_0.png)

图 10-4

解决方案的核心是 PriorityDocumentManager 类。这个类非常容易使用。通过该类的公共接口，可以将新的 Document 元素添加到链表中，可以检索第一个文档，并且为了测试目的，它还有一个方法可以显示集合中所有元素在链表中的链接方式。

PriorityDocumentManager 类包含两个集合。类型为 LinkedList<Document> 的集合包含所有文档。类型为 List<LinkedListNode<Document>> 的集合包含最多 10 个元素的引用，这些元素是添加具有特定优先级的新文档的入口点。两个集合变量都在 PriorityDocumentManager 类的构造函数中初始化。列表集合也被初始化为 null：

```csharp
public class PriorityDocumentManager
{
    private readonly LinkedList<Document> documentList;
```
