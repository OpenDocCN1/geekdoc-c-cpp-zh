

method:

Click here to view code image

```
protected override void OnActivated(IActivatedEventArgs args)
{
    base.OnActivated(args);

    if (args.Kind == ActivationKind.VoiceCommand)
    {
        var commandArgs = args as VoiceCommandActivatedEventArgs;
        var speechRecognitionResult = commandArgs.Result;
        var commandName =
 speechRecognitionResult.RulePath.First();
    }
}
```

此块用于确定应用是否由 Cortana 通过语音命令激活。如果是，则 args 参数包含一个 VoiceCommandActivatedEventArgs 对象。Result 属性包含一个 speechRecognitionResult 对象，其中包含有关命令的信息。此对象中的 RulePath 列表包含触发激活的短语的元素，而该列表中的第一项包含 Cortana 识别的命令的名称。在 Customers 应用中，CustomerSearchCommands.xml 文件中定义的唯一命令是 showDetailsOf 命令。

3. 将以下以粗体显示的代码添加到 OnActivated 方法中：

Click here to view code image

```
if (args.Kind == ActivationKind.VoiceCommand)
{
    ...
    var commandName = speechRecognitionResult.RulePath.First();
    string customerName = "";

    switch (commandName)
    {
        case "showDetailsOf":
            customerName =
 speechRecognitionResult.SemanticInterpretation.
            Properties["customer"].FirstOrDefault();
            break;

        default:
            break;
    }
}
```

switch 语句验证语音命令是否为 showDetailsOf 命令。如果添加更多语音命令，应扩展此 switch 语句。如果语音数据包含其他未知命令，则会被忽略。

speechRecognitionResult 对象的 SemanticInterpretation 属性包含 Cortana 识别的短语的属性信息。Customers 应用的命令包含 {customer} 占位符，此代码检索用户所说且由 Cortana 解析的该占位符的文本值。

4. 在 OnActivated 方法的末尾，在 switch 语句之后添加以下代码：

Click here to view code image

```
protected override void OnActivated(IActivatedEventArgs args)
{
    ...
    if (args.Kind == ActivationKind.VoiceCommand)
    {
        ...
        switch (commandName)
        {
            ...
        }

        Frame rootFrame = Window.Current.Content as Frame;
        if (rootFrame == null)
        {
            rootFrame = new Frame();
            rootFrame.NavigationFailed += OnNavigationFailed;
            Window.Current.Content = rootFrame;
        }

        rootFrame.Navigate(typeof(MainPage), customerName);
        Window.Current.Activate();
    }
}
```

这里的第一块是确保有应用程序窗口打开以显示页面的样板代码。第二块在此窗口中显示 MainPage 页面。Frame 对象的 Navigate 方法使 MainPage 成为活动页面。第二个参数作为对象传递，可供页面用于提供有关要显示内容的上下文信息。在此代码中，该参数是一个包含客户名称的字符串。

5. 在代码和文本编辑器窗口中打开 ViewModel.cs 文件并找到 ViewModel 构造函数。此构造函数中的代码已略微重构，并且初始化视图状态的语句已移至名为 _initializeState 的单独方法中，如下所示：

Click here to view code image

```
public ViewModel()
{
    _initializeState();
    this.customers = DataSource.Customers;
}
```

```
private void _initializeState()
{
    this.currentCustomer = 0;
    this.IsAtStart = true;
    this.IsAtEnd = false;
    this.NextCustomer = new Command(this.Next, () =>
        { return this.customers.Count > 1 && !this.IsAtEnd; });
    this.PreviousCustomer = new Command(this.Previous, () =>
        { return this.customers.Count > 0 && !this.IsAtStart; });
}
```

6. 向 ViewModel 类添加另一个构造函数。此构造函数应接收一个包含客户名称的字符串，并使用此名称过滤数据源中的记录，如下所示：

Click here to view code image

```
public ViewModel(string customerName)
{
    _initializeState();

    string[] names = customerName.Split(new[] {' '}, 2,
        StringSplitOptions.RemoveEmptyEntries);

    this.customers =
        (from c in DataSource.Customers
        where string.Compare(c.FirstName.ToUpper(),
        names[0].ToUpper()) == 0 &&
            (names.Length > 1 ?
                string.Compare(c.LastName.ToUpper(),
        names[1].ToUpper()) == 0 : true)
            select c).ToList();
}
```

客户姓名可以包含两部分：名字和姓氏。String 类的 Split 方法可以根据分隔符字符列表将字符串拆分为子字符串。在此情况下，Split 方法将客户姓名最多分为两部分，如果用户提供由一个或多个空格字符分隔的名字和姓氏。结果存储在 names 数组中。LINQ 查询使用此数据查找名字与 names 数组中的第一项匹配且姓氏与 names 数组中的第二项匹配的所有客户。如果用户只指定一个名字，则 names 数组将只包含一项，LINQ 查询仅与名字匹配。为了消除大小写敏感性，所有字符串比较均针对字符串的大写版本执行。匹配客户的 resulting 列表被分配给视图模型中的 customers 列表。

7. 返回代码和文本编辑器窗口中的 MainPage.xaml.cs 文件。
8. 将以下所示的 OnNavigatedTo 方法添加到 MainPage 类的末尾，构造函数之后：

Click here to view code image

```
public sealed partial class MainPage : Page
{
    public MainPage()
    {
        ...
    }

    protected override void OnNavigatedTo(NavigationEventArgs e)
    {
        string customerName = e.Parameter as string;

        if (!string.IsNullOrEmpty(customerName))
        {
            ViewModel viewModel = new ViewModel(customerName);
            this.DataContext = viewModel;
        }
    }
}
```

OnNavigatedTo 方法在应用程序通过 Navigate 方法显示（导航到）此页面时运行。提供的任何参数都出现在 NavigationEventArgs 参数的 Parameter 属性中。此代码尝试将 Parameter 属性中的数据转换为字符串，如果成功，则将此字符串作为客户名称传递给 ViewModel 构造函数。然后将 resulting ViewModel（应仅包含与此名称匹配的客户）设置为页面的数据上下文。

9. 在 Build 菜单上，单击 Build Solution 并验证解决方案是否成功编译。

作为最后的润色，下一个练习将添加一组图标，Windows 10 和 Cortana 可以使用这些图标在视觉上表示该应用。这些图标比 Blank App 模板提供的库存灰白十字图像更丰富多彩。

## 为 Customers 应用添加图标

- 1. 在 Solution Explorer 中，右键单击 Assets 文件夹，指向 Add，然后单击 Existing Item。
- 2. 在 Add Existing Item – Customers 对话框中，移动到 Documents 文件夹中的 \Microsoft Press\VCSBS\Chapter 26\Resources 文件夹，选择此文件夹中的三个 AdventureWorks 徽标文件，然后单击 Add。
- 3. 在 Solution Explorer 中，双击 Package.appxmanifest 文件以在 Manifest Designer 窗口中显示它。
- 4. 单击 Visual Assets 选项卡。然后，在左窗格中单击 All Image Assets。
- 5. 滚动到 Square 150x150 logo 部分。单击 Scale 100 图像正下方的省略号按钮，浏览到 Assets 文件夹，单击 AdventureWorksLogo150x150.png，然后单击 Open。此资产的图像应显示在框中。
- 6. 按照步骤 5 中的相同过程，将 Square 44x44 logo 的 Scale 100 图像设置为 Assets 文件夹中的 AdventureWorksLogo44x44.png，并将启动屏幕的 Scale 100 图像的值更改为 Assets 文件夹中的 AdventureWorksLogo620x300.png。
- 7. 在 Debug 菜单上，单击 Start Without Debugging 以构建并运行应用程序。验证启动屏幕在应用开始运行时短暂出现，然后显示名为 Orlando Gee 的客户的详细信息。您应该能够像以前一样在客户列表中前后移动。通过运行应用，您还注册了 Cortana 可用于调用应用的语音命令。
- 8. 关闭应用。

现在您可以测试 Customers 应用的语音激活功能。

## 测试搜索功能

- 1. 激活 Cortana，然后说出以下查询或在搜索框中键入：
- *Customers show details for Brian Johnson*

> Note
> 
> 无论您说出命令还是键入它，Cortana 的响应方式都应相同。

Cortana 应识别此命令应定向到 Customers 应用。

