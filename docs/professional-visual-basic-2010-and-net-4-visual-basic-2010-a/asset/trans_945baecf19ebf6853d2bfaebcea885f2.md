

在你签署并构建程序集之后，下一步是根据程序集的签名在数据库中创建一个密钥，并创建一个将与该密钥关联的用户。这是通过 T-SQL 查询完成的。在 SQL Management Studio 中运行以下查询（根据你的机器情况更新 DLL 的路径）：

```
USE master
GO
CREATE ASYMMETRIC KEY FooStoreKey
FROM EXECUTABLE FILE = 'C:\FooStore.dll'
GO
CREATE LOGIN FooUser
FROM ASYMMETRIC KEY FooStoreKey
GRANT EXTERNAL ACCESS ASSEMBLY TO FooUser
GO
```

创建新的非对称密钥必须在 master 数据库中进行。FROM EXECUTABLE FILE 子句中列出的 DLL 应该是你在 Visual Basic 中刚刚创建的 DLL；将 SQL 语句中的路径调整为与你的 DLL 位置相匹配。一旦密钥创建完成，你就可以基于此密钥创建一个新的登录名，并为该用户提供外部访问权限。你还应该将该登录名添加到数据库中并授予其访问所需对象的权限。

现在程序集能够访问外部站点，我们就可以开始编写将地址转换为经纬度（即对地址进行地理编码）的函数了。几家公司出售提供此功能的数据库或服务。然而，Yahoo! 提供了一个免费的 Web 服务来进行地理编码。它每天可以调用多达 5,000 次，对于本示例来说绰绰有余（但对于真正的商店来说可能不够）。

Geocode 服务是通过向 http://api.local.yahoo.com/MapsService/V1/geocode 发送 GET 请求来访问的，其参数如表 12-6 所示。

### TABLE 12-6: Parameters for Accessing the Geocode Service

| PARAMETER | DESCRIPTION |
|-----------|-------------|
| appid | （必需）用于标识使用该服务的每个应用程序的唯一字符串。请注意，此参数名称区分大小写。为测试目的，你可以使用 YahooDemo（Yahoo 示例本身使用）。然而，你自己的应用程序应具有唯一的应用程序 ID。你可以在 http://api.search.yahoo.com/webservices/register_application 上注册它们 |
| street | （可选）你要搜索的街道地址。这应进行 URL 编码。即，空格应替换为 + 字符，高 ASCII 或 <、/、> 等字符应替换为其等效的 "%##" 记法。 |
| city | （可选）你要搜索的位置的城市。这应进行 URL 编码，尽管这仅在城市名称包含空格或高 ASCII 字符时才真正必要。 |
| state | （可选）你要搜索的美国州（如果适用）。使用两位字母缩写或全名（URL 编码）均可。 |
| zip | （可选）你要搜索的美国邮政编码（如果适用）。可以是 5 位或 5+4 位格式。 |
| location | （可选）包含 URL 编码且以逗号分隔的地址信息的自由格式字段。这提供了一种更简便的查询方法，而无需设置上面列出的各个值。例如：location=1600+Pennsylvania+Avenue+NW,+Washington,+DC |

以下代码显示了 fnGetLocation 函数的完整源代码：

```
Imports System
Imports System.Data
Imports System.Data.SqlClient
Imports System.Data.SqlTypes
Imports Microsoft.SqlServer.Server
Imports System.Xml
Imports System.Text
Partial Public Class UserDefinedFunctions
    'Replace YahooDemo with your key
    Private Const YAHOO_APP_KEY As String = "YahooDemo"
    Private Const BASE_URL As String = _
    "http://api.local.yahoo.com/MapsService/V1/geocode"
    <Microsoft.SqlServer.Server.SqlFunction()> _
    Public Shared Function fnGetLocation(ByVal street As SqlString, _
    ByVal city As SqlString, _
    ByVal state As SqlString, _
    ByVal zip As SqlString) As Location
    Dim result As New Location
    Dim query As New StringBuilder
    'uses Yahoo geocoder to geocode the location
    'limited to 5000 calls/day
    'construct URL
    ' URL should look like:
    '     http://api.local.yahoo.com/MapsService/V1/geocode?
    '     appid=YahooDemo&street=701+First+Street&city=Sunnyvale&state=CA

    query.AppendFormat("{0}?appid={1}", BASE_URL, YAHOO_APP_KEY)
    If Not street.IsNull Then
        query.AppendFormat("&street={0}", street)
    End If
    If Not city.IsNull Then
        query.AppendFormat("&city={0}", city)
    End If
    If Not state.IsNull Then
        query.AppendFormat("&state={0}", state)
    End If
    If Not zip.IsNull Then
        query.AppendFormat("&zip={0}", zip)
    End If
    'Debug.Print(query.ToString())
    'send request
    Using r As XmlReader = XmlReader.Create(query.ToString())
        'parse output
        While r.Read
            If r.IsStartElement("Latitude") Then
                ' longitude directly follows latitude in the result xml
                result.Latitude = Double.Parse(r.ReadElementString)
                result.Longitude = Double.Parse(r.ReadElementString)
                Exit While
            End If
        End While
    End Using
    Return result
    End Function
End Class
```

前述示例中的大部分代码用于创建适当的 URL 来创建查询。查询应如下所示：

```
http://api.local.yahoo.com/MapsService/V1/geocode?appid=YahooDemo&street=701+First+Street&city=Sunnyvale&state=CA&country=USA
```

虽然 YahooDemo appid 可用于测试，但它有时可能无法工作。查询每个 appid 限制为 5,000 次请求，因此如果一天内有几个人调用地理编码器，请求将失败。因此，你应该为测试申请自己的 appid，并用你自己的 appid 替换前面的 appid，你可以在以下网页上获得：

```
http://api.search.yahoo.com/webservices/register_application
```

> 请注意，前述代码使用 StringBuilder 来构造查询。为什么不简单地连接字符串来创建查询呢？原因有几个，但最重要的是性能。因为 Visual Basic 中的字符串是不可变的，连接需要每次都创建新的字符串。例如，简单的表达式 Dim s As String = "Hello" & "world" 实际上需要三个字符串，其中两个会立即被丢弃。StringBuilder 类正是为避免这种重复的创建和释放对象而构建的，其 resulting 代码比简单连接的性能好得多。

一旦查询构造完成，就会使用 XmlReader 来执行查询。对 Yahoo! 地理编码器的调用返回的 XML 如下所示：

```
<?xml version="1.0" ?>
<ResultSet xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="urn:yahoo:maps" xsi:schemaLocation="urn:yahoo:maps http://api.local.yahoo.com/MapsService/V1/GeocodeResponse.xsd">
<Result precision="address" warning="The exact location could not be found, here is the closest match: 701 First Ave, Sunnyvale, CA 94089">
<Latitude>37.416384</Latitude>
<Longitude>-122.024853</Longitude>
<Address>701 FIRST AVE</Address>
<City>SUNNYVALE</City>
<State>CA</State>
<Zip>94089-1019</Zip>
<Country>US</Country>
</Result>
</ResultSet>
```

虽然你可以将所有内容加载到 XmlDocument 中进行处理，但 XmlReader 通常更快。此外，因为真正需要的只是经度和纬度这两个值，使用 XmlReader 使代码能够快速提取这两个值，而无需加载其他数据的开销。由于 XmlReader 类实现了 IDisposable，你应确保正确处理和释放该类，可以在 Try ... Finally 块中将对象设为 nothing，或使用 Using 语句：

```
Using r As XmlReader = XmlReader.Create(query.ToString())
    'parse output
    While r.Read
        If r.IsStartElement("Latitude") Then
            ' longitude directly follows latitude in the result xml
            result.Latitude = Double.Parse(r.ReadElementString)
            result.Longitude = Double.Parse(r.ReadElementString)
            Exit While
        End If
    End While
End Using
```

