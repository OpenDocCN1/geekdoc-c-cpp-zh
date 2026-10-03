
<?xml version="1.0"?>
<ArrayOfCustomer xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <Customer>
    <Id>1</Id>
    <SocialSecurityNumber>12324545</SocialSecurityNumber>
    <FirstName>Carl</FirstName>
    <LastName>Raintree</LastName>
  </Customer>
  <Customer>
    <Id>2</Id>
    <SocialSecurityNumber>95654123</SocialSecurityNumber>
    <FirstName>Lisa</FirstName>
    <LastName>Montgomery</LastName>
  </Customer>
</ArrayOfCustomer>

JSON 序列化基于 JavaScript 的子集，通常用于涉及使用 AJAX 从 JavaScript 进行异步调用。你不局限于同一个域，且 JSON 是轻量级的、人类可读的、易于解析的与平台无关的。必须引用 `System.Runtime.Serialization` 程序集并向 `System.Runtime.Serialization.Json` 添加 using 语句。

或者，在序列化到 JSON 时，可以使用 `System.Web.Extensions` 程序集中的 `JavaScriptSerializer`（见下例）。

以下代码显示了 JSON 输出示例：

```json
[{"Id":"1","SocialSecurityNumber":"12324545","FirstName":"Carl","LastName":"Raintree"},\n{"Id":"2","SocialSecurityNumber":"95654123","FirstName":"Lisa","LastName":"Montgomery"}]
```

# 序列化与反序列化

当你需要添加某些序列化代码以使类可序列化时，请在类定义上方添加 `[Serializable]` 特性并实现 `ISerializable` 接口；此接口包含 `GetObjectData` 方法定义，该方法在序列化数据时使用。你还需要添加一个接受两个参数 `SerializationInfo` 和 `StreamingContext` 的构造函数。此构造函数用于将数据反序列化为对象。如果你想在序列化过程中忽略某些字段，请向字段上添加 `[NonSerialized]` 特性。

```csharp
[Serializable]
public class Customer {
    public int Id { get; set; }
    public string SocialSecurityNumber { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    [NonSerialized]
    public string TempValue { get; set; }
}
```

# 二进制序列化

二进制序列化要求类被标记为 `[Serializable]` 特性。要使用二进制序列化序列化对象，你需要创建一个 `BinaryFormatter` 类的实例。接下来，你需要使用 `File` 或 `FileStream` 类创建一个文件来持久化对象。要序列化对象，你可以在 `BinaryFormatter` 实例上调用 `Serialize` 方法，并传递文件流和你想序列化的对象。不要忘记使用文件流上的 `Close` 方法关闭文件流。

示例中的 `GetCustomers` 方法返回一个 `List<Customer>` 集合。

```csharp
var formatter = new BinaryFormatter();
using (var stream = File.Create(@"C:\Test\binary.txt")) {
    formatter.Serialize(stream, GetCustomers());
}
```

# 二进制反序列化

要反序列化对象以打开以二进制格式存储的实例，你需要创建一个 `BinaryFormatter` 类的实例。要打开包含数据的文件，请使用 `File` 或 `FileStream` 类上的 `OpenRead` 方法。要重建对象，你可以在 `BinaryFormatter` 实例上调用 `Deserialize` 方法，传递文件流并将结果存储在序列化类型的实例变量中。不要忘记使用文件实例上的 `Close` 方法关闭文件流。

```csharp
var formatter = new BinaryFormatter();
using (var stream = File.OpenRead(@"C:\Test\binary.txt")) {
    var customers = (List<Customer>)formatter.Deserialize(stream);
}
```

# XML 序列化

要使用 XML 序列化序列化对象，你需要创建一个位于 `System.Xml.Serialization` 中的 `XmlSerializer` 实例。使用 `File` 或 `FileStream` 类创建你想持久化对象的文件。要序列化对象，你可以在 `XmlSerializer` 实例上调用 `Serialize` 方法，传递文件流和你想序列化的对象。不要忘记使用文件流上的 `Close` 方法关闭文件流。

示例中的 `GetCustomers` 方法返回一个 `List<Customer>` 集合。

```csharp
var serializer = new XmlSerializer(typeof(List<Customer>));
using (var stream = File.Create(@"C:\Test\binary.txt")) {
    serializer.Serialize(stream, GetCustomers());
}
```

# XML 反序列化

要将 XML 格式的对象反序列化以打开一个实例，你需要创建一个 `XmlSerializer` 类的实例。打开包含数据的文件，使用 `File` 或 `FileStream` 类上的 `OpenRead` 方法。要重建对象，你可以在 `XmlSerializer` 实例上调用 `Deserialize` 方法，传递文件流并将结果存储在序列化类型的实例变量中。不要忘记使用文件实例上的 `Close` 方法关闭文件流。你必须反序列化为正确的数据，在这种情况下是 `List<Customer>`。

```csharp
var xml = File.ReadAllText(@"C:\Test\binary.txt");
var deserializer = new XmlSerializer(typeof(List<Customer>));
using (var reader = new StreamReader(xml)) {
    var customers = (List<Customer>)deserializer.Deserialize(reader);
}
```

# JSON 序列化

你需要创建一个 `JavaScriptSerializer` 类并传入你要序列化的对象的类类型。使用 `File` 或 `FileStream` 类创建你想持久化对象的文件，并使用 `WriteAllText` 方法持久化数据。

**重要：** 你需要引用 `System.Web.Extensions` 程序集以访问 `JavaScriptSerializer` 类。

**注意：** 有其他 .NET 和第三方（JSON.NET）程序集可以在序列化到 JSON 时使用。

示例中的 `GetCustomers` 方法返回一个 `List<Customer>` 集合。

```csharp
string json = new JavaScriptSerializer().Serialize(GetCustomers());
File.WriteAllText(@"C:\test\json.txt", json);
```

# JSON 反序列化

要将持久化的对象反序列化为 JSON 格式的对象实例，你需要使用 `File` 类上的 `ReadAllText` 方法打开包含对象数据的文件。要重建对象，你可以在 `JavaScriptSerializer` 实例上调用 `Deserialize` 方法，传递从文件中读取的数据并将结果存储在变量类型的实例中。

```csharp
string json = File.ReadAllText(@"C:\test\json.txt");
var customers = new JavaScriptSerializer().Deserialize<List<Customer>>(json);
```

# 练习：租车 - 数据持久化

在此练习中，你将使用 JSON 序列化和反序列化为 **Car Rental** 添加持久化功能。

你需要完成的第一项工作是在 **Data Layer** 项目中为 `System.Web.Extensions` 程序集添加引用。

# C# 入门

创建一个描述为 Serialize/Deserialize the CollectionDataLayer 类的新区域（region），并将在此练习中创建的所有方法放入该区域内。

添加一个名为 `ISerialize` 的新公共接口，其中包含一个名为 `Serialize` 的 `void` 方法，该方法有一个名为 `path` 的字符串参数。`IDataLayer` 接口应继承 `ISerialize` 接口。在 `CollectionDataLayer` 类中实现 `Serialize` 方法；使用 `JavaScriptSerializer` 对象的 `Serialize` 方法来序列化 `TestData` 类和 `File` 类中的集合，并使用 `WriteAllText` 方法将数据持久化到文件中。

```csharp
File.WriteAllText(path + @"Bookings.txt", new JavaScriptSerializer().Serialize(TestData.Bookings));
```

在 `CollectionDataLayer` 类中添加四个名为 `DeserializeBookings`、`DeserializeCustomers`、`DeserializeVehicles` 和 `DeserializeVehicleTypes` 的方法，这些方法用于反序列化各自文件中的数据并返回获取数据的相应集合。查找该特定集合的类应使用 `File` 类的 `ReadAllText` 方法读取。将获取的数据传递给 `JavaScriptSerializer` 类的一个实例的 `Deserialize` 方法，并返回该方法的的结果。

```csharp
string json = File.ReadAllText(path);
return new JavaScriptSerializer().Deserialize<List<Booking>>(json);
```

添加一个名为 `Seed` 的 `void` 方法，它有一个名为 `path` 的字符串参数，将通过调用你刚刚添加的 `Deserialize` 方法将数据加载到相应的集合中。一旦通过调用 `TestClass.Seed` 方法创建了文件，就在 `CollectionDataLayer` 类中调用此方法来替换它。

你可以使用 `FormClosing` 事件在每次表单关闭时将数据持久化到文件中。调用处理器实例中 `DataLayer` 实例的 `Serialize` 方法。

```csharp
processor.DataLayer.Serialize(@"C:\Test\");
```

# 添加 ISerialize 接口

1. 在 Data Layer 项目的 Interfaces 文件夹中添加一个名为 `ISerialize` 的接口。
2. 将接口的访问性更改为 public（公共）。

# C# 入门

3. 为一个名为 `Serialize` 的 `void` 方法添加方法定义，该方法有一个名为 `path` 的字符串参数。
4. 打开 `IDataLayer` 接口并继承 `ISerialize` 接口。

```csharp
public interface IDataLayer : IRentalBase, ISerialize
```

`ISerialize` 接口的完整代码：

```csharp
public interface ISerialize {
  void Serialize(string path);
}
```

# 实现 ISerialize 接口

1. 打开 `CollectionDataLayer` 类。
2. 添加一个描述为 Serialize/Deserialize 的区域（region）。
3. 在区域中添加一个名为 `Serialize` 的 `void` 方法，该方法有一个名为 `path` 的字符串参数。
4. 调用 `File` 类的 `WriteAllText` 方法来持久化序列化数据。将要创建文件的路径和文件名作为其第一个参数，将序列化数据作为第二个参数。如下面的代码所示，该调用被压缩了一行代码。

```csharp
File.WriteAllText(path + @"Bookings.txt", new JavaScriptSerializer().Serialize(TestData.Bookings));
```

`Serialize` 方法的完整代码：

```csharp
public void Serialize(string path) {
  /* 需要引用 System.Web.Extensions 程序集 */
  File.WriteAllText(path + @"Bookings.txt",
    new JavaScriptSerializer().Serialize(TestData.Bookings));
  File.WriteAllText(path + @"Customers.txt",
    new JavaScriptSerializer().Serialize(TestData.Customers));
  File.WriteAllText(path + @"Vehicles.txt",
    new JavaScriptSerializer().Serialize(TestData.Vehicles));
  File.WriteAllText(path + @"VehicleTypes.txt",
    new JavaScriptSerializer().Serialize(TestData.VehicleTypes));
}
```

# C# 入门

# 实现四个反序列化方法

1. 打开 `CollectionDataLayer` 类。
2. 找到 Serialize/Deserialize 区域。
3. 添加一个名为 `DeserializeBookings` 的 `private List<Booking>` 方法，该方法有一个字符串参数 `path`。
4. 使用 `File` 类的 `ReadAllText` 方法获取存储在路径参数指定中的 JSON 数据。将结果存储在字符串变量 `json` 中。

```csharp
string json = File.ReadAllText(path);
```

5. 返回调用 `JavaScriptSerializer` 类实例的 `Deserialize` 方法的结果：`return new JavaScriptSerializer().Deserialize<List<Booking>>(json);`
6. 对其他方法 `DeserializeCustomers`、`DeserializeVehicles` 和 `DeserializeVehicleTypes` 以及 `TestData` 类中对应的集合 `Customers`、`Vehicles` 和 `VehicleTypes` 重复上述步骤。

反序列化方法的完整代码：

```csharp
/* 需要引用 System.Web.Extensions 程序集 */
private List<Booking> DeserializeBookings(string path) {
    string json = File.ReadAllText(path);
    return new JavaScriptSerializer().Deserialize<List<Booking>>(json);
}
```

```csharp
private List<Customer> DeserializeCustomers(string path) {
    string json = File.ReadAllText(path);
    return new JavaScriptSerializer().Deserialize<List<Customer>>(json);
}
```

```csharp
private List<Vehicle> DeserializeVehicles(string path) {
    string json = File.ReadAllText(path);
    return new JavaScriptSerializer().Deserialize<List<Vehicle>>(json);
}
```

```csharp
private List<VehicleType> DeserializeVehicleTypes(string path) {
    string json = File.ReadAllText(path);
    return new JavaScriptSerializer().Deserialize<List<VehicleType>>(json);
}
```
