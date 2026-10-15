
从 SQL Server 2005 开始，你可以使用 Visual Basic 创建 UDT。除了用户定义类型的常规优点之外，使用 Visual Basic 编写的 UDT 还有一个优点——它们还可以以方法的形式提供功能，这意味着你可以通过提供这些方法来扩展数据库的功能。

使用 Visual Basic 编写的 UDT 是作为结构或类实现的。由于 Visual Studio 默认将 UDT 创建为结构，因此这里假定采用结构形式，但请记住，你也可以将它们创建为类。结构的属性或字段成为 UDT 的子类型。公共方法也可以访问，就像在 Visual Basic 应用程序中一样。

除了编写结构时所使用的常规代码之外，你还需要实现其他项，以使 UDT 能在 SQL Server 中正常工作。首先，你的结构应具有 `Microsoft.SqlServer.Server.SqlUserDefinedType` 特性。该特性将结构标识为 SQL Server UDT。此外，强烈建议使用 `Serializable` 特性标记该类。`SqlUserDefinedType` 特性具有许多参数，这些参数提供影响 SQL Server 处理该类型的方式的信息。这些参数在表 12-3 中进行介绍。

### 表 12-3：SqlUserDefinedType 特性参数

| 参数 | 值 | 描述 |
|---|---|---|
| Format | Native 或 UserDefined | 标识序列化格式。如果使用 Native（使用 Visual Studio 创建 UDT 时的默认值），则会使用 SQL Server 序列化模型。如果设置为 UserDefined，则还必须实现 `Microsoft.SqlServer.Server.IBinarySerialize`。该接口包含用于读写数据类型的方法。通常，使用 Native 就足够安全，除非你的数据类型需要特殊处理以避免错误保存。例如，如果要存储媒体流，你可能会将其设置为 UserDefined，以避免错误写入媒体流。 |
| IsByteOrdered | Boolean | 如果数据按字节顺序存储，则为 True；如果按其他顺序存储，则为 false。如果为 True，则可以对该类型使用默认比较运算符，并可将其用作主键。比较两个值的能力是判断应如何使用此参数的重要指标。如果可以定义该 UDT 的一个实例大于另一个实例，则 `IsByteOrdered` 可能为 true。如果不能，例如纬度值，则 `IsByteOrdered` 为 false。 |
| IsFixedLength | Boolean | 如果该类型的所有实例大小相同，则应设为 true。如果 UDT 仅包含固定大小的元素（如 int、double 或 char (20)），则为 true。如果包含可变大小的元素（如 varchar (50) 或 text），则应为 false。这是一个标记，用于启用 SQL Server 查询处理器的优化。 |
| ValidationMethodName | String | 用于验证 UDT 中数据的方法的名称。此方法在加载 UDT 时使用，如果数据有效，应返回 true。 |
| MaxByteSize | Integer，最大值为 8000 | 定义 UDT 的最大大小（以字节为单位） |

除了此特性外，每个用户定义类型还需要实现共享方法 `Parse` 和实例方法 `ToString`。这些方法能够在新数据类型与中间格式 `SqlString` 之间进行转换。最后，虽然这不是必需的，但你还应该在结构中实现 `INullable`。此接口要求添加 `IsNull` 属性，该属性使你的 UDT 能够处理 null 值，无论这些值是存储在数据库中还是从客户端传递而来。

> 如果你使用 Visual Studio 创建 UDT，那么最好在开始使用它们之前创建并调试所有 UDT，尤其是如果你需要将它们用于任何表列。这是因为 Visual Basic 在部署项目时会删除你在 SQL Server 项目中创建的所有对象。如果有任何表使用了用户定义类型，你将无法删除该 UDT，因而也就无法部署你所做的更改。如果需要更改，你可能会收到类似“无法删除类型‘Location’，因为它当前正在使用中。”的错误。此错误会导致项目的部署步骤失败。如果发生这种情况，请更改列类型或暂时删除表。然后，你可以根据需要重新部署 UDT。不要忘记改回列类型，或者重新创建表。

虽然你可以使用任何 DLL 编写与 SQL Server 集成的代码，但 Visual Studio 提供了 Visual Basic SQL CLR 数据库项目（参见图 12-19）。此项目类型会生成 DLL，同时将 DLL 连接到数据库。

![](img/d99870e80390742f93963da7be0b2e61_485_0.png)

### 图 12-19

> 只有安装了 Service Pack 1 的累积更新 5，SQL Server 2008 才支持 .NET 4 程序集。

创建新的 SQL Server 项目时，Visual Studio 会提示你标识将承载 DLL 的数据库。此时，你可以选择现有数据库连接，或创建一个新连接。对于示例项目，请创建一个名为 FooStore 的新数据库。Visual Studio 还会询问是否要在该连接上启用 SQL/CLR 调试。通常，你需要在开发服务器上启用此功能，但请记住，调试时服务器仅限于单一连接。创建项目后，你可以通过“项目”菜单添加各种数据库类型。部署项目（通过“生成”菜单中的“部署”选项）会将创建的 DLL 加载到数据库中。你可以通过查看“服务器资源管理器”中的“程序集”文件夹来确认它已加载（参见图 12-20）。

![](img/d99870e80390742f93963da7be0b2e61_486_0.png)

以下代码示例展示了一个用 Visual Basic 编写的简单 `Location` 用户定义类型。此类型用于标识地理位置。在本章的其余部分，我们将使用它来跟踪客户和商店的位置。`Location` 类型有两个主要属性：`Latitude` 和 `Longitude`。可以通过从“项目”菜单中选择“添加用户定义类型”来创建此文件。

```vb
Imports System
Imports System.Data
Imports System.Data.SqlClient
Imports System.Data.SqlTypes
Imports Microsoft.SqlServer.Server
<Serializable()> _
<Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native)> _
Public Structure Location
    Implements INullable
    Public ReadOnly Property IsNull() As Boolean Implements INullable.IsNull
        Get
            If Me.Latitude = Double.NaN OrElse Me.Longitude = Double.NaN Then
                _isNull = True
            Else
                _isNull = False
            End If
            Return _isNull
        End Get
    End Property
    Public Shared ReadOnly Property Null As Location
        Get
            Dim result As Location = New Location
            result._isNull = True
            result.Latitude = Double.NaN
            result.Longitude = Double.NaN
            Return result
        End Get
    End Property
    Public Overrides Function ToString() As String
        Return String.Format("({0}, {1})", Latitude, Longitude)
    End Function
    Public Shared Function Parse(ByVal s As SqlString) As Location
        If s.IsNull Then
            Return Null
        End If
        Dim result As Location = New Location
        Dim temp() As String = s.Value.Split(CChar(","))
        If (temp.Length > 1) Then
            result.Latitude = Double.Parse(temp(0))
            result.Longitude = Double.Parse(temp(1))
        End If
        Return result
    End Function
    Public Function Distance(ByVal loc As Location) As Double
        Dim result As Double
        Dim temp As Double
        Dim deltaLat As Double
        Dim deltaLong As Double
        Const EARTH_RADIUS As Integer = 6378 'kilometers
        Dim lat1 As Double
        Dim lat2 As Double
        Dim long1 As Double
        Dim long2 As Double
        'convert to radians
        lat1 = Me.Latitude * Math.PI / 180
        long1 = Me.Longitude * Math.PI / 180
        lat2 = loc.Latitude * Math.PI / 180
        long2 = loc.Longitude * Math.PI / 180
        'formula from http://mathforum.org/library/drmath/view/51711.html
        deltaLong = long2 - long1
        deltaLat = lat2 - lat1
        temp = (Math.Sin(deltaLat / 2)) ^ 2 + _
            Math.Cos(lat1) * Math.Cos(lat2) * (Math.Sin(deltaLong / 2)) ^ 2
        temp = 2 * Math.Atan2(Math.Sqrt(temp), Math.Sqrt(1 - temp))
        result = EARTH_RADIUS * temp
        Return result
    End Function

    Private _lat As Double
    Private _long As Double
    Private _isNull As Boolean
    Public Property Latitude() As Double
        Get
            Return _lat
        End Get
        Set(ByVal value As Double)
            _lat = value
        End Set
    End Property
    Public Property Longitude() As Double
        Get
            Return _long
        End Get
        Set(ByVal value As Double)
            _long = value
        End Set
    End Property
End Structure
```

代码片段来自 FooStore

除了 `Latitude` 和 `Longitude` 属性之外，`Location` 类型还定义了 `Distance` 方法。该方法用于确定两个位置之间的距离。它使用球面上两点之间距离的计算公式来计算距离。这个公式在“Ask Dr. Math”论坛上有清晰说明（参见 http://mathforum.org/library/drmath/view/51879.html）。由于地球不是一个完美的球体，此计算仅为估算值，但应该足以满足我们的需求。

查看项目的属性；在“属性”的“数据库”选项卡上，确保连接字符串已设置为 FooStore 数据库。目前，请为“权限级别”选择“安全”。在“解决方案资源管理器”中右键单击项目，然后选择“部署”；这将生成项目并将 DLL 复制到数据库。

既然你已经创建了 `Location` 类型，就可以在表定义中使用它了。下面，我们将创建电子商务应用程序的一部分，以演示 `Location` 和其他 SQL Server 功能的使用。
