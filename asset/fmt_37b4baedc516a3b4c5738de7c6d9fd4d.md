
SingleTagHandler 的工作原理与之前的 `NameValueFileHandler` 和 `DictionarySectionHandler` 几乎相同。然而，此对象似乎用于处理包含属性键值对的单个元素。列表 28-49 展示了此处理程序。

## 列表 28-49：对 SingleTagSectionHandler 进行引用

```xml
<configSections>
  <section name="MyCompanyAppSettings"
    type="System.Configuration.SingleTagSectionHandler, System,
    Version=4.0.0, Culture=neutral, PublicToken=b77a5c6193ae0e89"
    restartOnChange="false" />
  </section>
</configSections>
```

完成此项配置设置后，你可以在 `web.config` 文件中创建一个不同的 `MyCompanySettings` section，如列表 28-50 所示。

## 列表 28-50：在 web.config 文件创建自定义键值对节

```xml
<configuration>
  <MyCompanySettings Key1="This is value 1" Key2="This is value 2" />
  <system.web>
    <!-- 为了清晰起见已移除 -->
  </system.web>
</configuration>
```

现在 `web.config` 文件已编写完成，你可以使用 Configuration API 从代码中调用这些项，如列表 28-51 所示。

## 列表 28-51：访问 web.config 中的自定义节

### VB

```vb
Dim ht As Hashtable = New Hashtable()
ht = System.Configuration.ConfigurationManager.GetSection("MyCompanySettings")
Response.Write(ht("Key1") + "<br/>")
Response.Write(ht("Key2"))
```

### C#

```csharp
Hashtable ht = new Hashtable();
ht = ConfigurationManager.GetSection("MyCompanySettings") as Hashtable;
Response.Write(ht["Key1"] + "<br/>");
Response.Write(ht["Key2"]);
```

## 使用你的自定义配置处理器

你也可以创建自己的自定义配置处理器。要实现这一点，你必须先创建一个表示 `web.config` 文件中节的类。在 `App_Code` 文件夹中，创建一个名为 `MyCompanySettings` 的类。列表 28-52 显示了该类。

## 列表 28-52：MyCompanySettings 类

### VB

```vb
Public Class MyCompanySettings
  Inherits ConfigurationSection

  <ConfigurationProperty("Key1", DefaultValue="This is the value of Key 1", IsRequired:=False)>
  Public ReadOnly Property Key1() As String
    Get
      Return Base.Item("Key1").ToString()
    End Get
  End Property

  <ConfigurationProperty("Key2", IsRequired:=True)>
  Public ReadOnly Property Key2() As String
    Get
      Return MyBase.Item("Key2").ToString()
    End Get
  End Property
End Class
```

### C#

```csharp
using System.Configuration;
public class MyCompanySettings : ConfigurationSection
{
    [ConfigurationProperty("Key1", DefaultValue = "This is the value of Key 1", IsRequired = false)]
    public string Key1
    {
        get
        {
            return this["Key1"] as string;
        }
    }

    [ConfigurationProperty("Key2", IsRequired = true)]
    public string Key2
    {
        get
        {
            return this["Key2"] as string;
        }
    }
}
```

你可以看到此类继承自 `ConfigurationSection`，并且使用 `ConfigurationProperty` 特性创建了两个属性。你可以在这里使用一些属性，例如 `DefaultValue`、`IsRequired`、`IsKey` 和 `IsDefaultCollection`。在准备好此类后，你可以配置应用程序使用此处理器，如列表 28-53 所示。

## 列表 28-53：对 MyCompanySettings 对象建立引用

```xml
<configSections>
    <section name="MyCompanySettings" type="MyCompanySettings" />
</configSections>
```

你可以在 `web.config` 文件中使用此节，如列表 28-54 所示。

## 列表 28-54：在 web.config 文件中创建你自己的自定义键值对节

```xml
<configuration>
    <configSections>
        <!-- 为了清晰起见已移除 -->
    </configSections>
    <MyCompanySettings Key2="Here is a value for Key2" />
    <system.web>
        <!-- 为了清晰起见已移除 -->
    </system.web>
</configuration>
```

使用此配置，你可以从代码中程序化访问此键值对，如列表 28-55 所示。

## 列表 28-55：访问 web.config 文件中的自定义节

### VB

```vb
Dim cs As MyCompanySettings = New MyCompanySettings()
cs = ConfigurationManager.GetSection("MyCompanySettings")
Response.Write(cs.Key1 + "<br/>")
Response.Write(cs.Key2)
```

### C#

```csharp
MyCompanySettings cs = ConfigurationManager.GetSection("MyCompanySettings") as MyCompanySettings;
Response.Write(cs.Key1 + "<br/>");
Response.Write(cs.Key2);
```

## 使用配置转换 (Configuration Transforms)

到此时，你应该已经看到 XML 配置系统有多强大。然而，你可能还在考虑有多少设置需要更改，或者在部署时更改配置文件的手动过程。尽管过去除了这些手动过程外还有许多解决方案，但 ASP.NET 团队意识到某些事情需要改变。随着 ASP.NET 4 和 Visual Studio 2010 的推出，引入了 `web.config` 转换。ASP.NET 4.5 继续使用这种行为。转换可以用于任何配置元素或属性，包括本章涵盖的自定义节。

> 注意：转换适用于应用程序，而不是网站。

### 添加 web.config 转换

`web.config` 转换用于 ASP.NET 应用程序。在创建新的 ASP.NET 应用程序后，你会发现 `web.config` 文件是可以展开的，并且将包含 `Debug.config` 和 `Release.config` 文件。这两个文件都是相关配置模式的转换。由于每个 ASP.NET 程序都带有 Debug 和 Release 配置模式，这些文件会自动创建。

在图 28-8 中，你可以看到存在两种配置模式。在解决方案管理器中，你可以看到两个 `web.config` 文件。假设你有一个对应部署到服务器的配置过程。通过在配置管理器中选择“新建”，你可以添加一个名为 Staging 的新配置模式，如图 28-9 所示。添加新配置模式后，该模式将在配置管理器中可用（图 28-10）。

此时，你已经添加了新的配置模式，但尚未添加转换。Visual Studio 2012 有内置方法帮助你添加转换。如果你在解决方案管理器中右键点击 `web.config` 文件，将看到一个“添加转换”的选项（图 28-11）。

添加转换后，你可以在解决方案管理器中看到对应的文件（图 28-12）。

## 更新转换文件

打开其中一个转换文件之一（例如 `web.Staging.config`），你会发现该文件基本上是空的。文件中包含了示例转换以及一个移除 `debug` 属性的活动转换，如列表 28-56 所示。

## 列表 28-56：浏览 web.Staging.config 文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- 有关使用 web.config 转换的更多信息请访问
     http://go.microsoft.com/en-us/fwlink?LinkID=125889 -->
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <!--
  在下面的示例中，“SetAttributes”转换仅当 "Match" 定位器
  找到属性 "name" 值为 "MyDB" 时，才会将 "connectionString" 的值更改为 "ReleaseSqlServer"。
  -->
  <connectionStrings>
    <add name="MyDB"
         connectionString="Data Source=ReleaseSqlServer;Initial Catalog=MyDatabase;Integrated Security=True"
         xdt:transform="SetAttributes" xdt:Locator="Match(name)" />
  </connectionStrings>
  
  <system.web>
    <compilation xdt:transform="RemoveAttributes(debug)" />
    <!--
    在下面的示例中，“Replace”转换将替换 web.config 文件中的整个 <customErrors> 节。
    注意由于 <system.web> 节点下只有一个 customErrors 节，因此不需要使用 xdt:Locator 属性。
    -->
    <customErrors defaultRedirect="GenericError.htm"
                  mode="RemoteOnly" xdt:transform="Replace">
      <error statusCode="500" redirect="InternalError.html" />
    </customErrors>
  </system.web>
</configuration>
```

> 注意：如文件注释中所建议，`web.config` 转换命令的完整列表可以在 http://go.microsoft.com/fwlink/?LinkId=125889 处找到。

编译配置元素包含一个转换（transform）。之所以能够进行转换，是因为在配置根元素中添加了 `XML Document` 命名空间。你会发现 `transform` 属性的值为 `RemoveAttributes(debug)`。`RemoveAttributes` 是将要使用的转换方法。在这种情况下，该方法将从配置元素中删除属性。传递给方法的值是 `debug`。这意味着名为 `debug` 的属性将从配置中删除。

`XML Document Transform` 命名空间有两个属性。第一个 `transform`，在编译配置元素的转换中已经过演示。`transform` 属性可能的方法包括：

- `Insert`：将定义的元素作为所选元素进行插入
- `InsertAfter`：在指定的路径（XPath 表达式）之后插入元素
- `InsertBefore`：在指定的路径（XPath 表达式）之前插入元素
- `Remove`：删除所选的元素
- `RemoveAll`：删除所有所选的元素
- `RemoveAttributes`：删除当前元素的指定属性
- `Replace`：用转换文件中指定的元素替换整个元素
- `SetAttributes`：设置当前元素指定属性的值

第二个属性 `location` 用于选择特定元素。`location` 属性可能的方法包括：

- `Condition`：在当前元素上进行求值的 XPath 表达式，以确定何时发生转换
- `Match`：指定一个或多个具有匹配值的元素
- `XPath`：导航到另一个元素的 XPath 表达式，并求值一个条件以确定是否应该发生转换

使用 `location` 和 `transform` 属性可能是必要的。例如，你在本章的早些时候创建了一个作为 `NameValueFileSectionHandler` 的自定义配置节，命名为 `MyCompanyAppSettings`。当你转换配置文件时，你可能需要替换集合中某一个项的值。例如，将以下内容添加到 `MyCompanyAppSettings` 配置节中：

```xml
<add key="Key2" value="The is 2 in staging"
      xdt:Transform="SetAttributes(value)" xdt:Locator="Match(key)" />
```

使用阶段配置模式发布你的阶段服务器后，你应该注意到你的 `web.config` 文件看起来与列表 28-57 类似。

> 注意：第 3 章详细介绍了各种发布方法。

## 列表 28-57：配置转换的结果

```xml
<?xml version="1.0"?>
<configuration>
  <configSections>
    <section name="MyCompanyAppSettings"
      type="System.Configuration.NameValueFileSectionHandler,System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c61934e089"
      restartOnExternalChanges="false" />
  </configSections>
  <MyCompanyAppSettings>
    <add key="Key1" value="This is value 1" />
    <add key="Key2" value="The is value 2 in staging" />
  </MyCompanyAppSettings>
  <system.web>
    <compilation framework="4.5" />
    <httpRuntime framework="4.5" />
  </system.web>
</configuration>
```

这种做法经常用于在发布部署期间替换特定连接的 `connectionString` 值。

> 注意：使用配置转换时有很多选项，我在本章中无法涵盖。强烈建议你继续在网上搜索更多配置转换示例。你也可以在 MSDN 中搜索 `Web.config Transformation Syntax`。

# 第 28 章 配置

# 打包与最小化

ASP.NET 4.5 包含了一项新功能，可以对 Web 应用程序中的 CSS 和 JavaScript 进行最小化和打包。如果你使用 Visual Studio 2012 中的任何默认项目模板，此功能已开启。

# 什么是打包和最小化？

大多数静态内容（如 CSS 和 JavaScript）包含大量的空白和注释。虽然空白和注释并不一定占用空间，但根据客户端速度，额外的空间会显著降低页面加载速度。图 28-13 显示了最小化之前的网络流量。

![](img/67a6707ff505c05edb96c0128fb309.png)

图 28-13

最小化之前的 JavaScript 示例如下：

```javascript
function HelloWorld(firstName) {
  // 声明变量
  var message = "Hello, " + firstName;

  // 显示消息
  alert(message);
}
```
