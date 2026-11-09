
## 第 12 章 泛型

**本章内容：**

- 框架类库中的泛型 .......... 270
- 泛型基础设施 .......... 271
- 泛型接口 .......... 277
- 泛型委托 .......... 278
- 委托和接口的逆变与协变泛型类型实参 .......... 279
- 泛型方法 .......... 281
- 泛型和其他成员 .......... 284
- 可验证性与约束 .......... 284

熟悉面向对象编程的开发者都知道它带来的好处。使开发者极具生产力的一个重大好处是代码重用，即能够派生一个继承基类所有能力的类。派生类只需重写虚方法或添加一些新方法，即可自定义基类的行为以满足开发者的需求。泛型是公共语言运行时（CLR）和编程语言提供的另一种机制，它提供了又一种代码重用形式：算法重用。

基本上，一名开发者定义一个算法，例如排序、搜索、交换、比较或转换。但是，定义该算法的开发者并未指定算法操作的数据类型；该算法可以泛型方式应用于不同类型的对象。另一名开发者随后可以使用这个现有算法，只要他或她指明该算法应操作的具体数据类型，例如操作 Int32、String 等的排序算法，或操作 DateTime、Version 等的比较算法。

大多数算法封装在类型中，CLR 允许创建泛型引用类型以及泛型值类型，但不允许创建泛型枚举类型。此外，CLR 允许创建泛型接口和泛型委托。有时，单个方法可以封装有用的算法，因此 CLR 允许创建定义在引用类型、值类型或接口中的泛型方法。

让我们看一个简单示例。框架类库（FCL）定义了一个泛型列表算法，它知道如何管理一组对象；这些对象的数据类型不由泛型算法指定。想要使用该泛型列表算法的人可以稍后指定要与其一起使用的确切数据类型。

封装泛型列表算法的 FCL 类称为 `List<T>`（读作 List of Tee），该类定义在 System.Collections.Generic 命名空间中。此类的定义如下所示（代码已大幅简化）。

```csharp
[Serializable]
public class List<T> : IList<T>, ICollection<T>, IEnumerable<T>,
    IList, ICollection, IEnumerable {

    public List();
    public void Add(T item);
    public Int32 BinarySearch(T item);
    public void Clear();
    public Boolean Contains(T item);
    public Int32 IndexOf(T item);
    public Boolean Remove(T item);
    public void Sort();
    public void Sort(IComparer<T> comparer);
    public void Sort(Comparison<T> comparison);
    public T[] ToArray();

    public Int32 Count { get; }
    public T this[Int32 index] { get; set; }
}
```

定义泛型 List 类的程序员通过将 `<T>` 紧跟在类名之后，表明它使用未指定的数据类型。定义泛型类型或方法时，它为类型指定的任何变量（如 T）称为类型参数。T 是一个变量名，可在源代码中任何可使用数据类型的地方使用。例如，在 List 类定义中，你会看到 T 用于方法参数（Add 方法接受类型为 T 的参数）和返回类型（ToArray 方法返回类型为 T 的一维数组）。另一个示例是索引器方法（在 C# 中称为 this）。索引器有一个 get 访问器方法，返回类型为 T 的值；还有一个 set 访问器方法，接受类型为 T 的参数。因为 T 变量可在任何可指定数据类型的地方使用，所以在方法内定义局部变量或在类型内定义字段时也可以使用 T。

> **注意** Microsoft 的设计准则规定，泛型参数变量应命名为 T，或至少以大写 T 开头（如 TKey 和 TValue）。大写 T 代表类型，正如大写 I 代表接口（如 IComparable）。

既然泛型 `List<T>` 类型已定义，其他开发者就可以通过指定希望该算法操作的确切数据类型来使用此泛型算法。使用泛型类型或方法时，指定的数据类型称为类型实参。例如，开发者可能想通过指定 DateTime 类型实参来使用 List 算法。

以下代码展示了这一点。

```csharp
private static void SomeMethod() {
    // Construct a List that operates on DateTime objects
    List<DateTime> dtList = new List<DateTime>();

    // Add a DateTime object to the list
    dtList.Add(DateTime.Now);       // No boxing

    // Add another DateTime object to the list
    dtList.Add(DateTime.MinValue);  // No boxing

    // Attempt to add a String object to the list
    dtList.Add("1/1/2004");         // Compile-time error

    // Extract a DateTime object out of the list
    DateTime dt = dtList[0];        // No cast required
}
```

正如刚才的代码所示，泛型为开发者提供了以下重大好处：

- **源代码保护** 使用泛型算法的开发者无需访问该算法的源代码。然而，对于 C++ 模板，使用该算法的开发者必须能够获得该算法的源代码。
- **类型安全** 当泛型算法与特定类型一起使用时，编译器和 CLR 理解这一点，并确保只有与指定数据类型兼容的对象才能与该算法一起使用。尝试使用不兼容类型的对象将导致编译器错误或引发运行时异常。在示例中，尝试将 String 对象传递给 Add 方法会导致编译器发出错误。
- **更简洁的代码** 因为编译器强制类型安全，源代码中需要的强制转换更少，这意味着代码更易编写和维护。在 SomeMethod 的最后一行，开发者不需要使用 (DateTime) 强制转换来将索引器的结果（查询索引 0 处的元素）放入 dt 变量。
- **更好的性能** 在泛型之前，定义通用算法的方式是将其所有成员定义为使用 Object 数据类型。如果要将该算法用于值类型实例，CLR 必须在调用算法成员之前对值类型实例进行装箱。如第 5 章“基元类型、引用类型和值类型”所述，装箱会导致托管堆上的内存分配，这会导致更频繁的垃圾回收，进而损害应用程序的性能。因为现在可以创建用于特定值类型的泛型算法，值类型的实例可以按值传递，CLR 不再需要进行任何装箱。此外，由于不需要强制转换（见上一项），CLR 不必检查所尝试的强制转换的类型安全，这也使代码更快。
