
```csharp
class Inventory {
    public string name;
    double cost;
    int onhand;

    public Inventory(string n, double c, int h) {
        name = n;
        cost = c;
        onhand = h;
    }

    public override string ToString() {
        return
            String.Format("{0,-10}Cost: {1,6:C}  On hand: {2}",
                name, cost, onhand);
    }
}

class IComparerDemo {
    static void Main() {
        CompInv comp = new CompInv();
        ArrayList inv = new ArrayList();

        // Add elements to the list.
        inv.Add(new Inventory("Pliers", 5.95, 3));
        inv.Add(new Inventory("Wrenches", 8.29, 2));
        inv.Add(new Inventory("Hammers", 3.50, 4));
        inv.Add(new Inventory("Drills", 19.88, 8));

        Console.WriteLine("Inventory list before sorting:");
        foreach (Inventory i in inv) {
            Console.WriteLine("  " + i);
        }
        Console.WriteLine();

        // Sort the list using an IComparer.
        inv.Sort(comp);

        Console.WriteLine("Inventory list after sorting:");
        foreach (Inventory i in inv) {
            Console.WriteLine("  " + i);
        }
    }
}
```

输出与程序的前一版本相同。

## 使用泛型 `IComparer<T>`

`IComparer<T>` 接口是 `IComparer` 的泛型版本。它定义了 `Compare()` 的泛型版本，如下所示：

```csharp
int Compare(T obj1, T obj2)
```

该方法比较 obj1 与 obj2，如果 obj1 大于 obj2 则返回大于零的值，如果两个对象相同则返回零，如果 obj1 小于 obj2 则返回小于零的值。

下面是前面程序的一个使用 `IComparer<T>` 的泛型版本。它产生的输出与程序的前几个版本相同。

```csharp
// Use IComparer<T>.

using System;
using System.Collections.Generic;

// Create an IComparer<T> for Inventory objects.
class CompInv<T> : IComparer<T> where T : Inventory {

    // Implement the IComparer<T> interface.
    public int Compare(T obj1, T obj2) {
        return obj1.name.CompareTo(obj2.name);
    }
}

class Inventory {
    public string name;
    double cost;
    int onhand;

    public Inventory(string n, double c, int h) {
        name = n;
        cost = c;
        onhand = h;
    }

    public override string ToString() {
        return
            String.Format("{0,-10}Cost: {1,6:C}  On hand: {2}",
                          name, cost, onhand);
    }
}

class GenericIComparerDemo {
    static void Main() {
        CompInv<Inventory> comp = new CompInv<Inventory>();
        List<Inventory> inv = new List<Inventory>();

        // Add elements to the list.
        inv.Add(new Inventory("Pliers", 5.95, 3));
        inv.Add(new Inventory("Wrenches", 8.29, 2));
        inv.Add(new Inventory("Hammers", 3.50, 4));
        inv.Add(new Inventory("Drills", 19.88, 8));

        Console.WriteLine("Inventory list before sorting:");
        foreach (Inventory i in inv) {
            Console.WriteLine("  " + i);
        }
        Console.WriteLine();

        // Sort the list using an IComparer.
        inv.Sort(comp);

        Console.WriteLine("Inventory list after sorting:");
        foreach (Inventory i in inv) {
            Console.WriteLine("  " + i);
        }
    }
}
```

## 通过枚举器访问集合

通常你会希望遍历集合中的元素。例如，你可能想显示每个元素。一种方法是使用 `foreach` 循环，如前面的示例所做的那样。另一种方法是使用枚举器。枚举器是一个实现非泛型 `IEnumerable` 或泛型 `IEnumerable<T>` 接口的对象。

`IEnumerator` 定义了一个名为 `Current` 的属性。非泛型版本如下所示：

```csharp
object Current { get; }
```

对于 `IEnumerator<T>`，`Current` 的声明如下：

```csharp
T Current { get; }
```

在两种情况下，`Current` 都会获取当前正在枚举的元素。由于 `Current` 是只读属性，因此枚举器只能用于检索集合中的对象，而不能修改它们。

`IEnumerator` 定义了两个方法。第一个是 `MoveNext()`：

```csharp
bool MoveNext()
```

每次调用 `MoveNext()` 都会将枚举器的当前位置移动到集合中的下一个元素。如果下一个元素可用，则返回 true；如果已到达集合末尾，则返回 false。在首次调用 `MoveNext()` 之前，`Current` 的值是未定义的。（从概念上讲，在首次调用 `MoveNext()` 之前，枚举器指向的是位于第一个元素之前的不存在元素。必须调用 `MoveNext()` 才能移动到第一个元素。）

可以通过调用 `Reset()` 将枚举器重置到集合的开头，如下所示：

```csharp
void Reset()
```

调用 `Reset()` 之后，枚举将再次从集合的开头开始。因此，在获取第一个元素之前，必须调用 `MoveNext()`。

在 `IEnumerator<T>` 中，方法 `MoveNext()` 和 `Reset()` 的工作方式相同。另外还有两点：第一，不能使用枚举器更改其正在枚举的集合。因此，枚举器相对于集合是只读的。第二，对正在枚举的集合的任何更改都会使枚举器失效。

## 使用枚举器

在通过枚举器访问集合之前，必须先获取一个枚举器。每个集合类都提供一个 `GetEnumerator()` 方法，该方法返回一个指向集合开头的枚举器。使用此枚举器，你可以一次一个元素地访问集合中的每个元素。通常，要使用枚举器遍历集合的内容，请遵循以下步骤：

- 1. 通过调用集合的 `GetEnumerator()` 方法，获取一个指向集合开头的枚举器。
- 2. 设置一个循环，调用 `MoveNext()`。只要 `MoveNext()` 返回 true，循环就继续迭代。
- 3. 在循环内，通过 `Current` 获取每个元素。

下面是一个实现这些步骤的示例。它使用 `ArrayList`，但一般原则适用于任何类型的集合，包括泛型集合。

```csharp
// Demonstrate an enumerator.

using System;
using System.Collections;

class EnumeratorDemo {
    static void Main() {
        ArrayList list = new ArrayList(1);

        for(int i=0; i < 10; i++)
            list.Add(i);

        // Use enumerator to access list.
        IEnumerator etr = list.GetEnumerator();
        while(etr.MoveNext())
            Console.Write(etr.Current + " ");

        Console.WriteLine();

        // Re-enumerate the list.
        etr.Reset();
        while(etr.MoveNext())
            Console.Write(etr.Current + " ");

        Console.WriteLine();
    }
}
```

输出如下所示：

```text
0 1 2 3 4 5 6 7 8 9
0 1 2 3 4 5 6 7 8 9
```

通常，当你需要遍历集合时，使用 **foreach** 循环比使用枚举器更方便。但是，枚举器允许你随意重置枚举器，从而为你提供了一点额外的控制。

## 使用 IDictionaryEnumerator

当使用非泛型 `IDictionary`（例如 `Hashtable`）时，遍历集合将使用 `IDictionaryEnumerator` 而不是 `IEnumerator`。`IDictionaryEnumerator` 继承 `IEnumerator` 并添加了三个属性。第一个是

```csharp
DictionaryEntry Entry { get; }
```

Entry 以 `DictionaryEntry` 结构的形式从枚举器获取下一个键/值对。回想一下，`DictionaryEntry` 定义了两个属性，名为 `Key` 和 `Value`，可用于访问条目中包含的键或值。`IDictionaryEnumerator` 定义的另外两个属性如下所示：

```csharp
object Key { get; }
object Value { get; }
```

这些属性允许你直接访问键或值。

`IDictionaryEnumerator` 的使用方式与常规枚举器类似，区别在于你将通过 `Entry`、`Key` 或 `Value` 属性而不是 `Current` 来获取当前值。因此，在获取 `IDictionaryEnumerator` 之后，必须调用 `MoveNext()` 来获取第一个元素。继续调用 `MoveNext()` 以获取集合中的其余元素。当没有更多元素时，`MoveNext()` 返回 false。

下面是一个通过 `IDictionaryEnumerator` 枚举 `Hashtable` 中元素的示例：

```csharp
// Demonstrate IDictionaryEnumerator.

using System;
using System.Collections;

class IDicEnumDemo {
    static void Main() {
        // Create a hash table.
        Hashtable ht = new Hashtable();

        // Add elements to the table.
        ht.Add("Tom", "555-3456");
        ht.Add("Mary", "555-9876");
        ht.Add("Todd", "555-3452");
        ht.Add("Ken", "555-7756");

        // Demonstrate enumerator.
        IDictionaryEnumerator etr = ht.GetEnumerator();
        Console.WriteLine("Display info using Entry.");
        while(etr.MoveNext())
            Console.WriteLine(etr.Entry.Key + ": " +
                              etr.Entry.Value);

        Console.WriteLine();

        Console.WriteLine("Display info using Key and Value directly.");
        etr.Reset();
        while(etr.MoveNext())
            Console.WriteLine(etr.Key + ": " +
                              etr.Value);
    }
}
```

输出如下所示：

