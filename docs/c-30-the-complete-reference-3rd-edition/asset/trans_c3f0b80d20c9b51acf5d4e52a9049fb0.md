
```csharp
cost = c;
onhand = h;
}

public override string ToString() {
    return
        String.Format("{0,-10}Cost: {1,6:C}   On hand: {2}",
            name, cost, onhand);
}

class TypeSafeInventoryList {
    static void Main() {
        List<Inventory> inv = new List<Inventory>();

        // Add elements to the list.
        inv.Add(new Inventory("Pliers", 5.95, 3));
        inv.Add(new Inventory("Wrenches", 8.29, 2));
        inv.Add(new Inventory("Hammers", 3.50, 4));
        inv.Add(new Inventory("Drills", 19.88, 8));

        Console.WriteLine("Inventory list:");
        foreach(Inventory i in inv) {
            Console.WriteLine("  " + i);
        }
    }
}
```

在这个版本中，请注意唯一真正的区别是将 Inventory 类型作为类型实参传递给了 `List<T>`。除此之外，这两个程序几乎完全相同。使用泛型集合几乎不需要额外的工作，并且增加了类型安全性，这一事实有力地支持了在集合中存储特定类型对象时使用它。

总的来说，关于前面的程序还有一点需要注意：两个程序都很简短。当你考虑到每个程序用不到 40 行代码就建立了一个可以存储、检索和处理库存信息的动态数组时，集合的强大之处就开始显现了。大多数读者都知道，如果所有这些功能都必须手工编码，那么程序的长度将是原来的好几倍。集合为各种各样的编程问题提供了现成的解决方案。只要情况允许，就应该使用它们。

前面的程序有一个可能不明显的限制：集合无法排序。原因在于 ArrayList 和 `List<T>` 都没有办法比较两个 Inventory 对象。有两种方法可以解决这个问题。首先，Inventory 可以实现 IComparable 接口。该接口定义了如何比较一个类的两个对象。其次，当需要比较时，可以指定一个 IComparer 对象。下面的章节将说明这两种方法。

## 实现 IComparable

如果要对包含用户定义对象的集合进行排序（或者要将这些对象存储到像 SortedList 这样按排序顺序维护元素的集合中），那么集合必须知道如何比较这些对象。一种实现方式是

```csharp
    return name.CompareTo(b.name);
  }
}

class IComparableDemo {
  static void Main() {
    ArrayList inv = new ArrayList();

    // Add elements to the list.
    inv.Add(new Inventory("Pliers", 5.95, 3));
    inv.Add(new Inventory("Wrenches", 8.29, 2));
    inv.Add(new Inventory("Hammers", 3.50, 4));
    inv.Add(new Inventory("Drills", 19.88, 8));

    Console.WriteLine("Inventory list before sorting:");
    foreach(Inventory i in inv) {
      Console.WriteLine("    " + i);
    }
    Console.WriteLine();

    // Sort the list.
    inv.Sort();

    Console.WriteLine("Inventory list after sorting:");
    foreach(Inventory i in inv) {
      Console.WriteLine("    " + i);
    }
  }
}
```

下面是输出结果。请注意，调用 `Sort()` 之后，库存按名称排序。

```text
Inventory list before sorting:
    Pliers    Cost: $5.95  On hand: 3
    Wrenches  Cost: $8.29  On hand: 2
    Hammers   Cost: $3.50  On hand: 4
    Drills    Cost: $19.88 On hand: 8

Inventory list after sorting:
    Drills    Cost: $19.88 On hand: 8
    Hammers   Cost: $3.50  On hand: 4
    Pliers    Cost: $5.95  On hand: 3
    Wrenches  Cost: $8.29  On hand: 2
```

### 为泛型集合实现 `IComparable<T>`

如果要对存储在泛型集合中的对象进行排序，那么需要实现 **`IComparable<T>`**。该版本定义了 **`CompareTo()`** 的泛型形式，如下所示：

```csharp
int CompareTo(T obj)
```

**`CompareTo()`** 会将调用对象与 *obj* 进行比较。要按升序排序，如果对象相等，实现必须返回零；如果调用对象大于 *obj*，则返回正值；如果调用对象小于 *obj*，则返回负值。要按降序排序，则反转比较的结果。在实现 **`IComparable<T>`** 时，通常会将实现类的类型名称作为类型实参传递。

下面的示例对前面的程序进行了改造，使其使用 **`IComparable<T>`**。注意它使用的是泛型 **`List<T>`** 集合，而不是非泛型 **`ArrayList`**。

```csharp
// Implement IComparable<T>.

using System;
using System.Collections.Generic;

// Implement the generic IComparable<T> interface.
class Inventory : IComparable<Inventory> {
    string name;
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

    // Implement the IComparable<T> interface.
    public int CompareTo(Inventory obj) {
        return name.CompareTo(obj.name);
    }
}

class GenericIComparableDemo {
    static void Main() {
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

        // Sort the list.
        inv.Sort();

        Console.WriteLine("Inventory list after sorting:");
        foreach (Inventory i in inv) {
            Console.WriteLine("  " + i);
        }
    }
}
```

该程序产生的输出与之前的非泛型版本相同。

## 使用 IComparer

尽管为你创建的类实现 IComparable 通常是让这些类的对象能够被排序的最简单方法，但你也可以通过使用 IComparer 以不同的方式解决这个问题。要使用 IComparer，首先创建一个实现 IComparer 的类，然后在需要比较时指定该类的对象。

IComparer 有两个版本：泛型和非泛型。虽然它们的使用方式相似，但存在一些细微差别，下面将分别讨论这两种方式。

### 使用非泛型 IComparer

非泛型 IComparer 只定义了一个方法 Compare()，如下所示：

```csharp
int Compare(object obj1, object obj2)
```

Compare() 会比较 obj1 和 obj2。要按升序排序，如果对象相等，实现必须返回零；如果 obj1 大于 obj2，则返回正值；如果 obj1 小于 obj2，则返回负值。可以通过反转比较的结果来按降序排序。如果 obj 的类型与调用对象不兼容，无法进行比较，该方法可能会抛出 ArgumentException。

在构造 SortedList、调用 ArrayList.Sort(IComparer) 以及集合类中的其他各种位置，都可以指定 IComparer。使用 IComparer 的主要优点是，你可以对未实现 IComparable 的类的对象进行排序。

下面的程序对非泛型库存程序进行了改造，使其使用 IComparer 对库存列表进行排序。它首先创建了一个名为 CompInv 的类，该类实现 IComparer 并比较两个 Inventory 对象。然后，在调用 Sort() 对库存列表排序时，使用了该类的对象。

```csharp
// Use IComparer.

using System;
using System.Collections;

// Create an IComparer for Inventory objects.
class CompInv : IComparer {
    // Implement the IComparer interface.
    public int Compare(object obj1, object obj2) {
        Inventory a, b;
        a = (Inventory) obj1;
        b = (Inventory) obj2;
        return a.name.CompareTo(b.name);
    }
}
```
