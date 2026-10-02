
```csharp
using System;
using System.Web.Profile;
using System.Web.Security;

namespace Wrox
{
    public class UserProfile : ProfileBase
    {
        public static UserProfile GetProfile(string username)
        {
            return (UserProfile)Create(username);
        }

        public static UserProfile GetProfile()
        {
            return (UserProfile)Create(Membership.GetUser().Name);
        }

        [SettingsAllowAnonymous(false)]
        public string FirstName
        {
            get { return (string)GetPropertyValue("FirstName"); }
            set { SetPropertyValue("FirstName", value); }
        }

        [SettingsAllowAnonymous(false)]
        public string LastName
        {
            get { return (string)GetPropertyValue("LastName"); }
            set { SetPropertyValue("LastName", value); }
        }

        [SettingsAllowAnonymous(true)]
        public DateTime LastVisited
        {
            get { return (DateTime)GetPropertyValue("LastVisited"); }
            set { SetPropertyValue("LastVisited", value); }
        }
    }
}
```

## 列表 18-22 (续)

```csharp
public class UserProfile : ProfileBase
{
    public static UserProfile GetUserProfile(string username)
    {
        return Create(username) as UserProfile;
    }

    public static UserProfile GetUserProfile()
    {
        return Create(Membership.GetUser().UserName) as UserProfile;
    }

    [SettingsAllowAnonymous(false)]
    public string FirstName
    {
        get { return base["FirstName"] as string; }
        set { base["FirstName"] = value; }
    }

    [SettingsAllowAnonymous(false)]
    public string LastName
    {
        get { return base["LastName"] as string; }
        set { base["LastName"] = value; }
    }

    [SettingsAllowAnonymous(true)]
    public DateTime LastVisited
    {
        get { return base["LastVisited"] as DateTime; }
        set { base["LastVisited"] = value; }
    }
}
```

然后，你需要在 `web.config` 中确保配置配置属性来自你刚刚创建的类。列表 18-23 显示了如何实现这一点。

## 列表 18-23：在 web.config 中引用配置类

```xml
<profile defaultProvider="AspNetSqlProfileProvider" inherits="Wrox.UserProfile" />
```

最后，列表 18-19 显示的 API 提供了对配置属性的访问。

# 个性化提供程序

如本章前面的图 18-1 所示，个性化模型的中间层（个性化 API 层）与系列默认数据提供程序通信。默认情况下，个性化模型使用 Microsoft SQL Server 版文件来存储你定义的个性化属性。然而，你并不限于这种数据存储。你还可以使用 Microsoft SQL Server 数据提供程序来处理 Microsoft SQL Server 7.0 或更高版本。除了 Microsoft SQL Server 数据提供程序，如果这些数据存储无法满足你的需求，该架构还允许你创建自己的提供程序。

## 使用 SQL Server Express 版

Microsoft SQL Server 数据提供程序允许你处理 SQL Server Express 版文件。SQL Server 提供程序是 ASP.NET 个性化系统使用的默认提供程序。当配合 Visual Studio 2012 使用时，IDE 会将 `ASPNETDB.MDF` 文件放置在应用程序的 `App_Data` 文件夹中。

当你查看 `machine.config` 文件时，请注意个性化引擎如何与此数据库交互的部分。在第一次引用 `LocalSqlServer` 文件处，你会在文件的 `<connectionStrings>` 字符串中找到指向该文件的连接字符串（如列表 18-24 所示）。

## 列表 18-24：为 SQL Server Express 文件添加连接字符串

```xml
<configuration>
  <connectionStrings>
    <clear />
    <add name="LocalSqlServer"
      connectionString="data source=.\SQLEXPRESS;Integrated Security=SSPI;"
      AttachDbFilename="Filename=|DataDirectory|appdb.mdf;User Instance=true"
      providerName="System.Data.SqlClient" />
  </connectionStrings>
</configuration>
```

在此示例中，你使用了 `LocalSqlServer` 文件的连接字符串。通过 `connectionString` 属性指定的文件位置是该文件的相对路径。这意味着在每个利用个性化功能的应用程序中，默认的 SQL Server 提供程序都应该位于应用程序的 `App_Data` 文件夹中，并命名为 `ASPNETDB.MDF`。

SQL Server Express 文件的连接字符串通过此 `<connectionStrings>` 部分中的 `LocalSqlServer` 进行指定。你可以在 `machine.config` 文件的 `<profile>` 部分看到个性化引擎对它的引用。`<profile>` 部分包含一个列出个性化引擎可用提供程序的子部分，如列表 18-25 所示。

## 列表 18-25：添加新的 SQL Server 数据提供程序

```xml
<configuration>
  <system.web>
    <profile>
      <providers>
        <add name="AspNetSqlProviders"
          connectionStringName="LocalSqlServer" applicationName="*"
          type="System.Web.Profile.SqlProfileProvider,System.Web,Version=4.0.0.0;Culture=neutral;PublicKeyToken=b03f577f11d5e0a3" />
      </providers>
    </profile>
  </system.web>
</configuration>
```

由此你可以看到通过使用 `<add>` 元素添加提供程序。该元素的 `connectionStringName` 属性指向了列表 18-24 中 `<connectionStrings>` 属性中所声明的内容。

你可以指定一个与 `machine.config` 文件指定的完全不同的 SQL Server Express 文件。创建一个指向新的 `ASPNETDB` 文件模板版本的 SQL Server Express 文件的连接字符串。此时，你使用 `<connectionStrings>` 指向此新文件。如果你更改了 `machine.config` 文件中的值，服务器上的所有 ASP.NET 应用程序将使用此指定的文件。如果你只对 `web.config` 文件进行更改，只有使用此特定 `web.config` 文件的应用程序将使用此新的数据存储。服务器上的应用程序保持不变。

## 使用 Microsoft SQL Server

你可能会发现使用 SQL Server Express 文件处理个性化框架非常简单。但当你处理需要性能和可靠性因素的大型应用程序时，你应该使用从 SQL 开始的 SQL Server 配合 SQL Server 个性化提供程序。

```xml
<profile>
  <add name="AsNetSql2012ProfileProvider"
    connectionStringName="LocalSql2012Server" applicationName=""
    type="Web.Profile.SqlProfileProvider, System.Web,
    Version=4.0.0.0, Culture=neutral,
    PublicKeyToken=b03f57ff51ffd0a33" />
  <properties>
    <add name="FirstName" />
    <add name="LastName" />
    <add name="LastVisited" />
    <add name="Age" />
    <add name="Member" />
  </properties>
</profile>
```

你对此配置定义的主要更改是使用 `defaultProvider` 属性，其值为你想要使用的提供程序名称——在本例中，为新创建的 SQL Server 提供程序 `AsNetSql2012ProfileProvider`。你也可以通过更改 `machine.config` 文件中的 `<profile>` 元素来实现此更改，如列表 18-27 所示。

### 列表 18-27：在 machine.config 中使用 SQL Server 作为提供程序

```xml
<configuration>
  <system.web>
    <profile enabled="true" defaultProvider="AsNetSql2012ProfileProvider">
    </profile>
  </system.web>
</configuration>
```

此更改将强制位于此服务器上的每个应用程序使用此新的 SQL Server 提供程序，而不是默认的 SQL Server 提供程序（除非在应用程序的 `web.config` 中进行了覆盖）。

### 使用多个提供程序

你不限于使用单个数据存储库或提供程序。相反，你可以使用任意数量的提供程序。你甚至可以为定义的每个属性指定个性化提供程序。这意味着你可以对大多数属性使用默认提供程序，同时允许其中一些使用完全不同的提供程序（见列表 18-28）。

### 列表 18-28：使用不同的提供程序

```xml
<configuration>
  <system.web>
    <profile defaultProvider="AspNetProvider">
      <properties>
        <add name="FirstName" />
        <add name="LastName" />
        <add name="LastVisited" />
        <add name="Age" />
        <add name="Member" provider="AsNetSql2012ProfileProvider" />
      </properties>
    </profile>
  </system.web>
</configuration>
```

从此示例可以看出，指定了一个默认提供程序——`AspNetProvider`。除非指定了另一个提供程序，否则将使用此提供程序。更改此设置的唯一属性是 `Member`。`Member` 本身使用了完全不同的个性化提供程序。通过使用 `<add>` 元素，你可以为定义的每个属性定义特定的提供程序。

### 使用通用提供程序

ASP.NET 4.5 配置功能与 SQL Server 绑定。要使用新的程序集，你仍然需要通过 `web.config` 配置 ASP.NET。技巧是让 ASP.NET 获取数据并与任何支持的数据库协作。目前支持的数据库列表重点关注微软的 Azure 产品，但以后可能会添加数据库。列表 18-29 显示了一个示例配置。

### 列表 18-29：在 web.config 中使用通用提供程序

```xml
<configuration>
  <connectionStrings>
    <add connectionString="..." name="DefaultConnection" />
  </connectionStrings>
  <system.web>
    <profile defaultProvider="DefaultProfileProvider">
      <providers>
        <add name="DefaultProfileProvider" type="System.Web.Providers.DefaultProfileProvider" connectionStringName="DefaultConnection" applicationName="/" />
      </providers>
    </profile>
  </system.web>
</configuration>
```

## 管理应用程序配置

当你将使用配置信息的 ASP.NET 应用程序投入生产时，你会很快发现你需要一种方法来管理应用程序生命周期内收集的所有配置信息。当你查看 ASP.NET MMC 嵌入程序或 ASP.NET 站点管理工具时，请注意这些工具都没有提供删除特定用户配置信息的方法，甚至无法清理数据库中长时间未活跃用户的配置信息。

ASP.NET 4.5 让你能够通过 .NET 中提供的 `ProfileManager` 类来管理应用程序存储的配置信息。你可以使用 `ProfileManager` 类来构建管理功能，以完全管理应用程序存储的配置信息。除了可以访问属性值（例如个性化系统正在使用的提供程序名称或相关应用程序的名称）外，`ProfileManager` 类中还提供了大量方法，用于检索有关用户配置的各种信息。通过 `ProfileManager` 类，你还有能力对这些存储的配置信息执行操作，包括清理数据库中旧的配置信息。

### ProfileManager 类属性

表 18-1 详细列出了 `ProfileManager` 类的属性。

| 属性 | 说明 |
| :--- | :--- |
| `ApplicationName` | 获取或设置要操作的应用程序名称 |
| `AutomaticSaveEnabled` | 获取或设置布尔值，指示是否在页面执行结束时存储配置信息 |
| `Enabled` | 获取或设置布尔值，指示应用程序是否可以使用个性化系统 |
| `Provider` | 获取用于个性化系统的提供程序名称 |
| `Providers` | 获取适用于 ASP.NET 应用程序的所有可用提供程序的集合 |

你可以看到，这些属性包含了有关个性化系统以及该系统可用提供程序的一些信息，你可以将它们集成到你构建的任何管理系统中。接下来，本章将介绍 `ProfileManager` 类的可用方法。

### ProfileManager 类方法

`ProfileManager` 类提供了许多可用方法，可以帮助你管理应用程序用户的配置。表 18-2 描述了这些方法。

| 方法 | 说明 |
| :--- | :--- |
| `DeleteInactiveProfiles` | 允许你删除在指定时间内没有任何活动的任何配置 |
| `DeleteProfile` | 允许你删除特定的配置 |
| `DeleteProfiles` | 允许你删除一组配置 |
| `FindInactiveProfilesByUserName` | 根据指定的日期，为你提供特定用户名下的所有非活跃配置 |
| `FindProfilesByUserName` | 为你提供特定用户名的所有配置 |
| `GetInactiveProfiles` | 为你提供自指定日期以来未活跃的所有配置 |
| `GetAllProfiles` | 为你提供所有配置的集合 |
