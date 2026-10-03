
## 20. 在 RuleComparator 类的实例上调用 `EvaluateRules<T>` 方法

在 `RuleComparator` 类的实例上调用 `EvaluateRules<T>` 方法，并将其返回值赋值给名为 `success` 的变量。将 `AddCustomer` 方法中正在创建的客户实例连同规则集合传递给 `EvaluateRules` 方法。

```csharp
var success = new RuleComparator().EvaluateRules(customer, rules);
```

## 21. 设置断点

在调用 `processor.AddCustomer` 方法处设置一个断点。

## 22. 运行应用程序

运行应用程序并在 **Add Data** 选项卡上添加新客户。

## 23. 验证结果

`success` 变量的值应为 `true`。

## 24. 停止应用程序

停止应用程序。

## 25. 修改规则属性

将 `id` 规则的 `Value` 属性改为 `0`。

# C# 入门

# 创建接口和类

复制 `IBookingProcessor` 接口和 `BookingProcessor` 类，并将它们重命名为 `IGenericProcessor` 和 `GenericProcessor`。对 `IDataLayer`、`IRentalBase` 和 `CollectionDataLayer` 执行相同的操作，并将它们重命名为 `IGenericDataLayer`、`IGenericBase` 和 `GenericDataLayer`。

不要忘记更改已实现和继承的接口以及相关类的构造函数。除了上述更改外，目前没有删除、更改或添加代码。

你可以通过以下方式复制 `.cs` 文件：

1. 在解决方案管理器中右键点击文件并复制。
2. 在你想粘贴的文件夹上右键点击并选择“粘贴”。
3. 选择你粘贴的文件并按键盘上的 F2 重命名文件，但这不会更改文件内部的内容。
4. 打开文件更改类或接口的名称，如果是类，则更改构造函数。

## 数据层（Data Layer）项目中复制并重命名后的接口和类的更改

```csharp
public interface IGenericBase
{
  // 此处不显示其他可用方法
}
```

```csharp
public interface IGenericDataLayer : IGenericBase, ISerializable
{
  // 此处不显示其他可用方法
}
```

```csharp
public class GenericDataLayer : IGenericDataLayer
{
  public GenericDataLayer()
  {
    // 代码未显示
  }
  // 此处不显示其他可用方法
}
```

## 业务层（Business Layer）项目中复制并重命名后的接口和类的更改

```csharp
public interface IGenericProcessor : IGenericBase {
    IGenericDataLayer DataLayer { get; }
    // 此处不显示其他可用方法
}

public class GenericProcessor : IGenericProcessor {
    #region Properties
    public IGenericDataLayer DataLayer { get; private set; }
    #endregion

    #region Constructor
    public GenericProcessor(IGenericDataLayer dataLayer) {
        DataLayer = dataLayer;
    }
    #endregion

    // 其他可用方法已省略
}
```

# 通用 Get 方法

要实现泛型 `Get` 方法，首先必须在 `IGenericBase` 接口中实现它，这样它在 `GenericProcessor` 和 `GenericDataLayer` 类中都必须实现。但该方法应该返回什么？如果有参数，应该是什么？

如果你查看接口中旧的 `Get` 方法，你会发现它们返回所获取数据类型的 `IEnumerable`；这意味着这是一个使用泛型的绝佳机会，因为类型决定了将返回的内容；这些类型可以很容易地替换为泛型类型 `T`。棘手之处在于，泛型类型不会让你直接访问类型成员，这意味着你将在泛型 `Get` 方法中必须使用反射（reflection）来访问它们。

为了降低复杂性，你会将无参数的 `Get` 方法视为一种情况，并将其他 `Get` 方法视为单独的情况，你仍然可以作为次要手段对这些方法使用泛型 `Get` 其他方法。因此，`GetCustomers`、`GetBooking` 和 `GetVehicleTypes` 方法都将被新的无参数泛型 `Get` 方法取代。

因此，新的泛型接口方法定义为 `IEnumerable<T> Get<T>()`。将该方法定义添加到 `IGenericBase` 接口中，但暂不要移除旧的 `Get` 方法定义。

在 `GenericProcessor` 类和 `GenericDataLayer` 类中实现 `Get` 方法。

在 `GenericProcessor` 类的 `Get` 方法中调用 `GenericDataLayer` 类的 `Get` 方法。

## 为 IGenericBase 接口添加 Get 方法

1. 打开 `IGenericBase` 接口。
2. 添加一个描述为 `Generic Methods`（通用方法）的区域（region）。
3. 在区域内添加方法定义。

`IGenericBase` 接口的更改：

```csharp
public interface IGenericBase
{
    #region Generic Methods
    IEnumerable<T> Get<T>();
    #endregion
    #region Action Methods ...
    #region Fetch Methods ...
}
```

## 在 GenericProcessor 类中实现 Get 方法

1. 打开 `GenericProcessor` 类。
2. 添加一个描述为 `Generic Methods` 的区域。
3. 添加一个与 `IGenericBase` 接口定义相同的公共 `Get` 方法。
4. 通过 `DataLayer` 属性调用 `GenericDataLayer` 类中的 `Get` 方法并返回结果。

```csharp
public IEnumerable<T> Get<T>() {
    return DataLayer.Get<T>();
}
```

## 在 GenericDataLayer 类中实现 Get 方法

此方法有点复杂，因为它涉及大量的反射。你需要的第一步是获取泛型类型 `T` 的类型定义，以便访问其成员定义。然后创建一个 `TestData` 类的实例并获取其类型定义，以便访问其成员定义和集合。

使用 `TestData` 类的类型定义来获取第一个具有与泛型类型 `T` 名称匹配的泛型参数的字段。这将找到括号中类型与存储在泛型 `T` 中的类型相同的集合。换句话说，如果 `T` 是 `ICustom`，则将使用该类型在 `TestData` 类中匹配类型名称的 `IEnumerable<ICustom>` 集合，并将其作为 `FieldInfo` 对象返回。

```csharp
var colFieldInfo = dataType.GetFields().FirstOrDefault(f => f.FieldType.GetGenericArguments().First().Name.Equals(type.Name));
```

```csharp
var colFieldInfo =
dataType.GetFields() // 获取 TestData 类中的变量
.FirstOrDefault(f =>) // 找到第一个匹配的字段
f.FieldType // 获取变量的数据类型 (IEnumerable)
.GetGenericArguments() // 获取括号中的数据类型
.First() // 获取第一个泛型类型（你只使用一个）
.Name // 获取泛型类型的名称
Equals(type.Name)); // 是否等于 T 的类型名称
```

使用 `FieldInfo` 对象，通过调用 `GetValue` 方法并传入 `TestData` 实例来获取其值。

1. 打开 `GenericDataLayer` 类。
2. 添加一个描述为 `Generic Methods` 的区域。
3. 添加一个与 `IGenericBase` 接口定义相同的公共 `Get` 方法。
4. 获取类型 `T` 的类型定义并将其存储在名为 `type` 的变量中。

   `var type = typeof(T);`

5. 创建 `TestData` 类的实例并将其存储在名为 `testDataObj` 的变量中。
6. 获取 `TestData` 类的类型定义并将其存储在名为 `testDataType` 的变量中。

   `var testDataType = testDataObj.GetType();`

7. 获取描述你正在寻找的集合的 `FieldInfo` 对象，并将其存储在名为 `collectionField` 的变量中（见上文描述）。

   `var collectionField = testDataType.GetFields().FirstOrDefault(f => f.FieldType.GetGenericArguments().First().Name.Equals(type.Name));`

8. 获取集合并强制转换为 `IEnumerable<T>`。将集合存储在名为 `collection` 的变量中。你需要将 `TestData` 实例传递给 `GetValue` 方法以访问数据。

   `var collection = (IEnumerable<T>)collectionField.GetValue(testDataObj);`

9. 从方法返回集合。

`GenericDataLayer` 类中 `Get` 方法的完整代码：

```csharp
#region Generic Methods
public IEnumerable<T> Get<T>()
{
  var type = typeof(T);
  var testDataObj = new TestData();
  var testDataType = testDataObj.GetType();

  var collectionField = testDataType.GetFields()
      .FirstOrDefault(f => f.FieldType.GetGenericArguments()
      .First().Name.Equals(type.Name));

  var collection = (IEnumerable<T>)collectionField
      .GetValue(testDataObj);

  return collection;
}
#endregion
```

## 在表单中替换 Get 方法调用

这基本上是一个搜索替换的场景，你把所有对 `GetCustomers`、`GetBookings` 和 `GetVehicleTypes` 方法的调用替换为泛型方法的调用，并指定要获取集合数据的类型；例如，`GetCustomers()` 访问将被替换为调用 `Get<Customer>()`。

将 `TestData` 中集合的访问修饰符更改为 `public` 将使你更容易通过反射处理类中的数据。

# C# 入门教程

1. 打开 **TestData** 类，并将所有集合的访问修饰符从 **internal** 改为 **public**。
2. 打开表单的代码后台文件（code-behind）。
3. 在表单开头找到 `IBookingProcessor` 处理器变量，将其更改为 `IGenericProcessor` 处理器。
4. 在 `Form_Load` 事件中更改 `BookingProcessor` 的实例，创建一个 `GenericProcessor` 类的实例。

```csharp
processor = new GenericProcessor(new GenericDataLayer());
```

5. 找到 `FillCustomers` 方法。
6. 将 LINQ 查询中对 `GetCustomers` 方法的调用替换为对泛型 Get 方法的调用。

```csharp
var customer = processor.Get<ICustomer>()
```

7. 找到 `FillBookings` 方法。
8. 将 LINQ 查询中对 `GetBookings` 和 `GetCustomers` 方法的调用替换为对泛型 Get 方法的调用。

```csharp
var bookings = from b in processor.Get<IBooking>
join c in processor.Get<ICustomer>() on b.CustomerId equals c.Id
```

9. 在 LINQ 查询中找到 `FillVehicleTypes` 方法，并替换为泛型 Get 方法的调用。

```csharp
cboTypes.DataSource = processor.Get<IVehicleType>();
```

10. 将 LINQ 查询中对 `GetVehicleTypes` 方法的调用替换为泛型 Get 方法的调用。

```csharp
return (from b in DataLayer.Get<IBooking>)
```

11. 找到 `GetBooking` 方法。
12. 将 LINQ 查询中对 `GetBookings` 方法的调用替换为泛型 Get 方法的调用。
13. 找到 `AddCustomer` 方法。
14. 将 `SocialSecurityNumber` 规则中对 `GetCustomers` 方法的调用替换为泛型 Get 方法的调用。

```csharp
new BusinessRule<ICustomer> { Property = "SocialSecurityNumber",
Items = processor.Get<ICustomer>(),
Comparer = RuleOperator.NotContains
```

15. 找到 `CustomerExist` 方法。
16. 将 LINQ 查询中对 `GetCustomers` 方法的调用替换为泛型 Get 方法的调用。

```csharp
var social = (from c in DataLayer.Get<ICustomer>())
```

17. 找到 `btnSave_Click` 事件。
18. 将 `WriteToFile` 方法调用中对 `GetCustomers` 方法的调用替换为泛型 Get 方法的调用。

```csharp
var success = IO.WriteToFile("C:\\Test\\Customers.txt", 
processor.Get<ICustomer>());
```

19. 运行应用程序，并确保所有列表视图和组合框都有数据。
20. 关闭应用程序。
21. 现在既然你已经知道程序可以正常运行，是时候进行清理并移除不再使用的代码了。
22. 打开 `GenericBase` 接口，移除（或注释掉）`GetCustomers`、`GetBookings` 和 `GetTypes` 方法。

```csharp
//IEnumerable<ICustomer> GetCustomers();
//IEnumerable<IBooking> GetBookings();
//IEnumerable<IVehicle> GetVehicleTypes();
```

23. 打开 `GenericProcessor` 类，移除（或注释掉）`GetCustomers`、`GetBookings` 和 `GetTypes` 方法。
24. 打开 `GenericDataLayer` 类，移除（或注释掉）`GetCustomers`、`GetBookings` 和 `GetTypes` 方法。
25. 运行应用程序，并确保所有列表视图和组合框都有数据。
26. 关闭应用程序。

# 重构 GetVehicles 方法

该方法将不再需要存在于 `GenericDataLayer` 类中，因为它将调用 `GenericProcessor` 类中 `GetVehicles` 方法的泛型 Get 方法。因此，该方法的接口定义将从 `GenericBase` 移动到 `GenericProcessor` 接口。

`GetVehicles` 方法包含关于获取哪些车辆的逻辑，你需要通过将其移动到 `GenericProcessor` 版本的方法来保留这些逻辑。

## C# 入门教程

1. 打开 `IGenericBase` 接口，剪切 `GetVehicles` 定义。
2. 打开 `IGenericProcessor` 接口，并将 `GetVehicles` 定义粘贴到接口中。

```csharp
IEnumerable<IVehicle> GetVehicles(VehicleStatus status);
```

3. 打开 `GenericDataLayer` 类中的 `GetVehicles` 方法，剪切 switch 块并删除该方法的剩余部分。
4. 打开 `GenericProcessor` 版本的 `GetVehicles` 方法，将对 `DataLayer.GetVehicles` 的调用替换为剪切出的 switch 块。
