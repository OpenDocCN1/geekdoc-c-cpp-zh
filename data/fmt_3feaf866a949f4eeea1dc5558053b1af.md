
```csharp
case VehicleStatus.Available:
    return c in TestData.Vehicles
    where GetVehicles(VehicleStatus.Booked)
    .Count(b => b.Id.Equals(c.Id)).Equals(0)
    select c;
```

7. 在 Fetch Methods 区域实现 `GetOutputType` 方法。

8. 为方法添加一个 LINQ 查询，使用 `FirstOrDefault` 方法根据 `vehicleTypeId` 获取车辆类型。

```csharp
return TestData.VehicleTypes.FirstOrDefault(vt => vt.Id.Equals(vehicleTypeId));
```

目前 `CollectionDataLayer` 的代码：

```csharp
public class CollectionDataLayer : IDataLayer
{
    public CollectionDataLayer() ...

    #region Fetch Methods
    public IEnumerable<ICustomer> GetCustomers() ...
    public IEnumerable<IVehicle> GetVehicles(VehicleStatus status)
    {
        switch (status)
        {
            case VehicleStatus.All:
                return TestData.Vehicles;

            case VehicleStatus.Booked:
                return c in TestData.Vehicles
                join b in TestData.Bookings on c.Id equals b.VehicleId
                where b.Returned.Equals(DateTime.MinValue)
                select c;

            case VehicleStatus.Available:
                return c in TestData.Vehicles
                where GetVehicles(VehicleStatus.Booked)
                .Count(b => b.Id.Equals(c.Id)).Equals(0)
                select c;
        }
        return new List<IVehicle>();
    }

    public IVehicle GetVehicleType(int vehicleID)
    {
    }
    #endregion

    #region Helper Methods
    #endregion
}
```

# BookingProcessor 类

由于这两个方法都不需要实现业务逻辑，它们的逻辑再简单不过了，直接通过你早些添加到 `BookingProcessor` 类的 `DataLayer` 属性调用 `CollectionLayer` 类中的 `GetVehicles` 和 `GetOutputType` 方法的结果即可。你还应该实现异常处理，重新抛出来自数据层的任何异常。

1. 打开 Business 层区域中的 `BookingProcessor` 类。

2. 在 Fetch Methods 区域实现 `GetVehicles` 方法。

3. 在方法中添加 `try/catch` 块，在 `catch` 块中重新抛出异常。

4. 返回调用数据层 `GetVehicles` 方法的结果。

```csharp
return DataLayer.GetVehicles(status);
```

# C# 入门

5. 在 Fetch Methods（获取方法）区域实现 `GetVehicleType` 方法。

6. 在方法中添加 `try/catch` 块，其中 catch 块重新抛出异常。

7. 在数据层中调用 `GetVehicleType` 方法并返回结果。

```csharp
return DataLayer.GetVehicleType(vehicleTypeId);
```

目前 `BookingProcessor` 类如下：

```csharp
public class BookingProcessor : IBookingProcessor
{
    #region Properties
    public IDataLayer DataLayer { get; private set; }
    #endregion

    #region Constructor
    public BookingProcessor(IDataLayer dataLayer) ...
    #endregion

    #region Action Methods
    #region Fetch Methods
    public IEnumerable<ICustomer> GetCustomers() ...
    public IEnumerable<IVehicle> GetVehicles(VehicleStatus status)
    {
        try
        {
            return DataLayer.GetVehicles(status);
        }
        catch
        {
            throw;
        }
    }

    public IVehicle GetVehicleType(int vehicleTypeId)
    {
        try
        {
            return DataLayer.GetVehicleType(vehicleTypeId);
        }
        catch { throw; }
    }
    #endregion
    #region Helper Methods
    #endregion
}
```

# GetVehicles ListItem 转换方法

```csharp
return v in processor.GetVehicles(vehicleStatus)
  select new ListItem(new string[])
  {
    processor.GetVehicleType(v.TypeId).Name,
  }};
```

# C# 入门

`GetVehicles` 方法的完整代码：

```csharp
private IEnumerable<ListItem> GetVehicles(VehicleStatus vehicleStatus)
{
    return v in processor.GetVehicles(vehicleStatus)
    select new ListItem(new string[]
    {
        v.RegistrationNumber,
        processor.GetStateType(v.TypeId).Name,
        v.BasePricePerKm.ToString(),
        v.BasePricePerDay.ToString(),
        v.Meter.ToString(),
        v.Id.ToString(),
        "" //BookingId
    });
}
```

# 填充列表视图

创建一个名为 `FillAvailableVehicles` 的方法，该方法通过调用你在表单中刚刚创建的 `GetVehicles` 方法来获取所有可用车辆，并传递可用车辆状态。

使用方法调用的结果填充 `lvwAvailableVehicles` 列表视图，在添加获取的车辆之前，**别忘了**清空列表视图中的项，以避免列表视图出现重复项。

可用车辆

| 注册号 | 类型 | 公里费率 | 日费率 | 里程 |
|---|---|---|---|---|
| FGH123 | 轿车 | 0 | 100 | 10000 |
| DCE123 | 货车 | 0,5 | 300 | 30000 |

1. 打开表单的代码后文件。

2. 在 Fill Data Methods（填充数据方法）区域添加名为 `FillAvailableVehicles` 的方法。

3. 调用 `GetVehicles` 方法传递 `VehicleStatus.Available`，并将结果存储在名为 `vehicles` 的变量中。

```csharp
var vehicles = GetVehicles(VehicleStatus.Available);
```

4. 清空 `lvwAvailableVehicles` 列表视图的 `Items` 集合。

5. 通过调用 `AddRange` 方法将获取的车辆添加到 `Items` 集合中。

6. 从 `Form_Load` 事件调用 `FillAvailableVehicles` 方法。

# C# 入门

7. 运行应用程序并确保可用车辆显示在“租车”（Rent Vehicle）选项卡的列表视图控件中。

`FillAvailableVehicles` 方法的完整代码：

```csharp
private void FillAvailableVehicles()
{
    var vehicles = GetVehicles(VehicleStatus.Available);
    lvwAvailableVehicles.Items.Clear();
    lvwAvailableVehicles.Items.AddRange(vehicles.ToArray());
}
```

# RentVehicle: 租车辆

现在“租车”选项卡中的 `cboCustomers` 框和 `lvwAvailableVehicles` 列表视图已经填充了数据，是时候点击 `btnRent` 按钮来实现租车了。为了租车，你需要从组合框中的选中客户获取客户 ID，并从列表视图中的选中车辆获取车辆 ID。

由于你将创建的 `RentVehicle` 方法并没有获取数据并执行向 `TestData` 类中的 `Bookings` 集合中添加订单的操作，因此它应该被添加到相关类的 `Action Methods` 区域以及 `IRentalBase` 接口中。在 `CollectionDataLayer` 和 `BookingProcessor` 类中实现 `IRentalBase` 接口中的 `RentVehicle` 方法定义。当两个类都实现该方法后，可以使用添加到表单代码后的 `processor` 变量来调用订单处理的 `RentVehicle` 方法。

由于你希望该方法返回一个表示订单是否成功的 `bool` 值。接口中定义的方法有三个参数：两个名为 `vehicleId` 和 `customerId` 的 `int` 参数和一个名为 `timeReturnDate` 的 `DateTime` 参数。

# IRentalBase 接口

为了在 `CollectionDataLayer` 和 `BookingProcessor` 类中实现相同签名的 `RentVehicle` 方法，你需要将其添加到 `IRentalBase` 接口中；这将强制这两个类都实现该方法，因为它们实现了该接口。未能实现其中或两个类将导致编译异常，在添加方法之前应用程序将无法运行。

# C# 入门

1. 打开 `IRentalBase` 接口。

2. 在接口的 `Action Methods` 中添加名为 `RentVehicle` 的方法定义，带有三个参数：两个名为 `vehicleId` 和 `customerId` 的 `int` 参数和一个名为 `timeRental` 的 `DateTime`。记住接口只定义而从不包含逻辑。

目前 `IRentalBase` 接口的代码如下：

```csharp
public interface IRentalBase
{
    #region Action Methods
    bool RentVehicle(int vehicleId, int customerId, DateTime timeRental);
    #endregion

    #region Fetch Methods
    IEnumerable<ICustomer> GetCustomers();
    IEnumerable<IVehicle> GetVehicles(VehicleStatus status);
    IVehicle GetVehicleType(int vehicleId);
    #endregion
}
```

# CollectionDataLayer

在 `CollectionDataLayer` 中添加名为 `RentVehicle` 的方法以实现接口中定义的方法；你可以从接口复制定义，将其粘贴到类中并添加大括号。

该方法的逻辑是首先添加一个 `try/catch` 块，然后通过在 `TestData` 类中 `Bookings` 集合的最高订单 ID 上加 1 来生成一个新订单（注意订单将从数据库自动生成）。一旦获得订单，你就可以使用 `Bookings` 集合的 `Add` 方法，通过使用传递给 `RentVehicle` 的值和新订单 ID 创建 `Booking` 类的新实例来添加新订单。如果没有抛出异常，则从方法返回 `true`。

1. 在数据层项目中打开 `CollectionDataLayer`。

2. 在 `Action Methods` 区域实现 `RentVehicle` 方法。

3. 为方法添加 `try/catch` 块。

4. 通过调用 `Bookings` 集合的 `Max` 方法并指定你想要获取最大值的属性，生成一个从 ID 1 到最高订单 ID 的新订单。

```csharp
var bookingId = TestData.Bookings.Max(b => b.Id) + 1;
```

5. 通过调用 `Bookings` 集合上的 `Add` 方法并传递 `Booking` 类的新实例来添加新订单。

```csharp
TestData.Bookings.Add(new Booking() { Id = bookingId, CustomerID = customerID, Rented = timeRental, VehicleId = vehicleId });
```

6. 如果没有抛出异常，返回 `true`，否则返回 `false`。

目前 `CollectionDataLayer` 类的代码如下：

```csharp
public class CollectionDataLayer : IDataLayer
{
    public CollectionDataLayer() ...

    #region Action Methods
    public bool RentVehicle(int vehicleId, int customerID, DateTime timeRental)
    {
        try {
            // 订单通常由数据库提供
            var bookingId = TestData.Bookings.Max(b => b.Id) + 1;
            TestData.Bookings.Add(new Booking() {
                Id = bookingId,
                CustomerID = customerID,
                Rented = timeRental,
                VehicleId = vehicleId
            });
            return true;
        }
        catch {
            return false;
        }
    }
    #endregion
}
```

# C# 入门

```csharp
catch
{
    throw;
}
```

```csharp
#region 获取数据方法
public IEnumerable<ICustomer> GetCustomers() ...
public IEnumerable<IVehicle> GetVehicles(VehicleStatus status) ...
public IVehicleType GetVehicleType(int vehicleTypeId) ...
#endregion
```

```csharp
#region 辅助方法
#endregion
```

# BookingProcessor 类

为 `BookingProcessor` 类添加一个名为 `RentVehicle` 的方法，以实现 `IRentalBase` 接口中定义的方法；你可以从接口中复制定义，将其粘贴到类中并添加括号。

由于该方法没有需要实现的业务逻辑，这没有再简单了，你只需要返回调用 `CollectionDataLayer` 类中 `RentVehicle` 方法的结果即可，你可以通过你之前为 `BookingProcessor` 类添加的 `DataLayer` 属性访问它。你还应该实现异常处理，抛出从数据层抛出的任何异常。

1. 在业务层（Business Layer）项目打开打开 `BookingProcessor` 类。

2. 在操作方法（Action Methods）区域实现 `RentVehicle` 方法。

3. 在方法中添加 `try/catch` 块，其中 `catch` 块重新抛出异常。

4. 返回从数据层调用 `RentVehicle` 方法的结果。

```csharp
return DataLayer.RentVehicle(vehicleId, customerId, DateTime.Now);
```

目前为止完整的 `BookingProcessor` 类：

```csharp
public class BookingProcessor : IBookingProcessor
{
```
