
public static object GetPropertyValue(object instance, string propertyName)
{
    try
    {
        var property = instance.GetType().GetProperty(propertyName);
        return property.GetValue(instance);
    }
    catch { throw; }
}

#endregion

# C# 初学者

## SetProperty 按钮的 Click 事件

1. 在代码后文件中添加 `btnSetProperty` 按钮的 `Click` 事件。
2. 在表单类中添加一个对象变量 `instance`。
3. 在 `Click` 事件中添加 `try/catch` 块，在 `catch` 块中显示异常消息。
4. 在 `btnSetProperty` 按钮的 `try` 块中调用 `LoadExecutable` 方法将程序集加载到内存中。
5. 调用 `GetType` 方法将类型（类）加载到内存中。
6. 使用该类型通过调用 `CreateDefaultConstructor` 创建实例。
7. 创建后，可以将其传递给 `SetPropertyValue` 方法，带有要赋值的属性名称以及从 `txt` 文本框获取的实际值。

```csharp
Members.SetPropertyValue(instance, "FirstName", txtValue.Text);
```

## Get Property 按钮的 Click 事件

你不需要创建类型实例，因为已经在 `btnSetProperty` 按钮的 `Click` 事件中完成并存储在名为 `instance` 的表单级变量中。

1. 在代码后文件中添加 `btnPropertyGroup` 按钮的 `Click` 事件。
2. 在 `Click` 事件中添加 `try/catch` 块，在 `catch` 块中通过消息框显示异常消息。
3. 将调用 `Members` 类 `GetPropertyValue` 方法的结果（传入 `instance` 变量和要获取值的属性名称）赋值给 `lblResult`。
4. 运行应用程序并在文本框中输入一个值。
5. 点击 Set Property 按钮将该值保存到 `Student` 类实例的 `FirstName` 属性中。
6. 点击 Get Property 按钮以获取存储在 `FirstName` 属性中的值。该值应显示在标签上。

```csharp
lblResult.Text = Members.GetPropertyValue(instance, "FirstName").ToString();
```

## 16. 泛型

### 为什么使用泛型？

在本节中，你将学习为什么可能需要使用泛型，以及为什么它是 C# 工具箱中强大的工具。

泛型是一种以类型安全的方式重用代码的强大方法。想象一下执行以下代码会发生什么：

```csharp
public void UseArrayList()
{
    ArrayList books = new ArrayList();
    books.Add(new Book("Lord of the Rings"));
    books.Add(new Book("The Color of Magic"));
    // 我们可以添加一个不是 Books 类的对象
    books.Add(new Car());
    // 运行时将抛出异常，因为
    // 你不能将 Car 转换为 Book
    Book book = (Book)books[2];
}
```

该程序将抛出异常，因为无法将用 `Car` 类创建的对象强制转换为 `Book` 类的对象。你可以通过在代码中添加额外的检查（如 `if` 块）来规避这个问题，但这将非常繁琐且难以管理。从本质上，你必须为每个现有和未来的类型添加检查以确保“安全”。

```csharp
Book book = (Book)books[2];
```

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_582_0.png)

### 集合

如果有一种方法可以声明集合中应该存储什么类型的对象，而无需向代码中添加大量额外逻辑（例如对象转换以及避免存储值类型时的装箱和拆箱），那不是很好吗？

正如你可能已经猜到的那样，确实有。那位拯救白白的勇敢骑士的名字就是“泛型”。泛型是一种推迟声明类型的方法，直到列表实例被创建。

注意，当你在 `List` 类之后编写左尖括号 `<` 时，会出现一个灰色的弹出消息，告诉你这是一个泛型列表，它接受类型 `T`，其中 `T` 被替换为你想与列表使用的实际类型。一旦你声明了泛型列表，它就变成了闭合泛型列表，只能与提供的类型一起。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_583_0.png)

注意，闭合泛型列表被用作方法的返回类型，用于返回方法内部创建的书籍列表。

```csharp
public List<Book> UseGenericCollection()
{
    var books = new List<Book>
    {
        new Book { ISBN = "1234567890", Title = "Lord of the Rings"},
        new Book { ISBN = "0987654321", Title = "The Color of Magic" }
    };
    // 现在已无法向列表添加 Books 以外的对象了
    // books.Add(new Car { ChassisId = "1223ABDS23", Make = "Volvo" });
    return books;
}
```

```csharp
books.Add(new Car { ChassisId = "1223ABDS23", Make = "Volvo" });
```

(本地变量) `List<Book> books`
Error: 找不到最佳重载方法 'System.Collections.Generic.List<Generic.Collections.Classes.Chapter_1.Book>.Add(Generic.Collections.Classes...'。

如果你尝试向 `Book` 列表添加一个 `Car`，将显示编译前的错误。

### 使用泛型创建专用集合

假设你意识到你的应用程序框架可以使用一种特殊的集合，该集合可以轻松地反转集合的内容。为了实现这一点，我们创建一个接受泛型类型并实现 `IEnumerable` 接口的类，使得对存储的项进行迭代成为可能。

我知道这个例子有些生硬，但它的目的是向你展示如何结合类、方法、方法参数、字段以及作为返回类型使用泛型。你还将学习如何使用 `yield` 关键字在循环时创建列表结果。

开始之前，你需要添加一个名为 `ReversibleCollection` 的类，该类实现了泛型版本的 `IEnumerable<T>` 接口。

重要：`yield` 关键字会构建一个状态机，它将实现 `IEnumerable<T>` 并在迭代结束返回修改或排序后的项。

```csharp
class ReversibleCollection<T> : IEnumerable<T>
{
    #region IEnumerable<T> 的实现
    public IEnumerator<T> GetEnumerator()
    {
        foreach (var item in collection)
        {
            yield return item;
        }
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        // 调用另一个 GetEnumerator 方法
        // 并返回其结果
        return GetEnumerator();
    }
    #endregion
}
```

接下来，你需要在私有集合中保存类型为 `T` 的项，该集合类外部无法访问。列表将存储通过接下来添加的 `Add` 和 `AddRange` 方法添加的项。

由于你使用泛型类型 `T` 实现了该类，这意味着 `T` 现在可以在整个类中使用。当你添加一个名为 `collection` 的 `List<T>` 时，你会利用这一点，它将存储添加到集合中的项。在创建 `Add(T item)` 和 `AddRange(T[] item)` 方法时，你也将使用泛型类型 `T`。

```csharp
public void Add(T item)
{
    collection.Add(item);
}

public void AddRange(T[] items)
{
    collection.AddRange(items);
}
```

`private List<T> collection = new List<T>();`

注意，闭合泛型列表被用作方法的返回类型，用于返回方法中创建的列表。（示例下）

```csharp
public IEnumerable<T> Reverse()
{
    foreach (var item in collection)
    {
        yield return item;
    }
}
```

### 练习：泛型集合

1. 创建一个新的 Windows Forms 解决方案。
2. 添加一个名为 `Classes` 的文件夹。
3. 在 `Classes` 中添加一个名为 `Car` 的类。`Car` 类应有两个属性：字符串类型的 `RegNo` 和 `Model`。
4. 在 `Classes` 中添加一个名为 `Motorcycle` 的类。该类应有两个字符串类型的 `RegNo` 和 `Model`。
5. 在表单上添加一个名为 `cboCars` 的组合框。
6. 在表单上添加一个名为 `btnCollections` 的按钮并打开其点击事件。

让我们先观察使用普通集合存储多种类型的值会发生什么。

7. 在表单类创建一个名为 `vehicles` 的 `ArrayList` 集合（不在按钮点击事件中）。
8. 在表单构造函数或表单的 `Load` 事件中向 `vehicles` 集合添加两辆汽车和一辆摩托车。

```csharp
vehicles.Add(new Car { RegNo = "ABC123", Model = "Volvo" });
vehicles.Add(new Car { RegNo = "XYZ123", Model = "Saab" });
vehicles.Add(new Motorcycle { RegNo = "QWE987", Model = "Honda" });
```

9. 在按钮点击事件中，编写一个 `for` 循环遍历集合中的 `vehicles`。
10. 因为你只想在 `cboCars` 组合框显示汽车，所以在将对象添加到组合框之前，使用 `Car` 类对其进行转换。

```csharp
foreach (var vehicle in vehicles)
    cboCars.Items.Add((Car)vehicle);
```

11. 当应用程序运行并按下按钮时，将显示 `InvalidCastException`，因为 `Motorcycle` 对象无法转换为 `Car` 对象。

```csharp
foreach (var vehicle in vehicles)
    cboCars.Items.Add(((Car)vehicle).RegNo);
```

12. 现在，使用泛型集合重写代码并限制它存储一种类型。这将使集合在存储单一类型的值时是安全的。

#### 到目前表单类的代码

```csharp
public partial class Form1 : Form
{
    ArrayList vehicles = new ArrayList();

    public Form1()
    {
        InitializeComponent();

        #region RegNo
        vehicles.Add(new Car { RegNo = "ABC123", Model = "Volvo" });
        vehicles.Add(new Car { RegNo = "XYZ123", Model = "Saab" });
        vehicles.Add(new Motorcycle { RegNo = "QWE987", Model = "Honda" });
        #endregion
    }

    private void btnnCollections_Click(object sender, EventArgs e)
    {
        foreach (var vehicle in vehicles)
        {
            cboCars.Items.Add(((Car)vehicle).RegNo);
        }
    }
}
```

### 接口解决方案

你可以通过使用一个名为 `IVehicle` 的中间接口来解决，让 `Car` 和 `Motorcycle` 类实现该接口，并使用该接口来避免异常。这将带来另一个挑战，我们将在练习中探索它。

1. 向项目添加一个名为 `Interfaces` 的文件夹。
2. 在 `Interfaces` 文件夹中添加一个名为 `IVehicle` 的接口。
3. 在 `IVehicle` 接口中添加 `RegNo` 和 `Model` 属性。
4. 在 `Car` 和 `Motorcycle` 类中实现 `IVehicle` 接口。
   `class Car : IVehicle`
   `class Motorcycle : IVehicle`
5. 为表单添加另一个名为 `btnCollectionInterface` 的按钮。
6. 进入按钮的 `Click` 事件并添加一个遍历 `vehicles` 集合的 `foreach` 循环。
7. 这次在将对象添加到组合框时，你将它们强制转换为 `IVehicle` 而不是 `Car`。

#### 到目前表单类的代码

```csharp
public partial class Form1 : Form
{
    ArrayList vehicles = new ArrayList();

    public Form1() ...

    private void btnCollections_Click(object sender, EventArgs e) ...

    private void btnCollectionswithInterface_Click(object sender, EventArgs e)
    {
        foreach (var vehicle in vehicles)
            cboCars.Items.Add(((IVehicle)vehicle).RegNo);
    }
}
```

8. 运行应用程序。这次没有抛出异常。但是，如果你查看组合框列表，你会发现现在摩托车对象也和汽车对象一起显示在组合框的下拉列表中。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_589_0.png)

显然，当目标是仅在组合框中显示汽车时，这并不是你想要的结果。

### 泛型解决方案

仅显示汽车的更好方法是在处理汽车时使用专门用于汽车对象的集合，在处理摩托车时使用专门用于摩托车的集合。为了实现这一点，你将使用泛型。

1. 在表单类中添加一个名为 `cars` 的 `List<T>` 集合用于存储汽车（而不是按钮的 `Click` 事件）。
   `List<Car> cars;`
2. 向 `List<Car>` 中添加两辆汽车
   ```csharp
   cars = new List<Car>
   {
       new Car { RegNo = "ABC123", Model = "Volvo" },
       new Car { RegNo = "XYZ123", Model = "Saab" }
   };
   ```
3. 尝试向 `cars` 集合添加一个摩托车实例，这应该会导致编译前的错误，并用红色波浪线下划代码。如你所示，一旦泛型列表用类型实例化并成为闭合泛型集合，就不可能存储汽车以外的任何内容。
4. 注释掉或删除添加摩托车的代码行。
5. 创建新按钮 `btnGenericCollection` 并添加其 `Click` 事件。
6. 在按钮事件中使用组合框的 `DataSource` 属性并通过 `DisplayMember` 属性显示注册号。
7. 运行应用程序并点击按钮。如你所见，列表只显示汽车。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_590_0.png)

#### 表单类的代码

```csharp
public partial class Form1 : Form
{
    ArrayList vehicles = new ArrayList();
    List<Car> cars;

    public Form1()
    {
        InitializeComponent();

        #region ArrayList collection
        #region Generic collection
        cars = new List<Car>
        {
            new Car { RegNo = "ABC123", Model = "Volvo" },
```
