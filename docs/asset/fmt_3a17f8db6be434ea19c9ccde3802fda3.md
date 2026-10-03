
```csharp
// 用 switch 替换此代码
return DataLayer.GetVehicles(status);
```

5. 代码看起来可能像圣诞树一样，但不用担心。只需将直接集合替换为对指定集合类型泛型 `Get` 方法的调用；例如，`TestData.Vehicles` 将变为 `DataLayer.Get<IVehicle>`。

```csharp
case VehicleStatusAll:
   // return TestData.Vehicles;
   // 将变为
   return DataLayer.Get<IVehicle>();
```

6. 运行应用程序，并确保所有列表都包含信息。

7. 关闭应用程序。

`GenericProcessor` 类中 `GetVehicles` 方法的完整代码：

```csharp
public IEnumerable<IVehicle> GetVehicles(VehicleStatus status)
{
  try
  {
    switch (status)
    {
      case VehicleStatus.All:
        return DataLayer.Get<IVehicle>();
      case VehicleStatus.Booked:
        return from c in DataLayer.Get<IBooking>
        join b in DataLayer.Get<IBooking> on c.Id equals b.VehicleId
        where b.Returned.Equals(DateTime.MinValue)
        select c;
    }
  }
}
```

# C# 入门教程

```csharp
case VehicleStatus.Available:
    return from c in DataLayer.Get<IVehicle>()
    where GetVehicles(VehicleStatus.Booked)
    .count(b => b.Id.Equals(c.Id)).Equals(0)
    select c;
default:
    return null;
}
catch {
    throw;
}
```

## 重构 GetVehicleTypes 方法

该方法将不再需要存在于 `GenericDataLayer` 类中，因为它将调用 `GenericProcessor` 类中 `GetVehicleTypes` 方法的泛型 `Get` 方法。因此，该接口定义将从 `IGenericBase` 移动到 `GenericProcessor` 接口。

`GetVehicleTypes` 方法包含关于获取哪些车辆的逻辑，你需要通过将其移动到 `GenericProcessor` 版本的方法来保留这些逻辑。

1. 打开 `IGenericBase` 接口，剪切 `GetVehicles` 定义。

2. 打开 `IGenericProcessor` 接口，并将 `GetVehicles` 定义粘贴到接口中。

```csharp
IEnumerable<IVehicle> GetVehicles(VehicleStatus status);
```

3. 打开 `GenericDataLayer` 类中的 `GetVehicles` 方法，剪切 switch 块并删除该方法的剩余部分。

4. 打开 `GenericProcessor` 版本的 `GetVehicles` 方法，将对 `DataLayer.GetVehicles` 的调用替换为剪切出的 switch 块。

```csharp
// 用 switch 替换此代码
return DataLayer.GetVehicles(status);
```

5. 代码看起来可能像圣诞树一样，但不用担心。只需将直接集合替换为对指定集合类型泛型 `Get` 方法的调用；例如，`TestData.Vehicles` 将变为 `DataLayer.Get<IVehicle>`。

```csharp
case VehicleStatusAll:
   // return TestData.Vehicles;
   // 将变为
   return DataLayer.Get<IVehicle>();
```

6. 运行应用程序，并确保所有列表都包含信息。

7. 关闭应用程序。

`GenericProcessor` 类中 `GetVehicles` 方法的完整代码：

```csharp
public IEnumerable<IVehicle> GetVehicles(VehicleStatus status)
{
  try
  {
    switch (status)
    {
      case VehicleStatus.All:
        return DataLayer.Get<IVehicle>();
      case VehicleStatus.Booked:
        return from c in DataLayer.Get<IBooking>
        join b in DataLayer.Get<IBooking> on c.Id equals b.VehicleId
        where b.Returned.Equals(DateTime.MinValue)
        select c;
    }
  }
}
```

# C# 入门

## 完整的 IGenericDataLayer 接口

```csharp
public interface IGenericDataLayer : IGenericBase, ISerialize {
    #region Generic Methods
    void Add<T>(T item);
    #endregion

    #region Helper Methods
    int RentalDuration(DateTime rented, DateTime returned);
    double CalculatePrice(IVehicle vehicle, double returnedMeterSetting, int duration);
    #endregion
}
```

### 在 GenericDataLayer 类中实现 Add 方法

这个方法有点棘手，因为它涉及到大量的反射。你需要做的第一件事是获取泛型 `T` 的类型定义，以便访问其成员定义。然后，你需要创建一个 `TestData` 类的实例，以获取其类型定义，并使用它来访问其成员定义，从而使你能够访问集合中的数据。

使用 `TestData` 类的类型定义获取第一个具有泛型参数的字段，该参数的类型名称与泛型 `T` 的类型匹配。这将定位到角括号中类型与泛型 `T` 中存储的类型相同的集合。换句话说，如果 `T` 是 `ICustomer`，则将使用该类型在 `TestData` 类中定位匹配类型名的 `IEnumerable<ICustomer>` 集合，并将其作为 `FieldObject` 返回。

```csharp
var collectionVariable = dataType.GetFields().FirstOrDefault(f => f.FieldType.GetGenericArguments().First().Name.Equals(type.Name));
```

```csharp
var collectionVariable = dataType.GetFields() // 获取 TestData 类中的变量
    FirstOrDefault(f => f.FieldType) // 获取变量的数据类型 (IEnumerable)
    GetGenericArguments() // 获取角括号中的数据类型
    First() // 获取第一个泛型类型（你只需要一个）
    Name // 获取该泛型类型的名称
    Equals(type.Name)); // 它是否与 T 的类型名称相等
```

使用 `collectionVariable`，通过传递 `TestData` 类的实例调用 `GetValue` 方法来获取集合中的值，并将结果存储在变量 `collection` 中。

使用该集合获取最高 id，并将该值加 1 后赋值给传递给方法的 `T` 类型 `item` 对象的 `Id` 属性。

使用 `Add` 方法将更新后的项对象添加到集合中。

1. 打开 `GenericDataLayer` 类。

2. 添加一个包含泛型方法 `Generic Methods` 的区域。

3. 添加一个与 `IGenericDataLayer` 接口中定义相同的 `public Add` 方法。

4. 获取 `T` 的类型定义并将其存储在变量 `type` 中。`var type = typeof(T);`

5. 创建一个 `TestData` 类的实例并将其存储在变量 `testDataObj` 中。

6. 获取 `TestData` 类的类型并将其存储在变量 `testDataType` 中。`var testDataType = testDataObj.GetType();`

7. 获取 `FieldInfo` 对象（见上文详细描述）。将其存储在变量 `collectionVariable = testDataType.GetFields().FirstOrDefault(f => f.FieldType.GetGenericArguments().First().Equals(type.Name));` 中。

8. 获取集合并将其转换为 `IEnumerable<T>`。将集合存储在变量 `collection` 中。你需要将 `TestData` 实例传递给 `GetValue` 方法以访问数据。`var collection = (IEnumerable<T>)collectionVariable.GetValue(testDataObj);`

9. 为项对象的 `id` 属性赋值。`item.GetType().GetProperty("Id").SetValue(item, collection.Max(b => (int)b.GetType().GetProperty("Id").GetValue(b) + 1));`

10. 将更新后的项对象添加到集合中。

`GenericDataLayer` 类中 `Add` 方法的完整代码：

```csharp
public void Add<T>(T item)
{
    // 获取定义集合的类型
    var type = typeof(T);
    // 创建 TestData 类的实例，
    // 在将项添加到集合时需要该实例
    var testDataObj = new TestData();
    // TestData 类的类型定义
    // 用于查找集合
    var testDataType = testDataObj.GetType();
    // 根据其泛型类型查找集合，
    // 例如 <ICustomer> 和 T 的类型名称
    // (ICustomer, IVehicle, ...)
    var collectionVariable = testDataType.GetFields()
        .FirstOrDefault(f => f.FieldType.GetGenericArguments()[0].Name.Equals(type.Name));

    // 使用集合变量获取实际的 List<T> 集合
    var collection = (List<T>)collectionVariable.GetValue(testDataObj);

    // 最高 Id + 1
    item.GetType().GetProperty("Id").SetValue(item,
        collection.Max(b => (int)b.GetType().GetProperty("Id").GetValue(b) + 1));

    // 将 T 的实例添加到集合
    collection.Add(item);
}
```

### IGenericProcessor 接口

你将拥有一个 void `Add` 方法，它包含一个类型为 `T` 的参数 `item`，以及另一个类型为 `List<BusinessRule<>>` 的参数 `rules`。

1. 打开 `IGenericProcessor` 接口。

2. 添加一个描述为 `Generic Methods` 的区域。

3. 在区域中添加带有上述两个参数的 void `Add` 方法。

   `bool Add<T>(T item, List<BusinessRule<T>> rules);`

完整的 `IGenericProcessor` 接口：

```csharp
public interface IGenericProcessor : IGenericBase
{
    IGenericDataLayer { get; }

    #region Generic Methods
    bool Add<T>(T item, List<BusinessRule<T>> rules);
    #endregion

    bool CustomerExist(string socialSNumber);
    IBooking GetBooking(int vehicle);
    IEnumerable<IVehicle> GetVehicles(VehicleStatus status);
    IVehicle GetVehicle(int vehicleId);
}
```

### 在 GenericProcessor 类中实现 Add 方法

你有一个 void `Add` 方法，它接受一个类型为 `T` 的项和一个 `List<BusinessRule<>>` 的规则。它实现了一个 try/catch 结构，在 catch 块中抛出任何异常。

try 块的第一件事是通过 `RuleComparator` 实例调用 `EvaluateRules` 方法评估规则。如果方法成功，则在 DataLayer 上调用 Add 方法。然后从 `EvaluateRules` 方法返回结果。

1. 打开 `GenericProcessor` 类。

2. 在 `Generic Methods` 区域添加上述的 Add 方法。
