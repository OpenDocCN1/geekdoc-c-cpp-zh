
最后，需要显示用于共享的用户界面。这使用户能够选择目标应用：

```
public void ShowShareUI()
{
    DataTransferManager.ShowShareUI();
}
```

图33.3展示了调用DataTransferManager的ShowShareUI方法后的用户界面。根据所提供的数据格式以及已安装的应用，会显示相应的应用供用户选择。

![](img/3d365b72b289213a91ade7eb366b8f35_1255_0.png)

## 图33.3

如果选择邮件应用，则会传递HTML信息。图33.4显示了该应用内接收到的数据。

| 标题 | 发布者 |
|-------|-----------|
| Professional C# 6 and .NET 5 Core Wrox Press | |
| Professional C# 5.0 and .NET 4.5.1 Wrox Press | |

> 注意 使用Windows 8时，用户可以通过超级按钮栏从应用启动数据共享。此时，如果数据不可共享，务必向用户说明需要进行哪些操作才能共享——例如，先选择某项或输入一些数据。此类错误信息可通过在DataRequestedEventArgs类型的Request属性上调用FailWithDisplayText方法来返回。使用Windows 10时，需要显式提供一个可见控件（例如按钮），用户可通过该控件启动共享。如果没有数据可供共享，则不要提供该可见控件。

## 共享目标

现在来看共享的接收方。如果应用要从共享源接收信息，则必须将其声明为共享目标。图33.5显示了Visual Studio中清单设计器的“声明”页面，可以在其中定义共享目标。在此处添加“共享目标”声明，该声明必须至少包含一种数据格式。可能的数据格式有Text、URI、Bitmap、HTML、StorageItems或RTF。还可以通过添加相应的文件扩展名来指定应支持的文件类型。

![](img/3d365b72b289213a91ade7eb366b8f35_1257_0.png)

## 图33.5

包清单中的信息在应用注册时使用。这会告知Windows哪些应用可用作共享目标。示例应用`SharingTarget`定义了`Text`和`HTML`的共享目标。

当用户将应用作为共享目标启动时，会调用`App`类中的`OnShareTargetActivated`方法，而不是`OnLaunched`方法。此时，会创建另一个页面（`ShareTargetPage`），当用户选择此应用作为共享目标时，该页面会显示屏幕（代码文件`SharingTarget/App.xaml.cs`）：

```
protected override void
OnShareTargetActivated(ShareTargetActivatedEventArgs args)
{
    Frame rootFrame = CreateRootFrame();
    rootFrame.Navigate(typeof(ShareTargetPage),
    args.ShareOperation);
    Window.Current.Activate();
}
```

为了避免在两个不同位置创建根框架，`OnLaunched`方法已重构，将框架创建代码放入单独的方法`CreateRootFrame`中。现在，`OnShareTargetActivated`和`OnLaunched`都会调用此方法：

```
private Frame CreateRootFrame()
{
    Frame rootFrame = Window.Current.Content as Frame;
    if (rootFrame == null)
    {
        rootFrame = new Frame();
        rootFrame.NavigationFailed += OnNavigationFailed;
        Window.Current.Content = rootFrame;
    }
    return rootFrame;
}
```

此处展示了OnLaunched方法的改动。与OnShareTargetActivated相反，此方法导航到MainPage：

```
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    Frame rootFrame = CreateRootFrame();
    if (rootFrame.Content == null)
    {
        rootFrame.Navigate(typeof(MainPage), e.Arguments);
    }
    Window.Current.Activate();
}
```

ShareTargetPage包含一些控件，用户可以在其中查看共享数据的信息（如标题和描述），以及一个组合框，用于显示用户可选择的数据格式（代码文件SharingTarget/ShareTargetPage.xaml）：

```
<StackPanel Orientation="Vertical">
<TextBlock Text="Share Target Page" />
<TextBox Header="Title" IsReadOnly="True"
Text="{x:Bind ViewModel.Title, Mode=OneWay}" Margin="12" />
<TextBox Header="Description" IsReadOnly="True" Text="{x:Bind ViewModel.Description, Mode=OneWay}" Margin="12" />
<ComboBox ItemsSource="{x:Bind ViewModel.ShareFormats, Mode=OneTime}"
SelectedItem="{x:Bind ViewModel.SelectedFormat, Mode=TwoWay}" Margin="12" />
<Button Content="Retrieve Data"
Click="{x:Bind ViewModel.RetrieveData, Mode=OneTime}" Margin="12" />
<Button Content="Report Complete"
Click="{x:Bind ViewModel.ReportCompleted, Mode=OneTime}" Margin="12" />
<TextBox Header="Text" IsReadOnly="True" Text="{x:Bind ViewModel.Text, Mode=OneWay}" Margin="12" />
<TextBox AcceptsReturn="True" IsReadOnly="True"
Text="{x:Bind ViewModel.Html, Mode=OneWay}" Margin="12" />
</StackPanel>
```

在代码隐藏文件中，将ShareTargetPageViewModel分配给ViewModel属性。在上述XAML代码中，此属性与编译绑定一起使用。此外，通过OnNavigatedTo方法，激活SharedTargetPageViewModel，并将ShareOperation对象传递给Activate方法（代码文件SharingTarget/ShareTargetPage.xaml.cs）：

```
public sealed partial class ShareTargetPage : Page
{
    public ShareTargetPage()
    {
        this.InitializeComponent();
    }
}
```

```
public ShareTargetPageViewModel ViewModel { get; } =
    new ShareTargetPageViewModel();

protected override void OnNavigatedTo(NavigationEventArgs e)
{
    ViewModel.Activate(e.Parameter as ShareOperation);

    base.OnNavigatedTo(e);
}
}
```

ShareTargetPageViewModel类定义了应在页面中显示的值的属性，并通过实现INotifyPropertyChanged接口提供更改通知（代码文件SharingTarget/ViewModels/ShareTargetViewModel.cs）：

```
public class ShareTargetPageViewModel: INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    public void OnPropertyChanged([CallerMemberName] string propertyName = null)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }

    // etc.

    private string _text;
    public string Text
    {
        get { return _text; }
        set
        {
            _text = value;
            OnPropertyChanged();
        }
    }

    private string _html;
    public string Html
    {
        get { return _html; }
        set
        {
            _html = value;
            OnPropertyChanged();
        }
    }

    private string _title;
    public string Title
    {
        get { return _title; }
        set
        {
            _title = value;
            OnPropertyChanged();
        }
    }

    private string _description;
    public string Description
```

```
{
    get { return _description; }
    set
    {
        _description = value;
        OnPropertyChanged();
    }
}
}
```

Activate方法是ShareTargetPageViewModel的重要部分。在这里，ShareOperation对象用于访问有关共享数据的信息，并获取一些元数据以显示给用户，例如Title、Description和可用数据格式列表。如果发生错误，则通过调用ShareOperation的ReportError方法向用户显示错误信息：

```
public class ShareTargetPageViewModel: INotifyPropertyChanged
{
    // etc.

    private ShareOperation _shareOperation;
    private readonly ObservableCollection<string> _shareFormats =
        new ObservableCollection<string>();
    public string SelectedFormat { get; set; }
    public IEnumerable<string> ShareFormats => _shareFormats;

    public void Activate(ShareOperation shareOperation)
    {
        string title = null;
        string description = null;
        try
        {
            _shareOperation = shareOperation;

            title = _shareOperation.Data.Properties.Title;
            description = _shareOperation.Data.Properties.Description;
            foreach (var format in
_shareOperation.Data.AvailableFormats)
            {
                _shareFormats.Add(format);
            }

            Title = title;
            Description = description;
        }
        catch (Exception ex)
        {
            _shareOperation.ReportError(ex.Message);
        }
    }
    // etc.
}
```

一旦用户选择数据格式，即可单击按钮检索数据。这进而会调用RetrieveData方法。根据用户的选择，会对Data属性返回的DataPackageView实例调用GetTextAsync或GetHtmlFormatAsync。在检索数据之前，

