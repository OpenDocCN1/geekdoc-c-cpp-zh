
例如，来看 IDisposable。如果一个类想要公开声明它实现了 Dispose() 方法，它必须实现 IDisposable —— 在 C# 术语中，这意味着该类派生自 IDisposable。

```csharp
class SomeClass: IDisposable
{
    // This class MUST contain an implementation of the
    // IDisposable.Dispose() method, otherwise
    // you get a compilation error.
    public void Dispose()
    {
        // implementation of Dispose() method
    }
    // rest of class
}
```

在此示例中，如果 SomeClass 派生自 IDisposable 但不包含与 IDisposable 中定义完全相同的签名的 Dispose() 实现，就会得到编译错误，因为该类违反了其同意实现 IDisposable 的契约。当然，编译器对于一个类拥有 Dispose() 方法但未派生自 IDisposable 并没有问题。问题在于，其他代码将无法识别 SomeClass 已同意支持 IDisposable 功能。

![](img/d7d2ffa0a76feaab821930e95daace93_162_0.png)

## 定义和实现接口

本节通过开发一个遵循接口继承范式的简短程序来说明如何定义和使用接口。示例基于银行账户。假设您正在编写最终将允许银行账户之间进行计算机化转账的代码。并且假设在本示例中，可能有许多公司实现银行账户，但它们已相互约定，任何代表银行账户的类都将实现一个接口 IBankAccount，该接口公开存款或取款的方法，以及一个返回余额的属性。正是通过此接口，外部代码才能识别由不同银行账户实现的各种银行账户类。虽然目标是允许银行账户相互通信以在账户之间转账资金，但我们暂时不会引入该功能。

为了保持简单，您将把示例的所有代码保留在同一个源文件中。当然，如果像示例这样的东西在现实生活中使用，您可以推断不同的银行账户类不仅会被编译到不同的程序集中，而且还会被托管在不同银行拥有的不同机器上。这对于我们的目的来说太复杂了。然而，为了保持一定的真实性，您将为不同的公司定义不同的命名空间。

首先，您需要定义 IBankAccount 接口：

```csharp
namespace Wrox.ProCSharp
{
    public interface IBankAccount
    {
        void PayIn(decimal amount);
        bool Withdraw(decimal amount);
        decimal Balance
        {
            get;
        }
    }
}
```

类型为 T。泛型类型也可以被返回和设置，因此属性 Next 和 Prev 现在的类型为 LinkedListNode<T>：

```csharp
public class LinkedListNode<T>
{
    public LinkedListNode(T value)
    {
        this.Value = value;
    }

    public T Value { get; private set; }
    public LinkedListNode<T> Next { get; internal set; }
    public LinkedListNode<T> Prev { get; internal set; }
}
```

代码片段 LinkedListSample\LinkedListNode.cs

在下面的代码中，类 LinkedList 也被更改为泛型类。LinkedList<T> 包含 LinkedListNode<T> 元素。LinkedList 中的类型 T 定义了属性 First 和 Last 的类型 T。方法 AddLast() 现在接受类型为 T 的参数并实例化一个 LinkedListNode<T> 对象。除了接口 IEnumerable 之外，还有一个泛型版本：IEnumerable<T>。IEnumerable<T> 派生自 IEnumerable 并添加了返回 IEnumerator<T> 的 GetEnumerator() 方法。LinkedList<T> 实现泛型接口 IEnumerable<T>。

![](img/d7d2ffa0a76feaab821930e95daace93_173_0.png)

```csharp
public class LinkedList<T>: IEnumerable<T>
{
    public LinkedListNode<T> First { get; private set; }
    public LinkedListNode<T> Last { get; private set; }

    public LinkedListNode<T> AddLast(T node)
    {
        var newNode = new LinkedListNode<T>(node);
        if (First == null)
        {
            First = newNode;
            Last = First;
        }
        else
        {
            Last.Next = newNode;
            Last = newNode;
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
```

让我们从一个泛型文档管理器开始示例。文档管理器用于从队列读取和写入文档。首先创建一个名为 DocumentManager 的新控制台项目并添加类 DocumentManager<T>。方法 AddDocument() 将文档添加到队列。只读属性 IsDocumentAvailable 如果队列不为空则返回 true：

```csharp
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

        public bool IsDocumentAvailable
        {
            get { return documentQueue.Count > 0; }
        }
    }
}
```

代码片段 DocumentManager/DocumentManager.cs

## 默认值

现在向 DocumentManager<T> 类添加一个 GetDocument() 方法。在此方法内部，类型 T 应该被赋值为 null。然而，不可能将 null 分配给泛型类型。原因是泛型类型也可以实例化为值类型，而 null 仅允许用于引用类型。为规避此问题，您可以使用 default 关键字。使用 default 关键字，会将 null 分配给引用类型，将 0 分配给值类型：

```csharp
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

> default 关键字根据使用上下文具有多种含义。switch 语句使用 default 来定义默认情况，而在泛型中，default 用于将泛型类型初始化为 null 或 0，具体取决于它是引用类型还是值类型。

## 约束

如果泛型类需要调用泛型类型的某些方法，您必须添加约束。

## 继承

之前创建的 LinkedList<T> 类实现了接口 IEnumerable<out T>：

```csharp
public class LinkedList<T>: IEnumerable<T>
{
    //...
}
```

泛型类型可以实现泛型接口。通过从类派生也可以实现同样的功能。泛型类可以从泛型基类派生：

```csharp
public class Base<T>
{
}

public class Derived<T>: Base<T>
{
}
```

要求是必须重复接口的泛型类型，或指定基类的类型，如本例所示：

```csharp
public class Base<T>
{
}

public class Derived<T>: Base<string>
{
}
```

这样，派生类可以是泛型类或非泛型类。例如，您可以定义一个抽象泛型基类，并在派生类中使用具体类型实现它。这允许您对特定类型进行特化：

```csharp
public abstract class Calc<T>
{
    public abstract T Add(T x, T y);
    public abstract T Sub(T x, T y);
}

public class IntCalc: Calc<int>
{
    public override int Add(int x, int y)
    {
        return x + y;
    }

    public override int Sub(int x, int y)
    {
        return x - y;
    }
}
```

## 静态成员

泛型类的静态成员需要特别注意。泛型类的静态成员仅与类的一个实例化共享。让我们看一个示例，其中类 StaticDemo<T> 包含静态字段 x：

```csharp
public class StaticDemo<T>
{
    public static int x;
}
```
