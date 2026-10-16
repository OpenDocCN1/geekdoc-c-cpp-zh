

```
Last.Prev = previous;
}
return newNode;
}

public IEnumerator<T> GetEnumerator()
{
    LinkedListNode<T> current = First;

    while (current != null)
    {
        yield return current.Value;
        current = current.Next;
    }
}

IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();
}
```

使用泛型 `LinkedList<T>`，可以用 `int` 类型实例化它，并且不会发生装箱。另外，如果使用 `AddLast` 方法时没有传入 `int`，编译器会报错。使用泛型 `IEnumerable<T>`，`foreach` 语句也是类型安全的，如果 `foreach` 语句中的变量不是 `int`，编译器会报错（代码文件 `LinkedListSample/Program.cs`）：

```
var list2 = new LinkedList<int>();
list2.AddLast(1);
list2.AddLast(3);
list2.AddLast(5);

foreach (int i in list2)
{
    WriteLine(i);
}
```

类似地，你可以将泛型 `LinkedList<T>` 与 `string` 类型一起使用，并向 `AddLast` 方法传递字符串：

```
var list3 = new LinkedList<string>();
list3.AddLast("2");
list2.AddLast("four");
list3.AddLast("foo");

foreach (string s in list3)
{
    WriteLine(s);
}
```

> 注意 每个处理 object 类型的类都可能是泛型实现的候选者。此外，如果类使用了层次结构，泛型对于避免强制转换非常有帮助。

## 泛型特性

创建泛型类时，可能需要一些额外的 C# 关键字。如果泛型类型不需要 `Object` 类的功能，但你又需要在泛型类中调用某些特定方法，则可以定义约束。

本节讨论以下主题：

- 默认值
- 约束
- 继承
- 静态成员

此示例从一个泛型文档管理器开始，用于从队列中读取文档以及向队列写入文档。首先创建一个名为 `DocumentManager` 的新控制台项目，并添加 `DocumentManager<T>` 类。`AddDocument` 方法将文档添加到队列中。如果队列不为空，只读属性 `IsDocumentAvailable` 返回 true（代码文件 `DocumentManager/DocumentManager.cs`）：

> **注意** *使用 .NET Core 时，此示例需要引用 NuGet 包* `System.Collections`。

```
using System;
using System.Collections.Generic;

namespace Wrox.ProCSharp.Generics
{
    public class DocumentManager<T>
    {
        private readonly Queue<T> documentQueue = new Queue<T>();

        public void AddDocument(T doc)
        {
            lock (this)
            {
                documentQueue.Enqueue(doc);
            }
        }

        public bool IsDocumentAvailable => documentQueue.Count > 0;
    }
}
```

线程和 lock 语句将在第 21 章“任务与并行编程”和第 22 章“任务同步”中讨论。

### 默认值

现在你向 `DocumentManager<T>` 类中添加一个 `GetDocument` 方法。在此方法内部，类型 `T` 应被赋值为 `null`。然而，不能将 `null` 赋给泛型类型。这是因为泛型类型也可以实例化为值类型，而 `null` 只允许用于引用类型。要避免此问题，可以使用 default 关键字。使用 default 关键字时，null 被赋给引用类型，0 被赋给值类型：

```
public T GetDocument()
{
    T doc = default(T);
    lock (this)
    {
        doc = documentQueue.Dequeue();
    }
    return doc;
}
```

> 注意 default 关键字根据上下文具有多种含义。switch 语句使用 default 来定义默认分支，而在泛型中，default 用于将泛型类型初始化为 null 或 0，具体取决于它是引用类型还是值类型。

### 约束

如果泛型类需要调用泛型类型的某些方法，你必须添加约束。

在 DocumentManager<T> 中，所有文档标题都应在 DisplayAllDocuments 方法中显示。Document 类实现了具有 Title 和 Content 属性的 IDocument 接口（代码文件 DocumentManager/Document.cs）：

```
public interface IDocument
{
    string Title { get; set; }
    string Content { get; set; }
}
```

```
public class Document: IDocument
{
    public Document()
    {
    }

    public Document(string title, string content)
    {
        Title = title;
        Content = content;
    }

    public string Title { get; set; }
    public string Content { get; set; }
}
```

要使用 DocumentManager<T> 类显示文档，你可以将类型 T 强制转换为 IDocument 接口以显示标题（代码文件 DocumentManager/DocumentManager.cs）：

```
public void DisplayAllDocuments()
{

foreach (T doc in documentQueue)
{
    WriteLine(((IDocument)doc).Title);
}
}
```

这里的问题是，如果类型 T 没有实现 IDocument 接口，进行强制转换会导致运行时异常。更好的做法是使用 DocumentManager<TDocument> 类定义一个约束，指定类型 TDocument 必须实现 IDocument 接口。为了在泛型类型名称中明确这一要求，将 T 改为 TDocument。where 子句定义了实现 IDocument 接口的要求：

```
public class DocumentManager<TDocument>
    where TDocument: IDocument
{
```

> 注意 为泛型类型添加约束时，最好在泛型参数名称中包含一些信息。示例代码现在使用 TDocument 而不是 T 作为泛型参数。对于编译器来说，参数名称并不重要，但更具可读性。

这样，你就可以编写 foreach 语句，使得 TDocument 类型包含 Title 属性。你将获得 Visual Studio IntelliSense 和编译器的支持：

```
public void DisplayAllDocuments()
{
    foreach (TDocument doc in documentQueue)
    {
        WriteLine(doc.Title);
    }
}
```

在 Main 方法中，使用实现了所需 IDocument 接口的 Document 类型实例化 DocumentManager<TDocument> 类。然后添加并显示新文档，并检索其中一个文档（代码文件 DocumentManager/Program.cs）：

```
public static void Main()
{
    var dm = new DocumentManager<Document>();
    dm.AddDocument(new Document("Title A","Sample A"));
    dm.AddDocument(new Document("Title B","Sample B"));

    dm.DisplayAllDocuments();

    if (dm.IsDocumentAvailable)
    {
        Document d = dm.GetDocument();
        WriteLine(d.Content);
    }
}
```

现在，DocumentManager 可以与任何实现 IDocument 接口的类一起使用。

在示例应用程序中，你已经看到了接口约束。泛型支持多种约束类型，如下表所示。

| 约束 | 说明 |
|---|---|
| where T: struct | struct 约束要求类型 T 必须是值类型。 |
| where T: class | class 约束表示类型 T 必须是引用类型。 |
| where T: IFoo | 指定类型 T 必须实现接口 IFoo。 |
| where T: Foo | 指定类型 T 必须派生自基类 Foo。 |
| where T: new() | 构造函数约束；指定类型 T 必须具有默认构造函数。 |
| where T1: T2 | 使用约束还可以指定类型 T1 派生自泛型类型 T2。 |

> 注意 构造函数约束只能为默认构造函数定义，不能为其他构造函数定义构造函数约束。

对于泛型类型，你还可以组合多个约束。MyClass<T> 声明中的约束 where T: IFoo, new() 指定类型 T 实现接口 IFoo 并具有默认构造函数：

```
public class MyClass<T>
    where T: IFoo, new()
{
    //...
```

> 注意 关于 C# 的 where 子句，一个重要限制是：无法定义必须由泛型类型实现的运算符。运算符不能在接口中定义。使用 where 子句只能定义基类、接口和默认构造函数。

### 继承

前面创建的 LinkedList<T> 类实现了 IEnumerable<T> 接口：

```
public class LinkedList<T>: IEnumerable<T>
{
    //...
```

