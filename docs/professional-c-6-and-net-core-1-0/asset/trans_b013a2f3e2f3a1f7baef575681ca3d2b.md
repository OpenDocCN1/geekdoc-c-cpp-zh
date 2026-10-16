
错误应尽可能早地被检测到。使用泛型类 `List<T>` 时，泛型类型 T 定义了允许的类型。若定义为 `List<int>`，则只有整数类型可以添加到集合中。编译器不会编译以下代码，因为 `Add` 方法的参数无效：

```
var list = new List<int>();
list.Add(44);
list.Add("mystring");    // compile time error
list.Add(new MyClass());    // compile time error
```

## 二进制代码复用

泛型能够实现更好的二进制代码复用。一个泛型类可以只定义一次，并可用许多不同的类型进行实例化。与 C++ 模板不同，无需访问源代码。

例如，这里将 `System.Collections.Generic` 命名空间中的 `List<T>` 类分别用 `int`、`string` 和 `MyClass` 类型实例化：

```
var list = new List<int>();
list.Add(44);

var stringList = new List<string>();
stringList.Add("mystring");

var myClassList = new List<MyClass>();
myClassList.Add(new MyClass());
```

泛型类型可以用一种语言定义，并从任何其他 .NET 语言中使用。

## 代码膨胀

你可能想知道，当使用不同的具体类型实例化泛型时，会生成多少代码。由于泛型类定义会进入程序集，使用具体类型实例化泛型类不会在 IL 代码中复制这些类。然而，当泛型类由 JIT 编译器编译为本地代码时，每种特定值类型都会创建一个新类。引用类型则共享相同本地类的同一实现。这是因为对于引用类型，在泛型实例化类中仅需要 4 字节内存地址（在 32 位系统中）来引用引用类型。而值类型包含在泛型实例化类的内存中；由于每种值类型可能有不同的内存需求，因此每种值类型都会实例化一个新类。

## 命名指南

如果在程序中使用泛型，那么能够区分泛型类型和非泛型类型会很有帮助。以下是泛型类型的命名指南：

- 使用字母 T 作为泛型类型名称的前缀。
- 如果泛型类型没有特殊要求，可以被任何类替换，并且只使用一个泛型类型，那么字符 T 作为泛型类型名称就很合适：

  ```
  public class List<T> { }
  public class LinkedList<T> { }
  ```

- 如果泛型类型有特殊要求（例如，它必须实现某个接口或派生自某个基类），或者使用了两个或更多泛型类型，请为这些类型名称使用描述性名称：

  ```
  public delegate void EventHandler<TEventArgs>(object sender, TEventArgs e);
  public delegate TOutput Converter<TInput, TOutput>(TInput from);
  public class SortedList<TKey, TValue> { }
  ```

## 创建泛型类

本节示例从一个普通的、非泛型的简化链表类开始，该类可以包含任意类型的对象，然后将此类转换为泛型类。

在链表中，一个元素引用下一个元素。因此，必须创建一个类，将对象包装在链表中并引用下一个对象。`LinkedListNode` 类包含一个名为 `Value` 的属性，该属性由构造函数初始化。除此之外，`LinkedListNode` 类还包含对列表中下一个和上一个元素的引用，可通过属性访问（代码文件 LinkedListObjects/LinkedListNode.cs）：

```
public class LinkedListNode
{
    public LinkedListNode(object value)
    {
        Value = value;
    }

    public object Value { get; private set; }

    public LinkedListNode Next { get; internal set; }
    public LinkedListNode Prev { get; internal set; }
}
```

`LinkedList` 类包含类型为 `LinkedListNode` 的 `First` 和 `Last` 属性，用于标记链表的开头和结尾。`AddLast` 方法将新元素添加到链表末尾。首先，创建一个 `LinkedListNode` 类型的对象。如果链表为空，则 `First` 和 `Last` 属性被设置为该新元素；否则，新元素作为最后一个元素添加到链表中。通过实现 `GetEnumerator` 方法，可以使用 `foreach` 语句遍历链表。`GetEnumerator` 方法利用 `yield` 语句创建枚举器类型：

```
public class LinkedList: IEnumerable
{
    public LinkedListNode First { get; private set; }
    public LinkedListNode Last { get; private set; }

    public LinkedListNode AddLast(object node)
    {
        var newNode = new LinkedListNode(node);
        if (First == null)
        {
            First = newNode;
            Last = First;
        }
        else
        {
            LinkedListNode previous = Last;
            Last.Next = newNode;
            Last = newNode;
            Last.Prev = previous;
        }
        return newNode;
    }

    public IEnumerator GetEnumerator()
    {
        LinkedListNode current = First;
        while (current != null)
        {
            yield return current.Value;
            current = current.Next;
        }
    }
}
```

> 注意：`yield` 语句为枚举器创建了一个状态机。该语句将在第 7 章“数组和元组”中说明。

现在你可以使用 `LinkedList` 类处理任何类型。以下代码片段实例化了一个新的 `LinkedList` 对象，并添加了两个整数类型和一个字符串类型。当整数类型转换为 `object` 时，会发生装箱（boxing），如本章前面所述。使用 `foreach` 语句时会发生拆箱（unboxing）。在 `foreach` 语句中，列表中的元素被强制转换为整数，因此列表中的第三个元素会导致运行时异常，因为转换为 `int` 失败（代码文件 LinkedListObjects/Program.cs）：

```
var list1 = new LinkedList();
list1.AddLast(2);
list1.AddLast(4);
list1.AddLast("6");

foreach (int i in list1)
{
    WriteLine(i);
}
```

现在制作链表的泛型版本。泛型类的定义方式与普通类类似，但带有泛型类型声明。然后，你可以在类中将泛型类型用作字段成员或方法的参数类型。`LinkedListNode` 类使用泛型类型 T 声明。现在 `Value` 属性的类型是 T 而不是 `object`；构造函数也改为接受类型为 T 的对象。泛型类型也可以被返回和设置，因此 `Next` 和 `Prev` 属性现在为 `LinkedListNode<T>` 类型（代码文件 LinkedListSample/LinkedListNode.cs）：

```
public class LinkedListNode<T>
{
    public LinkedListNode(T value)
    {
        Value = value;
    }

    public T Value { get; private set; }
    public LinkedListNode<T> Next { get; internal set; }
    public LinkedListNode<T> Prev { get; internal set; }
}
```

在下面的代码中，`LinkedList` 类也被改为泛型类。`LinkedList<T>` 包含 `LinkedListNode<T>` 元素。来自 `LinkedList` 的类型 T 定义了 `First` 和 `Last` 属性的类型 T。`AddLast` 方法现在接受类型为 T 的参数，并实例化一个 `LinkedListNode<T>` 对象。

除了 `IEnumerable` 接口之外，还有一个泛型版本：`IEnumerable<T>`。`IEnumerable<T>` 派生自 `IEnumerable`，并添加了返回 `IEnumerator<T>` 的 `GetEnumerator` 方法。`LinkedList<T>` 实现了泛型接口 `IEnumerable<T>`（代码文件 LinkedListSample/LinkedList.cs）：

> 注意：枚举器以及 `IEnumerable` 和 `IEnumerator` 接口将在第 7 章讨论。

```
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
            LinkedListNode<T> previous = Last;
            Last.Next = newNode;
            Last = newNode;
        }
    }
}
```
