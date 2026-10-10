
图中的三个类声明说明了其工作原理。第一个类声明是用于实现 `ICloneable` 接口的 `Product` 类。第二个类声明用于实现两个接口（`ICloneable` 和 `IDisplayable`）的 `Product` 类。第三个类声明用于继承 `Product` 类并实现 `ICloneable` 和 `IDisplayable` 接口的 `Book` 类。

当你在类声明中输入接口名称时，可以为接口的每个成员生成存根（stubs）。要这样做，你可以右键点击接口名称，并从生成的菜单中选择“实现接口”（`Implement Interface`）命令。然后，与图中倒数第二个示例中类似的代码将被插入到类中。此时，你就可以开始输入实现接口每个成员所需的代码。

注意在此示例中，生成的代码被 `#region` 和 `#endregion` 指令包围。在代码编辑器（`Code Editor`）窗口中，你可以通过点击区域名称左侧的 `` 符号来折叠此类区域。或者，你也可以点击出现在折叠区域旁的 `+` 符号来展开已折叠的区域。这让你能够轻松隐藏或显示接口的所有成员。

如果你右键点击接口名称并选择“显式实现接口”（`Explicit Implement Interface`）命令，它的作用与普通的“实现接口”命令相似。但它不使用 `public` 关键字，并且对接口的每个成员进行完全限定。例如，在图中，它指定了 `IClone` 而不是指定 `Clone` 方法。虽然这在某些情况下可以帮助避免命名冲突，但你通常不需要使用此命令。

# 第 15 章 如何使用接口和泛型

## 实现接口的语法

```csharp
public class ClassName : [BaseClassName,] InterfaceName1[, InterfaceName2]...
```

## 实现 ICloneable 的 Product 类

```csharp
public class Product : ICloneable
```

## 实现两个接口的 Product 类

```csharp
public class Product : ICloneable, IDisplayable
```

## 继承一个类并实现两个接口的类

```csharp
public class Book : Product, ICloneable, IDisplayable
```

## 输入接口名称时显示的提示符

![](img/3148667e42d4db35b3d08576aaa1fa01_486_0.png)

## 实现接口时生成的代码

```csharp
#region ICloneable Members
```

```csharp
public object Clone()
{
    throw new Exception("The method or operation is not implemented.");
}
#endregion
```

## 显式实现接口时生成的代码

```csharp
#region ICloneable Members
```

```csharp
object ICloneable.Clone()
{
    throw new Exception("The method or operation is not implemented.");
}
#endregion
```

### 描述

- 要声明实现一个或多个接口的类，请在类名后输入冒号，列出该类实现的接口。
- 如果类继承了另一个类，必须在接口名称之前列出该类。
- 在类声明中输入接口名称后，可以自动为接口的成员生成存根。要这样做，可以右键点击接口名称并从生成的菜单中选择实现接口。

15-4 如何实现接口

## 实现 ICloneable 接口的 Product 类

现在你已经学习了创建和实现接口的基本技能，15-5 展示了一个实现 `IDisplayable` 和 `ICloneable` 接口的 `Product` 类。该示例与 15-1 中的示例类似。

`Product` 类首先声明了 `Code`、`Description` 和 `Price` 三个属性。然后，在构造函数之后，`GetDisplayText` 方法提供了 `IDisplayable` 接口的实现。该方法位于 Visual Studio 生成的区域内。在代码编辑器工作时，你可以折叠或展开此方法。最后，`Clone` 方法创建一个新产品，将当前产品的 `Code`、`Description` 和 `Price` 值复制到新产品，并返回该产品。

图中的第二个代码说明了如何使用 `Product` 类的 `Clone` 和 `GetDisplayText` 方法。首先，声明并赋值一个命名为 `p1` 的 `Product` 变量。然后，声明另一个命名为 `p2` 的变量，并使用 `p1` 对象的 `Clone` 方法创建一个副本。注意由于 `Clone` 方法返回 `object` 类型，必须转换为 `Product` 才能赋值给变量 `p2`。接下来，修改第二个对象的 `Code` 和 `Description` 字段。最后，最后语句使用 `GetDisplayText` 方法在控制台上显示两个产品。你可以看到两个产品包含不同的数据，这证明了类是有效的。

在此示例中，产品对象的数据存储在三个字段中。如果你想克隆包含其他对象的复杂对象怎么办？例如，考虑一个私有字段中存储了 `Customer` 对象的 `Invoice` 类。在这种情况下，你可以使用浅拷贝或深拷贝来克隆 `Invoice` 对象。

如果你使用浅拷贝，克隆 `Invoice` 对象的 `Customer` 字段将指向与原始 `Invoice` 对象相同的 `Customer` 对象。相反，如果你使用深拷贝，克隆 `Invoice` 对象的 `Customer` 字段将指向 `Customer` 对象的副本。实现该目标简单的方法是在 `Customer` 类中实现 `ICloneable` 接口，然后 `Invoice` 对象调用该类的 `Clone` 方法。然而，你也可以在 `Invoice` 类的 `Clone` 方法内部克隆 `Customer` 对象。

根据 `ICloneable` 接口的定义，`Clone` 方法并没有指定返回的是深拷贝还是浅拷贝。你可以实现你认为最适合类的拷贝类型。只需在类文档中指定 `Clone` 方法返回的是深拷贝还是浅拷贝，这样类的用户在使用时就知道预期的结果。

![](img/3148667e42d4db35b3d08576aaa1fa01_487_0.png)

## 克隆 Product 类的代码

```sharp
public class Product : IDisplayable, ICloneable
{
    public string Code { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }

    public Product(string Code, string Description, decimal Price)
    {
        this.Code = Code;
        this.Description = Description;
        this.Price = Price;
    }

#region IDisplayable Members
public string GetDisplayText(string sep)
{
    return this.Code + sep + this.Description
    + sep + this.Price.ToString("c");
}
#endregion

#region ICloneable Members
public object Clone()
{
    Product p = new Product();
    p.Code = this.Code;
    p.Description = this.Description;
    p.Price = this.Price;
    return p;
}
#endregion
}
```

## 创建并克隆 Product 对象的代码

```csharp
Product p1 = new Product("JAV5", "Murach's Beginning Java 2, JDK 5, 52.50);
Product p2 = (Product)p1.Clone();
p2.Code = "JSE6";
p2.Description = "Murach's Java SE 6";
Console.WriteLine(p1.GetDisplayText("\n") + "\n");
Console.WriteLine(p2.GetDisplayText("\n") + "\n");
```

## 上述代码显示的输出

```
JAV5
Murach's Beginning Java 2, JDK 5
$52.50

JSE6
Murach's Java SE 6
$52.50
```

## 如何将接口作为参数

图 15-6 显示了如何将接口作为方法的参数。要做到这一点，你可以如第一个示例所示，将接口名称编码为参数类型。这里，名为 `CreateList` 的方法接受两个参数：一个实现了 `ICloneable` 的对象以及另一个。该方法返回一个列表，该列表充满了由第一个参数指定的对象的副本。列表中包含的副本数量由第二个参数指定。为了生成副本，`CreateList` 方法使用了传递给它的对象的 `Clone` 方法。

第二个示例显示了如何编写名为 `WriteToConsole` 的方法，它接受 `IDisplayable` 接口作为参数。该方法使用 `GetDisplayText` 方法返回对象的显示文本。然后，它使用 `Console` 的 `WriteLine` 方法将此文本到控制台。

当你声明一个接受接口作为参数的方法时，你可以将任何实现该接口的对象传递给该方法。如图中第三个代码示例所示。这里，创建了一个新的 `Product` 对象并将其存储在名为 `product` 的变量中。然后，使用 `CreateList` 方法创建三个 `Product` 对象的副本。最后，使用 `WriteToConsole` 方法将每个 `Product` 对象写入控制台。你可以在此图的对话框中看到结果。

关键点在于，`CreateList` 方法不知道它正在克隆的是什么类型的对象。它只知道该对象实现了 `ICloneable` 接口，这意味着它有一个 `Clone` 方法。同样，`WriteToConsole` 方法不知道它正在向控制台写入的是什么类型的对象。它只知道该对象实现了 `IDisplayable` 接口。这两个方法对 `Product` 对象都有效，因为 `Product` 类实现了 `Cloneable` 和 `IDisplayable`。

这个示例说明了一个更广泛的问题。简而言之，一个 `Product` 对象可以被认为是一个 `ICloneable` 或 `IDisplayable` 对象。因此，你可以在任何需要 `ICloneable` 或 `IDisplayable` 对象的地方提供一个 `Product` 对象。在图中，接口被用于指定方法参数的类型。然而，接口也可以用于指定其他地方的类型。例如，接口可以作为方法的返回类型。同样，接口可以用于指定属性的类型。在任何使用接口指定类型的地方，你都可以提供任何实现该接口的对象。

## 使用接口作为参数的 CreateList 方法

```csharp
public static List<object> CreateList(ICloneable obj, int count)
{
    List<object> objects = new List<object>();
    for (int i = 0; i < count; i++)
    {
        object o = obj.Clone();
        objects.Add(o);
    }
    return objects;
}
```

## 使用接口作为参数的 WriteToConsole 方法

```csharp
public static void WriteToConsole(IDisplayable d)
{
    Console.WriteLine(d.GetDisplayText("\n") + "\n");
}
```

## 使用这些方法的代码

```csharp
Product product = new Product("CS10", "Murach's C# 2010", 54.50m);
List<object> products = CreateList(product, 3);
foreach (Product p in products)
{
    WriteToConsole(p);
}
```

## 所示显示的输出

```
CS10
Murach's C# 2010
$54.50

CS10
Murach's C# 2010
$54.50

CS10
Murach's C# 2010
$54.50
```

### 描述

- 你可以将方法中使用的参数声明为接口类型。然后，你可以将任何实现该接口的对象传递给该参数。
- 由于 `Product` 类同时实现了 `ICloneable` 和 `IDisplayable` 接口，它可以作为参数传递给接受 `ICloneable` 或 `IDisplayable` 类型对象的方法。

## 如何使用泛型

在第8章中，你学习了如何使用泛型集合，例如由 `List<>`、`SortedList<>`、`Stack<>` 和 `Queue<>` 类定义的集合。大多数时候，当你需要处理对象集合时，可以使用这些或其他 .NET Framework 中的集合。但有时你需要使用泛型来定义自己的泛型集合，以添加 .NET Framework 泛型集合不支持的功能。如果是这样，接下来的主题将教你如何这样做。此外，它们还将介绍 .NET Framework 中泛型集合的内部机制。

## 如何编写定义泛型集合的类

图 15-7 显示了一个名为 `CustomList<>` 的类，它定义了一个泛型集合。要定义泛型类，要在类名后编写角括号，并在括号内指定类型参数。在类内部，你可以在任何可能使用类型的地方使用该类型参数。例如，接口可以作为方法的返回类型或参数类型。按照惯例，大多数程序员在类中使用字母 `T` 作为类型参数。

```csharp
public class CustomList<T>
{
    private List<T> list = new List<T>();

    // Add 方法
    public void Add(T item)
    {
        list.Add(item);
    }

    // 只读索引器
    public T this[int i]
    {
        get
        {
            return list[i];
        }
    }

    // 只读属性
    public int Count
    {
        get
        {
            return list.Count;
        }
    }

    // ToString 方法
    public override string ToString()
    {
        string listString = "";
        for (int i = 0; i < list.Count; i++)
        {
            listString += list[i].ToString() + "\n";
        }
        return listString;
    }
}
```

```csharp
CustomList<Product> products = new CustomList<Product>();
products.Add(new Product("JAV5", "Murach's Beginning Java 2, JDK 5, 52.50));
products.Add(new Product("JSE6", "Murach's Java SE 6", 52.50));
foreach (Product p in products)
{
    Console.WriteLine(p);
}
```

### 描述

- 你可以使用泛型来定义一个可以接受任何类型元素的类型安全集合。
- 要定义泛型集合的类，要在类名后编写角括号，并在括号内指定类型参数。在类内部，你可以在任何可能使用类型的地方使用该类型参数。例如，它可以作为方法的返回类型或参数类型。

图 15-7 的第二部分显示了一些使用第 1 部分定义的 `CustomList<>` 类的代码。首先，第一个测试创建了一个可以存储 `int` 类型的 `CustomList<>` 类，向列表添加了两个 `int` 值，并将这些值打印到控制台。然后，第二个测试创建了一个可以存储 `Product` 类型的 `CustomList<>` 类，向列表添加了两个 `Product` 对象，并将这些对象打印到控制台。

此示例显示 `CustomList<>` 类可以存储值类型（如 `int` 类型）或引用类型（如 `Product` 类型）。更重要的是，它展示了 `CustomList<>` 类的工作原理与 .NET Framework 定义的其他泛型类相似，尽管它提供的功能还没有其中任何一类多。注意，此示例的输出假设 `Product` 类包含一个 `ToString` 方法，该方法返回一个包含产品代码、描述和价格并用制表符分隔的字符串。

# 第 15 章 如何使用接口和泛型

## 使用 CustomList<> 的代码
