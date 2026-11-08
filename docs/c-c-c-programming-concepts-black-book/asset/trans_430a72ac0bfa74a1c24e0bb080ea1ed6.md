
C# 借助 Enum 类和 enum 关键字实现枚举。Enum 类提供了用于操作该类实例的方法。枚举技术提供了一种高效的方式来定义一组整型常量，这些常量可以使用 enum 类型赋给变量。enum 中的每个元素都与一个基础类型相关联，该类型默认为整数。在本节中，我们讨论在 .NET 中使用 enum 类型实现枚举器。

### 清单 18.38：展示枚举器示例

```csharp
using System;
class Enumeration
{
    // Defining enum
    public enum SortingOrder
    {
        Ascending,
        Descending,
        NotDefined
    }
    public static void Main()
    {
        // Type casting the enum variable
        SortingOrder sortingorder = SortingOrder.Descending;
        switch (sortingorder)
        {
            case SortingOrder.Ascending:
                Console.WriteLine("Please sort in Ascending order");
                break;
            case SortingOrder.Descending:
                Console.WriteLine("Please sort in Descending order");
                break;
            case SortingOrder.NotDefined:
                Console.WriteLine("Please provide the sorting order");
                break;
        }
    }
}
```

在前面的代码中，关键字 enum 用于定义 SortingOrder 枚举器，其成员为 Ascending、Descending 和 NotDefined。由于没有为 enum 中的成员定义基础类型，编译器会自动为枚举成员分配 0、1 和 2。换言之，它将 0 分配给 Ascending，将 1 分配给 Descending，将 2 分配给 NotDefined。此外，我们在 Main() 方法中使用持有枚举成员 Descending 基础值的 enum 变量 sortingOrder，定义了一个名为 sortingOrder 的 enum 变量。

前面程序的输出如下：

```text
Please sort in Descending order
```

接下来，我们考虑另一个示例，它展示了枚举中类型转换的重要性，如清单 18.39 所示：

### 清单 18.39：实现枚举器的类型转换

```csharp
using System;
class Enumeration
{
    public enum Flammable
    {
        High,
        Low
    }
    public enum SpeedLimit
    {
        High = 100,
        Low = 10
    }
    public static void Main()
    {
        // Type casting to avoid conflict
        Type flammable = typeof(Flammable);
        Type speedLimit = typeof(SpeedLimit);
        // Printing the Enums
        foreach (string flammableEnum in Enum.GetNames(flammable))
        {
            Console.WriteLine("The flammable enums are:" + flammableEnum);
        }
        foreach (string speedLimitEnum in Enum.GetNames(speedLimit))
        {
            Console.WriteLine("The speed limit enums are:" + speedLimitEnum);
        }
    }
}
```

在前面的程序中，两个枚举的成员及其基础类型相同，但值不同。最大速度限制为 100（km/hr），最小速度限制为 10（km/hr）；而可燃对象的 High 和 Low 的基础值分别为 0 和 1。前面程序的输出如下：

```text
The flammable enums are:High
The flammable enums are:Low
The speed limit enums are:Low
The speed limit enums are:High
```

现在，如果我们只是编写前面的程序，在其中使用成员 High 而不应用类型转换，那么这将产生错误，因为该成员存在两个值，如清单 18.40 所示：

### 清单 18.40：展示枚举的歧义实现

```csharp
using System;
class EnumOperation
{
    public enum Flammable
    {
        High,
        Low
    }
    public enum SpeedLimit
    {
        High = 100,
        Low = 10
    }
    public static void Main()
    {
        Console.WriteLine("The highest member value of SpeedLimit enum is" + High);
    }
}
```

因此，我们应该始终对枚举的成员进行类型转换，以避免该错误。

如清单 18.39 所示，我们使用 Enum 类获取成员变量名称的列表。Enum 类属于基类库（BCL）。

### 表 18.2：Enum 类中值得注意的成员方法

| 成员方法 | 描述 |
|---|---|
| Equals (object obj1, object obj2) | 确定传入的两个对象实例是否相似。如果相似，则返回 true，否则返回 false。 |
| Format(Type enumType, Object obj, string format) | 将 enumType 的 obj 转换为作为参数传入的特定格式，然后返回已转换对象的字符串类型。 |
| GetName(Type enumType, Object obj) | 返回参数列表中指定的 enumType 对象的名称。 |
| GetNames(Type enumType) | 返回一个字符串数组，其中包含参数中指定的特定 enumType 的名称。 |
| GetUnderlyingType(Type enumType) | 返回 Type 的实例，其中包含参数中指定的 enumType 的基础类型。 |
| GetValues(Type enumType) | 返回 Array 类的对象，其中包含与参数中指定的 enumType 相关联的常量值列表。 |
| IsDefined(Type enumType, Object obj) | 如果已为参数中指定的 enumType 的特定 Object 类型定义了该常量值，则返回 true。 |
| Parse(Type enumType, Object obj) | 将 enumType 的名称或常量转换为等效的枚举对象，并在最后返回该对象。<br>重载：<br>• Parse (Type enumType, Object obj, bool ignoreCase)➔如果 ignoreCase 设置为 true，则忽略大小写。 |
| ReferenceEquals (object obj1, object obj2) | 如果对象的所有实例都是同一对象，则返回 true；否则返回 false。 |
| ToObject (Type enumType, ulong value) | 返回设置为指定 64 位无符号整数值的枚举类型对象。<br>重载：<br>• ToObject (Type enumType, byte value)➔返回设置为指定 8 位无符号整数值的枚举类型实例。<br>• ToObject (Type enumType, int value)➔返回设置为指定 32 位有符号整数值的枚举类型实例。<br>• ToObject (Type enumType, long value)➔返回设置为指定 64 位有符号整数值的枚举类型实例。<br>• ToObject (Type enumType, object value)➔返回设置为 object 类型值的枚举类型实例。<br>• ToObject (Type enumType, sbyte value)➔返回设置为指定 8 位有符号整数值的枚举类型实例。<br>• ToObject (Type enumType, short value)➔返回设置为指定 16 位有符号整数值的枚举类型实例。<br>• ToObject (Type enumType, uint value)➔返回设置为指定 32 位无符号整数值的枚举类型实例。<br>• ToObject (Type enumType, ushort value)➔返回设置为指定 16 位无符号整数值的枚举类型实例。 |

现在让我们学习 C# 中的泛型。

## 泛型

在上一章中，我们已经学习了数组和 ArrayList，以及它们在 .NET 平台中的工作方式。因此，ArrayList 是一种基于对象的数据结构。然而，这类数据结构的主要问题在于，在插入值类型元素之前，我们需要将其装箱为 Object 类型，然后再拆箱以检索确切类型的元素。这会降低程序的性能，因为装箱和拆箱会带来显著的性能损失，因为它会对托管堆造成更大压力，从而导致更多的垃圾回收。因此，我们可以说 ArrayList 不是类型安全的。另一方面，Array 是类型安全的，但数组大小受到限制；而 ArrayList 中没有大小限制。因此，Array 和 ArrayList 各有优缺点。在 C# 中，泛型结合了数组和 ArrayList 的优点，为用户提供类型安全的集合。

在本节中，我们将介绍 Dictionary 的泛型集合。要访问该集合，我们需要在程序中添加以下程序集引用：

```csharp
using System.Collections.Generic;
```

使用此引用，我们可以实现诸如 `List<T>` 和 `Dictionary<Key, Value>` 之类的集合。可以如下声明 List，其中 T 表示类型：

```csharp
List<T> list = new List<T>();
```

如果我们想创建一个包含字符串的 List，那么可以如下声明它：

```csharp
List<string> list = new List<string>();
```

另一方面，Dictionary 集合表示一个键值列表，其中为所有已定义的文本都有一个键。我们可以如下声明 Dictionary 集合：

```csharp
Dictionary<key, value> list = new Dictionary<key, value>();
```

### 清单 18.41：展示 Dictionary 集合示例

```csharp
using System;
using System.Collections.Generic;
class Program
{
    public static void Main()
    {
        // Declaring the generic Dictionary
        Dictionary<int, Customer> customerList = new Dictionary<int, Customer>();
        CustomerIndexer customers = new CustomerIndexer();
        customers[0] = new Customer(10, "Customer_1");
        customers[1] = new Customer(20, "Customer_2");
        customers[2] = new Customer(30, "Customer_3");
        // Adding the customer information to Dictionary object
        for (int i = 0; i < 3; i++)
        {
            customerList.Add(i + 1, customers[i]);
        }
        Console.WriteLine("The customers are:");
        // Printing the Dictionary content
        foreach (KeyValuePair<int, Customer> custKeyVal in customerList)
        {
            Console.WriteLine("Customer ID: {0}, Name: {1}",
                custKeyVal.Key,
                custKeyVal.Value.custName);
        }
    }
    class Customer
```
