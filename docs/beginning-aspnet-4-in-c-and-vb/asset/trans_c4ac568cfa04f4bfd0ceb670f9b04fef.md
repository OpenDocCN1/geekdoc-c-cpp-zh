
现在，使用 Data Service 模板并创建 RestaurantDataService.svc。.svc 文件包含 ASP.NET ServiceHost 指令，并使用 DataServiceHostFactory 在请求时实例化数据服务。

```
<%@ ServiceHost Language="C#" Factory="System.Data.Services.DataServiceHostFactory,
System.Data.Services, Version=4.0.0.0, Culture=neutral,
PublicKeyToken=b77a5c561934e089"
Service="Wrox.ProCSharp.DataServices.RestaurantDataService" %>
```

代码片段 RestaurantDataServiceWeb/RestaurantDataService.svc

在代码隐藏中，你需要将 DataService<T> 类的模板参数更改为引用之前创建的实体数据服务上下文类，并更改实体集访问规则和服务操作访问规则以允许访问：

```
using System.Data.Services;
using System.Data.Services.Common;

namespace Wrox.ProCSharp.DataServices
{
    public class RestaurantDataService : DataService<RestaurantEntities>
    {
        // This method is called only once to initialize service-wide policies.
        public static void InitializeService(DataServiceConfiguration config)
        {
            config.SetEntitySetAccessRule("Menus", EntitySetRights.All);
            config.SetEntitySetAccessRule("Categories", EntitySetRights.All);
            config.DataServiceBehavior.MaxProtocolVersion = DataServiceProtocolVersion.V2;
        }
    }
}
```

代码片段 RestaurantDataServiceWeb/RestaurantDataService.svc.cs

现在，你可以使用 Web 浏览器像以前一样向此数据服务发出查询；例如，你可以使用 http://localhost:13617/RestaurantDataService.svc/Menus 来接收数据库中所有菜单的 AtomPub。接下来，你创建一个使用 Data Services 客户端部分的应用。

![](img/d7d2ffa0a76feaab821930e95daace93_956_0.png)

## 使用 System.Data.Service.Client 的 .NET 应用程序

本章前面，你已阅读如何创建一个 .NET 客户端应用程序，该应用程序仅使用 HttpWebRequest 类发送 HTTP 请求。Data Services 的客户端部分，命名空间为 System.Data.Services.Client，为客户端构建 HTTP 请求提供了功能。该命名空间的两个最重要的类是 DataServiceContext 和 DataServiceQuery<TEntity>。DataServiceContext 表示在客户端管理的状态。此状态跟踪从服务器加载的对象以及在客户端所做的所有更改。DataServiceQuery<TEntity> 表示对数据服务的 HTTP 查询。

用于引用数据服务的应用程序配置文件的内容如下所示：

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="Wrox.ProCSharp.DataServices.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </sectionGroup>
  </configSections>
  <applicationSettings>
    <Wrox.ProCSharp.DataServices.Properties.Settings>
      <setting name="RestaurantServiceURL" serializeAs="String">
        <value>http://localhost:13617/RestaurantDataService.svc</value>
      </setting>
    </Wrox.ProCSharp.DataServices.Properties.Settings>
  </applicationSettings>
</configuration>
```

*代码片段 ClientApp/app.config*

使用 SendingRequest 事件，数据服务上下文在每次向服务发送请求时都会调用处理程序。方法 data_sendingRequest() 与 SendingRequest 事件关联，并在 SendingRequestEventArgs 参数中接收有关请求的信息。使用 SendingRequestEventArgs，你可以访问请求和标头信息。从 Method 和 RequestUri 属性检索到的请求方法和 URI 会写入 UI 中的 textStatus 控件。

```
void data_SendingRequest(object sender, SendingRequestEventArgs e)
{
    var sb = new StringBuilder();
    sb.AppendFormat("Method: {0}\n", e.Request.Method);
    sb.AppendFormat("Uri: {0}\n", e.Request.RequestUri.ToString());
    this.textStatus.Text = sb.ToString();
}
```

*代码片段 ClientApp/MainWindow.xaml.cs*

数据服务上下文 RestaurantEntities 允许你从服务检索实体；跟踪已检索的实体；允许你在数据上下文中添加、删除和更改实体；并保留更改的状态以发送更新请求。

## LINQ 查询

数据服务上下文实现了一个 LINQ 提供程序，用于将 LINQ 请求转换为 HTTP 请求。MainWindow 类的 Categories 属性使用数据上下文定义了一个 LINQ 查询，以返回所有类别：

```
public IEnumerable<R.Category> Categories
{
    get
    {
        return from c in data.Categories
               orderby c.Name
               select c;
    }
}
```

*代码片段 ClientApp/MainWindow.xaml.cs*

要创建 DataServiceCollection<T> 实例，类 DataServiceCollection 定义了静态方法 Create() 和 CreateTracked()。Create() 创建一个与数据服务上下文无关的列表。CreateTracked() 跟踪从数据服务上下文返回的对象，以便你可以通过发送更改到服务来保存对象。

Menus 属性调用 DataServiceCollection.CreateTracked<R.Menu>() 方法来填充名为 trackedMenus 的 DataServiceCollection<R.Menu> 列表并返回该列表。由 LINQ 查询定义的检索到的实体与数据服务上下文 data 关联。

```
public IEnumerable<R.Menu> Menus
{
    get
    {
        if (trackedMenus == null)
            trackedMenus = DataServiceCollection.CreateTracked<R.Menu>(
                data,
                from m in data.Menus
                where m.CategoryId == ((comboCategories.SelectedItem as R.Category).Id)
                && m.Active
                select m);
        return trackedMenus;
    }
}
```

代码片段 ClientApp/MainWindow.xaml.cs

XAML 代码中的 DataGrid 使用 Binding 标记扩展映射到 Menus 属性：

```
<DataGrid Grid.Row="2" ItemsSource="{Binding Path=Menus}" AutoGenerateColumns="False">
  <DataGrid.Columns>
    <DataGridTextColumn Binding="{Binding Path=Name}" />
    <DataGridTextColumn Binding="{Binding Path=Description}" />
    <DataGridTextColumn Binding="{Binding Path=Price}" />
    <DataGridTextColumn Binding="{Binding Path=CategoryId}" />
  </DataGrid.Columns>
</DataGrid>
```

代码片段 ClientApp/MainWindow.xaml

使用 ComboBox 的 SelectionChanged 事件选择新类别，在处理程序方法 OnCategorySelection() 中，使用新选择的类别再次检索菜单：

```
private void OnCategorySelection(object sender, SelectionChangedEventArgs e)
{
    var selectedCategory = comboCategories.SelectedItem as R.Category;
    if (selectedCategory != null && trackedMenus != null)
    {
        trackedMenus.Clear();
        trackedMenus.Load(from m in data.Menus
                          where m.CategoryId == selectedCategory.Id
                          select m);
    }
}
```

代码片段 ClientApp/MainWindow.xaml.cs

有关可观察集合和类 ObservableCollection<T> 的更多信息，请参阅第 10 章，“Collections。”

## 对象跟踪

数据服务上下文跟踪所有已检索的对象。你可以通过迭代 Entities 属性的返回值来获取有关对象的的信息。Entities 返回一个 EntityDescriptor 对象的只读集合。EntityDescriptor 包含可通过 Entity 属性访问的实体本身，以及状态信息。类型为 EntityStates 的状态是一个枚举，可能的值为 Added、Deleted、Detached、Modified 和 Unchanged。此信息用于跟踪更改并向服务发送更改请求。

为了获取与数据上下文关联的当前实体信息，处理程序方法 OnShowEntities() 与 Show Entities 按钮的 Click 事件关联。在这里，State、Identity 和 Entity 属性用于将状态信息写入 UI。

```
private void OnShowEntities(object sender, RoutedEventArgs e)
{
    var sb = new StringBuilder();
    foreach (var entity in data.Entities)
    {
        sb.AppendFormat("state = {0}, Uri = {1}, Element = {2}\n", entity.State, entity.Identity, entity.Entity);
    }
    this.textStatus.Text = sb.ToString();
}
```

代码片段 ClientApp/MainWindow.xaml.cs

图 32-6 显示了正在运行的应用，其中包含有关跟踪对象的的信息。

![](img/d7d2ffa0a76feaab821930e95daace93_961_0.png)

图 32-6

## 添加、修改和删除实体

要向数据服务上下文添加新实体，从而稍后将新对象发送到数据服务，你可以使用 AddObject() 方法，或强类型变体，如 AddToMenu() 和 AddToCategories()。你只需填写必需的属性；否则，保存状态将不成功。添加新对象会将状态设置为 Added。数据服务上下文的 DeleteObject() 方法将对象的状态设置为 Deleted。如果对象的属性被修改，状态会从 Unchanged 更改为 Modified。现在你可以调用 SaveChanges() 方法，该方法发送 HTTP MERGE 请求来更新实体，发送 HTTP DELETE 请求来删除实体，并发送 HTTP POST 请求来添加新实体。

