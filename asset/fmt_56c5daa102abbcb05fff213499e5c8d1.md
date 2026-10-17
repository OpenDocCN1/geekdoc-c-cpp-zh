
`switch` 语句验证语音命令是否为 `showDetailsOf` 命令。如果你添加了更多语音命令，你应该扩展此 `switch` 语句。如果语音数据包含其他未知命令，则会将其忽略。

`speechRecognitionResult` 对象的 `SemanticInterpretation` 属性包含有关 Cortana 识别的短语属性的信息。`Customers` 应用的命令包括占位符，此代码检索用户口述并由 Cortana 解释的占位符的文本值。

### 4. 将以下代码添加到 `OnActivated` 方法的末尾，位于 `switch` 语句之后：

点击此处查看代码图像

```csharp
protected override void OnActivated(IActivatedEventArgs args)
{
    if (args.Kind == ActivationKind.VoiceCommand)
    {
        ...
        switch (commandName)
```

```
{
  ..
}
```

```csharp
Frame rootFrame = Window.Current.Content as Frame;
if (rootFrame == null)
{
  rootFrame = new Frame();
  rootFrame.NavigationFailed += OnNavigationFailed;
  Window.Current.Content = rootFrame;
}
```

```csharp
rootFrame.Navigate(typeof(MainPage), customerName);
Window.Current.Activate();
```

这里的第一个块是样板代码，确保应用程序窗口已打开以显示页面。第二个块在此窗口中显示 `MainPage` 页面。`Frame` 对象的 `Navigate` 方法使 `MainPage` 成为活动页面。第二个参数作为对象传递，页面可以使用它可以提供有关显示内容的上下文信息。在此代码中，参数是一个包含客户名称的字符串。

### 5. 在代码编辑器窗口中打开 `ViewModel.cs` 文件并找到 `ViewModel` 构造函数。此构造函数中的代码经过了重构，初始化视图状态的语句已移动到名为 `_initState` 的独立方法中，所示：

点击此处查看代码图像

```csharp
public ViewModel()
{
  _initState();
  this.customers = DataSource.Customers;
}
```

```csharp
private void _initState()
{
  this.currentCustomer = 0;
  this.IsStart = true;
  this.IsAtEnd = false;
  this.Next = new Command(() => { ... });
  this.Previous = new Command(() => { ... });
}
```

### 6. 在 `ViewModel` 中添加另一个构造函数。该构造函数应接收一个字符串并按如下方式过滤数据源：

```csharp
public ViewModel(string customerName)
{
    string[] names = customerName.Split(new[] { ' ' }, 2, StringSplitOptions.RemoveEmptyEntries);
    this.customers = (from c in DataSource.Customers
                      where c.FirstName.ToUpper() == names[0].ToUpper()
                      && (names.Length > 1 ? c.LastName.ToUpper() == names[1].ToUpper() : true)
                      select c).ToList();
}
```

客户名称可能包含部分：如果用户提供了姓和名，`Split` 方法将字符串拆分为两部分。结果存储在 `names` 数组中。为了消除大小写敏感，所有的字符串比较都是针对字符串的大写形式进行的。如果用户指定了单个名称，`names` 数组将只包含一个项，且 LINQ 查询将仅与第一个名称进行匹配。匹配的客户列表被赋值给视图模型中的 `customers`。

### 7. 返回 `MainPage.xaml` 文件。

### 8. 将此处所示的 `OnNavigatedTo` 方法添加到 `MainPage` 类的末尾，位于构造函数之后：

```csharp
public sealed partial class MainPage : Page
{
    public MainPage()
    {
        InitializeComponent();
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

当应用程序使用 `Navigate` 方法显示（导航到）此页面时会运行 `OnNavigatedTo` 方法。`NavigationEventArgs.Parameter` 属性提供的任何参数都解析为字符串，如果成功，此代码会将此字符串传递客户名称。生成的 ViewModel 然后被设置为页面的上下文。

### 9. 在生成菜单中点击生成解决方案并验证解决方案编译成功。

作为最后的完善，下一个练习添加一组 Windows 10 和 Cortana 可用于视觉上表示应用程序的图标。这些图标比空模板提供的灰色白色十字图像更具色彩。

## 在 Customers 应用中添加图标

### 1. 在解决方案管理器中，右键点击 `Assets` 文件夹，指向添加，然后点击现有项。

### 2. 在添加项对话框中，移动到文档文件夹中的 `\Microsoft Press\VCS Chapter 26Resources`，选择此文件夹中的三个 AdventureWorks 图标文件，然后点击添加。

### 3. 在解决方案管理器中，双击 `Package.appxmanifest` 以在程序设计器窗口中显示它。

### 4. 点击视觉资产选项卡。然后在左侧窗格中点击中磁贴。

### 5. 滚动到预览图像部分，并在缩放资产列表中点击 Scale 100 下方的省略号按钮。浏览到

进入 `Assets` 文件夹，点击 `AdventureWorksLogo150x150.png`，然后点击 Open。此资产的图像应显示在框中。

### 6. 在左窗格中，点击 App Icon（应用图标）。滚动到 Preview Images（预览图像）部分，在 Scaled Assets（缩放资产）列表中，点击 Scale 100 图像正方的省略号按钮。浏览到 `Assets` 文件夹，点击 `AdventureWorksLogo44x44.png`，然后点击 Open。

### 7. 在左窗格中，点击 Splash Screen（启动屏幕）。滚动到 Preview Images（预览图像）部分，在 Scaled Assets（缩放资产）列表中，点击 Scale 100 图像正方的省略号按钮。浏览到 `Assets` 文件夹，点击 `AdventureWorksLogo620x300.png`，然后点击 Open。

### 8. 在 Debug（调试）菜单上，点击 Start Without Debugging（不调试启动）来编译并运行应用程序。验证应用运行时启动屏幕是否短暂出现，然后显示名为 Orlando Gee 的客户详细信息。你应该能够以前一样在客户列表中来回移动。通过运行应用，你还注册了 Cortana 可用于调用该应用的语音命令。

### 9. 关闭应用。

你现在可以测试 Customers（客户）应用的语音激活了。

# 测试搜索功能

### 1. 激活 Cortana，然后说出查询或在搜索框中输入：

`Customers show details for Brian Johnson`

> 注意：如果你是说话而不是输入，请记住先通过“Hey, Cortana”提示提醒 Cortana。无论你是口述命令还是输入命令，Cortana 的响应方式都是相同的。

Cortana 应该识别出此命令应指向 Customers 应用。

![](img/74dd8343b56b72576ea64f076a8146e6_963_0.png)

Cortana 将将启动 Customers 应用并显示 Brian Johnson 的详细信息。注意命令栏中的 Previous（上一个）和 Next（下一个）按钮不可用，因为只有一个匹配的客户。

![](img/74dd8343b56b72576ea64f076a8146e6_964_0.png)

### 2. 返回 Cortana，然后说出查询或在搜索框中输入：

`Search for John in Customers`

这次，应用找到了所有名字名为 John 的客户。返回了多个匹配项，你可以使用命令栏中的 Previous 和 Next 按钮在结果之间移动。

### 3. 尝试其他搜索。注意，你可以使用格式“Search for ...”（搜索...）、“Show details for ...”（显示...的详细信息）和“Show details of ...”（显示...的详细信息），并在命令开头指定应用名称（由“in”前缀）。注意，如果你输入不同格式的查询，Cortana 将无法理解，而是会执行 Bing 搜索。

### 4. 完成后，返回 Visual Studio。

# 为语音命令提供语音响应

在应用中添加语音命令时，你可以让它进行语音响应。要实现这一点，UWP 应用使用了 Windows 10 提供的语音合成功能。实现此功能相当简单，但有一条礼仪是你应该遵守的：应用程序只有在被呼唤时才进行语音响应。如果用户使用的是短语而不是口述，应用程序应保持沉默。幸运的是，你可以通过检查对命令进行语义解释时返回的 `commandMode` 属性来检测命令是口说的还是输入的，如下所示：

点击此处查看代码图像

```csharp
SpeechRecognitionResult speechRecognitionResult = ...;
string commandMode = speechRecognitionResult.SemanticInterpretation.Properties["commandMode"].FirstOrDefault();
```

`commandMode` 属性的值是一个字符串，根据用户输入命令的方式，将包含 "text" 或 "voice"。在下面的练习中，你将使用此字符串来确定应用程序应该进行语音响应还是保持沉默。

## 为搜索请求添加语音响应

### 1. 在 Visual Studio 中，打开 `App.xaml.cs` 文件并在代码和文本编辑器（Code and Text Editor）窗口中显示它。

### 2. 在 `OnActivated` 方法中，添加如下加粗所示语句：

点击此处查看代码图像

```csharp
protected override void OnActivated(IActivatedEventArgs args)
{
    if (args.Kind == ActivationKind.VoiceCommand)
    {
        var commandArgs = args as VoiceCommandActivatedEventArgs;
        var speechRecognitionResult = commandArgs.Result;
        var commandName = speechRecognitionResult.RulePath.First();
        string commandMode =
            speechRecognitionResult.SemanticInterpretation.
            Properties["commandMode"].FirstOrDefault();
    }
```

```csharp
string customerName = "";
...
}
}
```

### 3. 在方法末尾，更改调用 `Navigate` 方法的语句，以便第二个参数传递 `NavigationArgs` 对象。此对象封装了客户名称和命令模式。

[点击此处查看代码图像](#)

```csharp
protected override void OnActivated(IActivatedEventArgs args)
{
    if (args.Kind == ActivationKind.VoiceCommand)
    {
        Switch (commandName)
        {
        }
    }
    rootFrame.Navigate(typeof( MainPage), new NavigationArgs{customerName, commandMode});
    Window.Current.Activate();
}
```

Visual Studio 将报告找不到 `NavigationArgs` 类型。此发生是因为 `NavigationArgs` 类型尚不存在；你需要创建它。

### 4. 右键点击 `NavigationArgs` 引用并点击 Quick Actions（快速操作）。在新文件中生成类（Generate Class），所示：

![](img/74dd8343b56b72576ea64f076a8146e6_963_0.png)

此操作将创建一个名为 `NavigationArgs.cs` 的新文件，其中包含带有 `customerName` 和 `commandMode` 字段的类，以及填充这些字段的构造函数。

### 5. 在解决方案管理器（Solution Explorer）中，双击 `NavigationArgs.cs` 文件在代码编辑器窗口中显示它。

### 6. 修改 `customerName` 和 `commandMode` 字段，使其成为可以从外部访问的只读属性：

```csharp
internal class NavigationArgs
{
internal string commandMode { get; }
internal string customerName { get; }
public NavigationArgs(string customerName, string commandMode)
{
this.customerName = customerName;
this.commandMode = commandMode;
}
```

### 7. 返回代码编辑器窗口中的 `MainPage.xaml.cs`，找到 `OnNavigatedTo` 方法。将此方法标记为 `async`，并按如下修改体内的代码：

点击此处查看代码图像

```csharp
protected override async void OnNavigatedTo(NavigationEventArgs e)
{
    NavigationArgs args = e.Parameter as NavigationArgs;
    if (args != null)
    {
        string customerName = args.customerName;
        ViewModel viewModel = new ViewModel(customerName);
        this.DataContext = viewModel;
    }
    if (args.commandMode == "voice")
    {
        if (viewModel.Current != null)
        {
            await Say("$Here are the details for ");
        }
        else
        {
            await Say("was not found");
        }
    }
}
```

注意 `Say` 方法尚未实现。稍后我们将创建此方法。

### 8. 在文件顶部的列表中添加以下 `using` 指令：

点击此处查看代码图像

```csharp
using Windows.Media.SpeechSynthesis;
using System.Threading.Tasks;
```

### 9. 将所示的 `Say` 方法添加到 `MainPage` 类的末尾：

点击此处查看代码图像

```csharp
private async Task Say(string message)
{
    MediaElement mediaElement = new MediaElement();
    var synth = new SpeechSynthesizer();
    SpeechStream stream =
    await synth.SynthesizeTextToStreamAsync(message);
```
