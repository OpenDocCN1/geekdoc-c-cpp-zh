
- 5. 为名为 `VehicleException` 和 `CustomerException` 的两个类重复 1-4 点，更改 `message` 参数的默认文本。

`BookingException` 类的完整代码：

```csharp
public class BookingException : KeyNotFoundException
{
    public int Id { get; private set; }

    public BookingException(int id, string message = "The given booking id does not exist") : base(message)
    {
        Id = id;
    }
}
```

`VehicleException` 类的完整代码：

```csharp
public class VehicleException : KeyNotFoundException
{
    public int Id { get; private set; }

    public VehicleException(int id, string message = "The given vehicle id does not exist") : base(message)
    {
        Id = id;
    }
}
```

## IDataLayer 接口

为了在 `CollectionDataLayer` 类中实现 `RentalDuration` 和 `CalculatePrice` 方法，你需要将其添加到 `IDataLayer` 接口中；这将强制类实现这些方法。未在类中实现这些方法将导致编译异常，在添加方法之前应用程序无法运行。

1. 打开 `IDataLayer` 接口。
2. 在接口的 `Helper Methods` 区域定义一个名为 `RentalDuration` 的 `int` 方法，带有两个名为 `rented` 和 `returned` 的 `DateTime` 参数。记住接口定义成员且永远不包含逻辑。

   `int RentalDuration(DateTime rented, DateTime returned);`

3. 定义一个名为 `CalculatePrice` 的 `double` 方法，包含三个参数：一个名为 `vehicle` 的 `IVehicle` 参数、一个名为 `returnedMeterSetting` 的 `double` 参数和一个名为 `duration` 的 `int` 参数。将方法添加到接口的 `Helper Methods` 区域。

   `double CalculatePrice(IVehicle vehicle, double returnedMeterSetting, int duration);`

`IDataLayer` 接口的完整代码：

```csharp
public interface IDataLayer : IRentalBase
{
    #region Helper Methods
    int RentalDuration(DateTime rented, DateTime returned);

    double CalculatePrice(IVehicle vehicle, double returnedMeterSetting, int duration);
    #endregion
}
```

## RentalDuration 方法

此在 `IDataLayer` 接口中定义的方法通过从归还日期减去租赁日期来计算车辆租赁了多久，并将结果存储在一个名为 `TimeSpan` 对象中。使用传入的 `TimeOfDay` 参数来检查租赁时长是否在接受范围内；如果 `time` 对象的 `Days` 属性等于零，且 `returned` 和 `rented` 的 `TimeOfDay` 属性之差大于时间跨度的最小值，则返回 1，否则返回 `time` 对象的 `Days` 属性值。

```csharp
if (time.Days == 0 && returned.TimeOfDay - rented.TimeOfDay > TimeSpan.MinValue)
```

在 `CollectionDataLayer` 的 `Helper Methods` 区域添加 `RentalDuration`。该方法应有两个名为 `rented` 和 `returned` 的 `DateTime` 参数，并返回一个表示车辆租赁天数的 `int` 值。

1. 打开 `CollectionDataLayer` 类。
2. 在 `Helper Methods` 区域添加名为 `RentalDuration` 的方法，带有名为 `rented` 和 `returned` 的 `DateTime` 参数。

   `public int RentalDuration(DateTime rented, DateTime returned)`

3. 添加一个名为 `time` 的 `TimeSpan` 变量，并将 `returned` 和 `rented` 参数之间的差的结果赋值给它。
4. 添加一个 `if` 语句检查天数是否为零，如果是则返回 1，否则返回 `time` 变量计算的天数。

### C# 初学者

```csharp
if (time.Days == 0 && returned.TimeOfDay - rented.TimeOfDay > 
TimeSpan.MinValue)
  return 1;
else
  return time.Days;
```

`RentalDuration` 方法的完整代码：

```csharp
public class CollectionDataLayer : IDataLayer
{
  public CollectionDataLayer()...

  #region Action Methods
  public bool RentVehicle(int vehicleId, int
  customerID, DateTime timeOfRental) ...
  #endregion

  #region Fetch Methods
  public IEnumerable<ICustomer> GetCustomers() ...
  public IEnumerable<IVehicle> GetVehicles(VehicleStatus status) ...
  public IVehicle GetVehicle(int vehicleId) ...
  #endregion

  #region Helper Methods
  public int RentalDuration(DateTime rented, DateTime returned)
  {
    TimeSpan time = returned - rented;

    if (time.Days == 0 &&
      returned.TimeOfDay - rented.TimeOfDay > TimeSpan.MinValue)
      return 1;
    else
      return time.Days;
  }
  #endregion
}
```

## CalculatePrice 方法

此方法定义在 `IDataLayer` 接口中，将根据用例指定的公式计算客户租赁车辆应支付的费用（见下文）。返回 `double` 的 `CalculatePrice` 方法应添加到 `CollectionDataLayer` 类的 `Helper Methods` 区域中，并包含三个参数：`IVehicle` 类型的 `vehicle`、`int` 类型的 `returnedMeterSetting` 以及 `int` 类型的 `duration`。

### C# 初学者

- **轿车 (Sedan)**：价格 = 每日费用 * 天数
- **多功能车 (Combi)**：价格 = 每日费用 * 天数 * 日费 + 每公里费用 * 实际行驶里程。日费初始为 1.5，但可以随时间更改。
- **货车 (Van)**：价格 = 每日费用 * 天数 * 日费 + 每公里费用 * 实际行驶里程 * 距离费。日费初始为 2.0，距离费初始为 2.5，但可以随时间更改。

1. 打开 `CollectionDataLayer` 类。
2. 在 `Helper Methods` 区域添加一个名为 `CalculatePrice` 的方法，并包含三个参数：`IVehicle` 类型的 `vehicle`、`int` 类型的 `returnedMeterSetting` 以及 `int` 类型的 `duration`。
3. 计算价格并从方法返回结果。

```csharp
public double CalculatePrice(IVehicle vehicle, double
returnedMeterSetting, int duration)
return vehicle.BasePricePerDay * duration * vehicle.DayTariff +
vehicle.BasePricePerKm * (returnedMeterSetting - vehicle.Meter) *
vehicle.KmTariff;
```

`CalculatePrice` 方法的完整代码：

```csharp
public double CalculatePrice(IVehicle vehicle, double
returnedMeterSetting, int duration)
{
    return vehicle.BasePricePerDay * duration * vehicle.DayTariff +
    vehicle.BasePricePerKm *
    (returnedMeterSetting - vehicle.Meter) *
    vehicle.KmTariff;
}
#endregion
```

## IRentalBase 接口

要在 `CollectionDataLayer` 和 `BookingProcessor` 类中实现具有相应签名的 `ReturnVehicle` 和 `GetBookings` 方法，你需要将它们添加到 `IRentalBase` 接口中；这将强制这两个类实现这些方法，因为它们实现了该接口。未实现这些方法会导致编译失败；该方法在系统中使用，在添加这些方法之前，应用程序将无法运行。

`ReturnVehicle` 方法用于还车并更改 `TestData` 类中 `Bookings` 集合中的 `Booking` 对象。`GetBookings` 方法返回系统中的所有订单，并当 `BookingProcessor` 类中使用 `GetBooking` 方法获取单个订单时作为基础。

1. 打开 `IRentalBase` 接口。
2. 在接口的 `Action Methods` 区域添加一个名为 `ReturnVehicle` 的 `double` 方法，包含三个参数：一个名为 `bookingId` 的 `int` 参数、一个名为 `meter` 的 `double` 参数以及一个名为 `Returned` 的 `DateTime` 参数。记住，接口只定义成员，绝不包含任何逻辑。

   `double ReturnVehicle(int bookingId, double meter, DateTime returned);`

3. 在接口的 `Fetch Methods` 区域添加一个无参数的 `IEnumerable<IBooking>` 方法 `GetBookings`。

   `IEnumerable<IBooking> GetBookings();`

### C# 初学者

到目前为止 `IRentalBase` 接口的完整代码：

```csharp
public interface IRentalBase
{
    #region Action Methods
    bool RentVehicle(int vehicleId, int customerId, DateTime timeRental);
    double ReturnVehicle(int bookingId, double meter, DateTime returned);
    #endregion
    #region Fetch Methods
    IEnumerable<ICustomer> GetCustomers();
    IEnumerable<IVehicle> GetVehicles(VehicleStatus status);
    IVehicle GetVehicleType(int vehicleTypeId);
    IEnumerable<IBooking> GetBookings();
    #endregion
}
```

## CollectionDataLayer 类中的 ReturnVehicle 方法

在 `CollectionDataLayer` 类中添加一个名为 `ReturnVehicle` 方法来实现 `IRentalBase` 接口中定义的方法；你可以从接口拷贝定义，将其粘贴到类中并添加大括号。

该方法的逻辑比之前的方法更复杂。首先，你添加一个 `try/catch` 块，然后在使用 `booking` 和 `vehicle` 对象进行计算之前，检查一组可能导致订单异常和车辆异常的条件。

以下条件将导致方法在计算租赁时长和费用之前抛出 `BookingException`：

- 获取的 `booking` 对象为 `null`，这意味着在 `Bookings` 集合中不存在传入 id 对应的订单对象。
- 获取的 `booking` 对象中的 `Vehicle` 属性为 `null` 或小于 1。
- 获取的 `booking` 对象中的 `DateOfTheRented` 属性等于日期的最小值。
- 获取的 `booking` 对象中的 `DateOfTheRented` 属性大于日期。
- 传入方法的 `returned` 参数等于日期的最小值。这意味着车辆已租赁但尚未归还。

以下条件将导致你在计算租赁时长和费用之前抛出 `VehicleException`：

- 获取的车辆对象为 `null`。
- 获取的车辆对象中的 `Meter` 属性大于通过方法 `meter` 参数传入的设置值。

如果没有抛出异常，则可以调用 `RentalDuration` 和 `CalculatePrice` 方法来计算租赁时长和费用。其用途是为获取的 `booking` 的 `Returned`、`Cost` 和 `Meter` 属性赋值以完成还车。

1. 在 Data Layer 项目中打开 `CollectionDataLayer` 类。
2. 在 `Action Methods` 区域实现 `ReturnVehicle` 方法。
3. 为方法添加 `try/catch` 块。
4. 获取匹配传入的 `bookingId` 且 `Returned` 属性包含日期最小值的订单。将该订单存储在名为 `booking` 的变量中。

   ```csharp
   var booking = TestData.Bookings.FirstOrDefault(b =>
   b.Id.Equals(bookingId) && b.Returned.Equals(DateTime.MinValue));
   ```

5. 为可能触发订单异常的条件添加 `if` 语句。
6. 获取与获取的 `booking` 中的 `Vehicle` 属性匹配的车辆。

   ```csharp
   var vehicle = TestData.Vehicles.FirstOrDefault(v =>
   v.Id.Equals(booking.Vehicle));
   ```

7. 为可能触发车辆异常的条件添加 `if` 语句。
8. 调用 `RentalDuration` 方法，传入 `booking` 对象的 `Rented` 属性值和传入方法的 `returned` 参数，以计算车辆租赁时长，将结果存储在变量 `duration` 中。
9. 调用 `CalculatePrice` 方法，传入车辆对象、`meter` 参数和计算出的时长，将结果存储在变量 `cost` 中。
10. 将 `returned` 参数的值赋值给 `booking` 对象的 `Returned` 属性。
11. 将 `cost` 变量的值赋值给 `booking` 对象的 `Cost` 属性。
12. 将 `meter` 参数的值赋值给 `booking` 对象的 `Meter` 属性。
13. 从方法返回 `cost` 变量。
14. 在 `catch` 块中重新抛出任何异常。

### C# 初学者

目前 `CollectionDataLayer` 类中的代码如下：
