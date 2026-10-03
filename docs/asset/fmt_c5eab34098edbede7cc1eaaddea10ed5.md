
```csharp
public class CollectionDataLayer : IDataLayer
{
    public CollectionDataLayer() ...

    #region Action Methods
    public bool RentVehicle(int vehicleId, int customerId, DateTime timeOfRental) ...
    public double ReturnVehicle(int bookingId, double meter, DateTime returned)
    {
        try
        {
            var booking = TestData.Bookings.FirstOrDefault(
                b => b.Id.Equals(bookingId) &&
                b.Rented.Equals(DateTime.MinValue));
            // 如果订单对象有问题，则抛出异常
            if (booking == null) throw new BookingException(bookingId);
            if (booking.VehicleId == null || booking.VehicleId < 1)
                throw new BookingException(bookingId);
            if (booking.Rented.Date == DateTime.MinValue)
                throw new BookingException(bookingId);
            if (booking.Rented.Date > returned)
                throw new BookingException(bookingId, "Rental date is greater than the return date.");
            if (returned == DateTime.MinValue)
                throw new BookingException(bookingId, "The car is still rented out.");
            var vehicle = TestData.Vehicles.FirstOrDefault(
                v => v.Id.Equals(booking.Id));
            // 如果车辆对象有问题，则抛出异常
            if (vehicle == null) throw new VehicleException(vehicle.Id, "The vehicle is not rented out.");
            if (vehicle.Meter > meter)
                throw new VehicleException(vehicle.Id, "The meter setting is lower than the current meter setting.");

            // 计算费用。
            var duration = RentalDuration(booking.Rented, returned);
            var cost = CalculatePrice(vehicle, meter, duration);
            booking.Returned = returned;
            booking.Cost = cost;
            vehicle.Meter = meter;

            return cost;
        }
        catch
        {
            throw;
        }
    }
    #endregion

    #region Fetch Methods
    public IEnumerable<ICustomer> GetCustomers() ...
    public IEnumerable<IVehicle> GetVehicles(VehicleStatus status) ...
    public IVehicleType GetVehicleType(int vehicleTypeId) ...
    #endregion

    #region Helper Methods
    public int RentalDuration(DateTime rented, DateTime returned) ...
    public double CalculatePrice(IVehicle vehicle, double returnedMeterSetting, int duration) ...
    #endregion
}
```

## BookingProcessor 类中的 ReturnVehicle 方法

在 `BookingProcessor` 类中添加一个名为 `ReturnVehicle` 的方法，以实现 `IRentalBase` 接口中定义的方法；你可以从接口拷贝定义，将其粘贴到类中并添加大括号。

该方法的逻辑与 `RentVehicle` 方法几乎相同。首先你添加一个 `try/catch` 块，并在 `try` 块中调用数据层实例属性上的 `ReturnVehicle` 方法。

1. 打开业务层项目中的 `BookingProcessor` 类。
2. 在 Action Methods 方法区域实现 `ReturnVehicle` 方法。
3. 为方法添加一个 `try/catch` 块。
4. 在 `try` 块中返回调用 `ReturnVehicle` 方法的结果，并传递必要的参数。
   `return DataLayer.ReturnVehicle(bookingId, meter, returned);`
5. 根据获取的订单的 `VehicleId` 属性获取车辆。
6. 在 `catch` 块中重新抛出异常。

`BookingProcessor` 类中 `ReturnVehicle` 方法的代码如下：

```csharp
public double ReturnVehicle(int bookingId, double meter, DateTime returned)
{
    try
    {
        return DataLayer.ReturnVehicle(bookingId, meter, returned);
    }
    catch
    {
        throw;
    }
}
```

## CollectionDataLayer 类中的 GetBookings 方法

在 `CollectionDataLayer` 类中添加一个名为 `GetBookings` 的方法，以实现 `IRental` 接口中定义的方法。

该方法的逻辑非常简单，你只需要返回 `TestData` 类中的 `Bookings` 集合。

1. 打开 `CollectionDataLayer` 类。
2. 在类的 Fetch Methods 添加一个无参数的 `IEnumerable<Booking>` 类型方法 `GetBookings`。
3. 返回 `TestData` 类中 `Bookings` 集合中的数据。

目前 `CollectionDataLayer` 类的代码如下：

```csharp
public class CollectionDataLayer : IDataLayer
{
    public CollectionDataLayer() ...

    #region Action Methods
    public bool RentVehicle(int vehicleId, int customerId, DateTime timeOfRental) ...
    public double ReturnVehicle(int bookingId, double meter, DateTime returned) ...
    #endregion

    #region Fetch Methods
    public IEnumerable<ICustomer> GetCustomers() ...
    public IEnumerable<IVehicle> GetVehicles(VehicleStatus status) ...
    public IVehicle GetVehicle(int vehicleId) ...
    public IEnumerable<IBooking> GetBookings()
    {
        return TestData.Bookings;
    }
    #endregion

    #region Helper Methods
    public int RentalDuration(DateTime rented, DateTime returned) ...
    public double CalculatePrice(IVehicle vehicle, double returnedSetting, int duration) ...
    #endregion
}
```

## IBookingProcessor 接口

你必须在 `IBookingProcessor` 接口中添加一个名为 `GetBooking` 的方法，带一个 `int` 参数 `vehicle`。该方法的目的是从 `IBooking` 接口返回单个 `Booking` 对象。

1. 打开 `IBookingProcessor`。
2. 添加带有 `int` 参数 `vehicle` 的 `IBooking` 定义。

目前 `IBookingProcessor` 的代码如下：

```csharp
public interface IBookingProcessor : IRentalBase
{
    IDataLayer DataLayer { get; }
    IBooking GetBooking(int vehicle);
}
```

## BookingProcessor 类中的 GetBooking 方法

你必须在 `BookingProcessor` 类中添加两个方法：`GetBookings` 和 `GetBooking`。`GetBookings` 方法的逻辑很容易实现，你只需要返回数据层 `Bookings` 集合中的所有订单。`GetBooking` 的逻辑稍微复杂，因为你必须使用 LINQ 根据车辆和是否已还从 `Bookings` 集合中获取特定订单。

1. 打开 `BookingProcessor` 类。
2. 在 Fetch Methods 区域添加一个无参数的 `IEnumerable<IBooking>` 类型方法 `GetBookings`。
3. 添加一个 `try/catch` 块，其中 `catch` 块重新抛出任何异常。
4. 返回调用 `DataLayer` 属性上的 `GetBookings` 方法的结果。
   `return DataLayer.GetBookings();`
5. 在 Fetch Methods 方法中添加一个名为 `GetBooking` 的公共方法，带一个 `int` 参数 `vehicle`。
6. 添加一个 `try/catch` 块，其中 `catch` 块重新抛出任何异常。
7. 返回一个 LINQ 查询结果，该查询使用 `GetBookings` 方法过滤出匹配传递车辆 ID 且其 `Returned` 属性为 `DateTime` 最小值的订单。
   `return (from b in DataLayer.GetBookings() where b.VehicleId.Equals(vehicleId) && b.Returned.Equals(DateTime.MinValue) select b).FirstOrDefault();`

目前 `BookingProcessor` 类的代码如下：

```csharp
public IBooking GetBooking(int vehicleId)
{
    try
    {
        return (from b in DataLayer.GetBookings()
                where b.VehicleId.Equals(vehicleId) &&
                b.Returned.Equals(DateTime.MinValue)
                select b).FirstOrDefault();
    }
    catch
    {
        throw;
    }
}
#endregion
#region Helper Methods
#endregion
```

## IsNumeric 方法

这是一个辅助方法，使用正则表达式来检查字符串是否为数值值。

```csharp
Regex regex = new Regex("^[-+]?[0-9]*\\.?[0-9]+$");
```

1. 打开表单的代码后文件。
2. 找到 Helper 区域并添加一个名为 `IsNumeric` 的 `bool` 方法，并带有一个名为 `text` 的字符串参数。
3. 创建一个新的 `RegEx` 对象，并将正则表达式传递给其构造函数。
   `Regex regex = new Regex(@"^[-+]?[0-9]*\.?[0-9]+$");`
4. 调用正则变量的 `IsMatch` 方法，将 `text` 参数中的字符串传递进去并返回结果。
   `return regex.IsMatch(text);`

`IsNumeric` 方法的完整代码：

```csharp
#region Helper Methods
bool IsNumeric(string text)
{
    Regex regex = new Regex("^[-+]?[0-9]*\\.?[0-9]+$");
    return regex.IsMatch(text);
}
#endregion
```

## 退还车辆

当用户点击 `btnReturn` 按钮、在 `lvwBookedVehicles` 列表视图中选择了一个车辆并在 `txtMeterTextbox` 中输入了一个值后，应通过向 `Returned` 属性返回当前日期来将车辆标记为已分配。应当计算费用并分配给 `Cost` 属性，并将当前的里程表值分配给该特定订单的 `Meter` 属性。这是通过调用订单处理器实例上的 `ReturnVehicle` 方法并传递订单 ID、里程表设置和当前日期来实现。

为了保持按钮 Click 事件中的代码整洁，你将在表单的 Action Methods 区域创建一个名为 `ReturnVehicle` 的方法，并在 Click 事件中调用它。

在方法中，你必须检查文本框中输入的值是否为数字，如果不是，则向用户显示消息并返回 `false`。你还需要检查列表视图中是否选择了车辆，如果没有选择车辆，则显示消息并返回 `false`。

从列表视图的选中项中获取车辆 ID，并将值存储在名为 `vehicleId` 的变量中。然后通过调用处理器实例上的 `GetBooking` 方法获取订单 ID，并将结果存储在名为 `booking` 的变量中。

调用处理器实例的 `ReturnVehicle` 方法，传递订单 ID、里程表设置和当前日期以返回所选车辆。

调用 `FillAvailableVehicles` 和 `FillBookedVehicles` 方法更新列表视图的内容。

为文本框的 `Text` 属性分配空字符串并从方法返回 `true`。

如果抛出异常，则返回 `false`。

1. 打开表单的代码后文件。
2. 找到 Action Methods 区域并向其中添加一个私有的、无参数 `bool` 方法 `ReturnVehicle`。
3. 添加一个名为 `success` 的 `bool` 变量并赋值为 `false`。
4. 添加一个 `try/catch` 块，在 `catch` 块中将 `success` 变量赋值为 `false`。
5. 添加一个 `if` 语句，通过调用之前定义的 `IsNumeric` 方法检查文本框中的变量是否不是数字，如果语句为真，则向用户显示消息并返回 `success` 变量的值。
   `if (!IsNumeric(txtMeterReturn.Text))`
6. 添加一个 `if` 语句，检查列表视图中是否没有选择车辆，如果语句为真，则向用户显示消息并返回 `success` 变量的值。
   `if (lvwBookedVehicles.SelectedItems.Count == 0)`
7. 通过解析列表视图中选中车辆的 ID 获取车辆 ID。
   `var vehicleId = Int32.Parse(lvwBookedVehicles.SelectedItems[0].SubItems[5].Text);`
8. 通过调用处理器实例上的 `GetBooking` 方法并传递车辆获取订单 ID。
   `var bookingId = processor.GetBooking(vehicleId).Id;`
9. 通过调用处理器实例上的 `ReturnVehicle` 方法并传递订单 ID、里程表设置和当前日期来返回车辆。
   `processor.ReturnVehicle(bookingId, Double.Parse(txtMeterReturn.Text), DateTime.Now);`
10. 调用 `FillAvailableVehicles` 和 `FillBookedVehicles` 方法更新列表视图。
11. 清空文本框。
12. 将 `success` 变量赋值为 `true`。
13. 在方法末尾添加一个返回语句，返回 `success` 变量的值。
14. 在 Button Events 区域为 `btnReturn` 按钮添加 Click 事件。
