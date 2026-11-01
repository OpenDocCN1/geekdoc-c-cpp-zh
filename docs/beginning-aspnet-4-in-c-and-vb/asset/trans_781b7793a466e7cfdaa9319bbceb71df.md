

![](img/d7d2ffa0a76feaab821930e95daace93_1166_0.png)

## 图 38-5

ComboBox 绑定到数据上下文的 EventList 属性，并使用包含两个 TextBlock 元素的 DataTemplate，这两个 TextBlock 元素绑定到项的 Name 和 DateFrom 属性。

```
<ComboBox x:Name="comboEvents"
    ItemsSource="{Binding Path=EventList, Mode=OneWay}"
    Grid.Row="0" Grid.Column="1" Margin="5"
    VerticalAlignment="Center">
    <ComboBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Vertical">
                <TextBlock Text="{Binding Path=Name}" />
                <TextBlock Text="{Binding Path=DateFrom}" />
            </StackPanel>
        </DataTemplate>
    </ComboBox.ItemTemplate>
</ComboBox>
```

代码片段 WCFRegistration/Views/Home.xaml

对于数据输入，该控件使用多个 TextBox 元素，这些元素绑定到由 CurrentAttendee 属性返回的 Attendee 对象的属性。在 WPF 中，默认绑定模式取决于使用它的控件；在 Silverlight 中，默认绑定模式是 OneWay，因此需要改为双向绑定。Button 元素将处理程序方法 OnRegistration() 关联到 Click 事件。

```
<TextBox Grid.Row="1" Grid.Column="1" Margin="5"
    Text="{Binding Path=CurrentAttendee.RegistrationCode,
        Mode=TwoWay}" />
<TextBox Grid.Row="2" Grid.Column="1" Margin="5"
    Text="{Binding Path=CurrentAttendee.Name,
        Mode=TwoWay}" />
<TextBox Grid.Row="3" Grid.Column="1" Margin="5"
    Text="{Binding Path=CurrentAttendee.Email,
        Mode=TwoWay}" />
```

```
<TextBox Grid.Row="4" Grid.Column="1" Margin="5" Text="{Binding Path=CurrentAttendee.Company, Mode=TwoWay}" />
<Button Grid.Row="5" Grid.Column="1" Content="Submit Registration" Margin="5" Click="OnRegistration" />
```

在代码隐藏文件中，Silverlight 页面的 DataContext 设置为 this，以映射 EventList 和 CurrentAttendee 属性。

```csharp
using System.Collections.ObjectModel;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Navigation;
using Wrox.ProcSharp.Silverlight.RegistrationService;

namespace Wrox.ProcSharp.Silverlight
{
    public partial class Home : Page
    {
        public Home()
        {
            CurrentAttendee = new Attendee();
            EventList = new ObservableCollection<Event>();
            InitializeComponent();
            this.DataContext = this;
        }

        public ObservableCollection<Event> EventList { get; private set; }
        public Attendee CurrentAttendee { get; private set; }
    }
}
```

代码片段 WCFRegistration/Views/Home.xaml.cs

通过向 RegistrationService 添加服务引用，代理类仅创建异步方法。该代理类使用异步组件模式。

![](img/d7d2ffa0a76feaab821930e95daace93_1167_0.png)

重写的方法 OnNavigatedTo() 在导航到该页面时被调用。在此处，通过调用 GetEventsAsync() 方法调用 WCF 服务的 GetEvents 操作。异步操作完成时，会触发 GetEventsCompleted 事件。一个 Lambda 表达式被赋值给该事件，以将返回的事件添加到 eventList 集合中。由于 eventList 是 ObservableCollection<T>，用户界面会更新关于此列表的更改。

```csharp
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    var client = new RegistrationServiceClient();
    client.GetEventsCompleted += (sender, el) =>
    {
        if (el.Error != null)
        {
        }
        else
        {
            foreach (var ev in el.Result)
{
    EventList.Add(ev);
}
};
client.GetEventsAsync(DateTime.Today, DateTime.Today.AddMonths(2));
}
```

当“Submit Registration”按钮的 Click 事件被触发时，会调用方法 OnRegistration()。这里再次调用异步方法：RegisterAttendeeAsync() 来注册参加者。该方法完成后，使用 NavigationService.Navigate() 将用户导航到另一个页面。

```csharp
private void OnRegistration(object sender, RoutedEventArgs e)
{
    var client = new RegistrationServiceClient();
    CurrentAttendee.EventID = ((comboEvents.SelectedItem as Event).Id);
    client.RegisterAttendeeCompleted += (sender1, e1) =>
    {
        if (e1.Error == null)
        {
            if (e1.Result)
            {
                NavigationService.Navigate(
                    new Uri("/Success", UriKind.Relative));
            }
            else
            {
                NavigationService.Navigate(
                    new Uri("/ErrorPage", UriKind.Relative));
            }
        }
        else
        {
            // display error
        }
    };
    client.RegisterAttendeeAsync(CurrentAttendee);
}
```

现在可以启动 Silverlight 应用程序来调用 WCF Web 服务。

## 使用 WCF 数据服务

Silverlight 还允许你访问 WCF 数据服务的客户端部分。借助此功能，你可以使用 HTTP 请求从 Silverlight 控件检索和更新数据，而无需手动定义服务方法。检索、更新和添加新数据都可以通过简单的 HTTP 请求完成。

> 第 32 章“数据服务”介绍了 WCF 数据服务。

要为 Silverlight 应用程序提供使用 WCF 数据服务的服务，需要在 Web 项目中添加一个名为 EventRegistrationDataService 的新 WCF 数据服务项。该实现派生自 DataService<EventRegistrationEntities>。基类 DataService<T> 的泛型参数是由 ADO.NET 实体框架模板创建的实体数据上下文。通过 config.SetEntitySetAccessRule() 定义访问规则，允许对 Events 实体集和 Attendees 实体集进行读取或全部访问。

```csharp
using System.Collections.Generic;
using System.Data.Services;
using System.Data.Services.Common;
using System.Linq;
using System.Data.Model.Web;

namespace Wrox.ProcSharp.Silverlight.Web
{
    public class EventRegistrationDataService : DataService<EventRegistrationEntities>
    {
        public static void InitializeService(DataServiceConfiguration config)
        {
            config.SetEntitySetAccessRule("Events", EntitySetRights.AllRead);
            config.SetEntitySetAccessRule("Attendees", EntitySetRights.All);
            config.SetServiceOperationAccessRule("AddAttendee", ServiceOperationRights.All);
            config.DataServiceBehavior.MaxProtocolVersion = DataServiceProtocolVersion.V2;
        }
    }
}
```

代码片段 SilverlightDemos.Web/EventRegistrationDataService.svc.cs

要使用 WCF 数据服务提供比仅添加新记录更复杂的参加者注册操作，需要将方法 AddAttendee() 添加到 EventRegistrationDataService 类中。WebGet 特性指定该方法可以通过 HTTP GET 请求进行访问。对于 POST、PUT 或 DELETE 请求，可以使用 WebInvoke 特性。在 InitializeService() 方法中，通过 SetServiceOperationAccessRule() 方法授予对该操作的访问权限。AddAttendee() 使用单独的参数接收参加者信息，并在将参加者写入从实体数据模型映射的 Attendees 表之前，首先验证 registrationCode 是否存在。使用此方法时必须采用单独参数而不是 Attendee 对象，这样才能通过 HTTP GET 请求调用该方法。

```csharp
[WebGet]
public bool AddAttendee(string name, string email, string company,
    string registrationCode, int eventId)
{
    if ((from rc in this.CurrentDataSource.RegistrationCodes
         where rc.RegistrationCode == registrationCode
         select rc).Count() < 1)
    {
        return false;
    }
    else
    {
        var attendee = new Attendee {
            Name = name,
            Email = email,
            Company = company,
            RegistrationCode = registrationCode,
            EventId = eventId
        };
        this.CurrentDataSource.Attendees.AddObject(attendee);
        return !(this.CurrentDataSource.SaveChanges() < 1);
    }
}
```

向 Silverlight 控件项目 EventRegistration 添加服务引用后，就可以使用 WCF 数据服务客户端类来访问该服务。现在，方法 OnNavigatedTo() 已改为使用从数据服务客户端生成的代理，而不是之前使用的纯 WCF 代理。

