

![](img/16f6e3fe08f01ddadb2741a92c392b0e_797_0.png)

Visual Studio 生成默认的 XML 文件并在代码和文本编辑器窗口中打开它。

## 4. 将下面以粗体显示的标记添加到 XML 文件中。

Click here to view code image

```
<?xml version="1.0" encoding="utf-8"?>
<VoiceCommands
xmlns="http://schemas.microsoft.com/voicecommands/1.2">
    <CommandSet xml:lang="en-us" Name="CustomersCommands">
        <CommandPrefix>Customers</CommandPrefix>
        <Example>Show details of John Sharp</Example>
    </CommandSet>
</VoiceCommands>
```

语音命令在命令集中定义。每个命令集都有一个命令前缀（由 CommandPrefix 元素指定），Cortana 可以在运行时使用它来识别应用程序。命令前缀不必与应用程序的名称相同。例如，如果你的应用程序名称很长或包含数字字符，Cortana 可能难以识别它，因此你可以使用命令前缀提供一个更短、更易发音的别名。Example 元素包含一个短语，显示用户如何调用命令。Cortana 在响应诸如“我说什么？”或“帮助。”之类的询问时显示此示例。

## Note

命令前缀应反映应用程序的目的，并且不应与其它知名应用程序或服务冲突。例如，如果你指定命令前缀为“Facebook”，如果提交到 Windows Store，你的应用程序可能无法通过验证测试。

5. 如果你不在美国，将 CommandSet 元素的 xml:lang 属性更改为反映你的区域设置。例如，如果你在英国，请指定 xml:lang="en-gb"。

这很重要。如果指定的语言与你的区域设置不匹配，Cortana 在运行时将无法识别你的语音命令。其背后的原理是，你应为应用程序将运行的每个区域设置指定一个单独的 CommandSet 元素。这使你能够为不同语言提供替代命令。Cortana 使用应用程序运行的机器的区域设置来确定使用哪个命令集。

6. 将下面以粗体显示的 Command 和 PhraseTopic 元素添加到 XML 文件中的 CommandSet 元素：

Click here to view code image

```
<?xml version="1.0" encoding="utf-8"?>
<VoiceCommands
xmlns="http://schemas.microsoft.com/voicecommands/1.2">
  <CommandSet xml:lang="en-us" Name="CustomersCommands">
    <CommandPrefix>Customers</CommandPrefix>
    <Example>Show details of John Sharp</Example>

    <Command Name="showDetailsOf">
      <Example>show details of John Sharp</Example>
      <ListenFor RequireAppName="BeforeOrAfterPhrase">
        show details of {customer}
      </ListenFor>
      <ListenFor RequireAppName="BeforeOrAfterPhrase">
        show details for {customer}
      </ListenFor>
      <ListenFor RequireAppName="BeforeOrAfterPhrase">
        search for {customer}
      </ListenFor>
      <Feedback>Looking for {customer}</Feedback>
      <Navigate/>
    </Command>
    <PhraseTopic Label="customer" Scenario="Search">
      <Subject>Person Names</Subject>
    </PhraseTopic>
  </CommandSet>
```

```
</CommandSet>
</VoiceCommands>
```

你可以向命令集添加一个或多个命令，每个命令都可以调用应用程序中的不同操作。每个命令都有一个唯一的标识符（Name 属性）。此标识符传递给 Cortana 调用的应用程序，以便应用程序可以确定用户说了哪个命令，从而确定要执行哪个操作。

Example 元素中的文本由 Cortana 显示，如果用户响应“我说什么？”查询而选择你的应用；Cortana 将显示你的应用理解的每个命令的示例短语。

ListenFor 元素由 Cortana 用于识别应调用此应用的请求。你可以指定多个 ListenFor 短语，为用户提供灵活性。在此情况下，用户可以说同一短语的三种变体来调用命令。用户所说的短语应包含应用程序的名称或 CommandSet 元素中指定的前缀。在此示例中，名称（或前缀）可以在所说短语的开头或结尾指定（RequireAppName 属性设置为 BeforeOrAfterPhrase）——例如，“Customers, show details of John Sharp”或“Search for John Sharp in Customers”。ListenFor 短语中的文本 {customer} 是一个占位符，受 PhraseTopic 元素管辖（稍后描述）。

Feedback 元素在 Cortana 识别请求时由 Cortana 朗读。用户指定的客户将被替换到 {customer} 占位符中。

Navigate 元素表示 Cortana 将在前台启动应用。你可以可选地指定应显示哪个页面（如果应用包含多个页面）作为此元素的 Target 属性。Customers 应用仅包含一个页面，因此未指定 Target 属性。如果应用 intended 在后台运行并将数据传回供 Cortana 显示，则指定 VoiceCommandService 元素而不是 Navigate。有关更多信息，请访问 Cortana 在线上的页面“Launch a background app with voice commands”，网址为 https://msdn.microsoft.com/library/dn974228.aspx。

PhraseTopic 元素用于定义口语短语中的占位符。Label 属性指定元素与哪个占位符相关联。在运行时，Cortana 将在此短语位置所说的词或词组替换为短语主题。Scenario 属性和 Subject 元素是可选的，并为 Cortana 提供有关如何解释这些词的提示。在此示例中，这些词用作搜索参数，构成人名。你可以指定其它场景，例如 *Short Message* 或 *Natural Language*，在这种情况下，Cortana 可能会以不同方式解析这些词。你还可以指定替代主题，例如地址、电话号码或城市和州。

- 7. 在文件菜单上，单击保存 CustomerVoiceCommands.xml，然后关闭文件。

- 8. 在解决方案资源管理器中，选择 CustomerVoiceCommands.xml 文件。在属性窗口中，将复制到输出目录属性更改为如果更新则复制。

此操作会导致 XML 文件在更改时被复制到应用程序文件夹并随应用部署。

下一步是在应用运行时将语音命令注册到 Cortana。你可以在 App.xaml.cs 文件中 *OnLaunched* 方法的代码中执行此操作。*OnLaunched* 方法在每次发生 *Launched* 事件时应用程序开始运行时都会发生。当应用程序关闭时，你可以保存有关应用程序状态的信息（例如用户正在查看哪个客户），并且你可以使用此事件在应用程序再次启动时恢复应用程序的状态（通过显示相同的客户）。你还可以使用此事件执行每次应用程序运行时应发生的操作。

## Register voice commands with Cortana

- 1. 在解决方案资源管理器中，展开 App.xaml，然后双击 App.xaml.cs 以在代码和文本编辑器窗口中显示该文件。

- 2. 在文件顶部列表中添加以下 *using* 指令。

Click here to view code image

```
using Windows.Storage;
using Windows.ApplicationModel.VoiceCommands;
using System.Diagnostics;
```

- 3. 找到 *OnLaunched* 方法并通过添加 *async* 修饰符启用异步操作：

Click here to view code image

```
protected async override void OnLaunched(LaunchActivatedEventArgs e)
{
    ...
}
```

- 4. 将下面以粗体显示的代码添加到 *OnLaunched* 方法的末尾：

Click here to view code image

```
protected async override void OnLaunched(LaunchActivatedEventArgs
e)
{
    ...
    // Ensure the current window is active
    Window.Current.Activate();

    try
    {
        var storageFile = await Package.Current.
            InstalledLocation.GetFileAsync(@"CustomerVoiceCommands
        await VoiceCommandDefinitionManager.
            InstallCommandDefinitionsFromStorageFileAsync(storageF
    }
    catch (Exception ex)
    {
        Debug.WriteLine(
            $"Installing Voice Commands Failed:
{ex.ToString()}");
    }
}
```

第一个语句从应用程序文件夹中检索包含语音命令定义的 XML 文件。然后将此文件传递给 VoiceCommandDefinitionManager 管理器。此类提供与操作系统注册和查询语音命令定义的接口。静态 InstallCommandDefinitionsFromStorageFileAsync 方法注册在指定存储文件中找到的语音命令。如果在此过程中发生异常，则记录异常，但允许应用程序继续运行（它只是不会响应语音命令）。

最后一步是让你的应用在 Cortana 识别 intended 用于该应用的语音命令时做出响应。在此情况下，你可以使用 App 类的 OnActivated 方法捕获 Activated 事件。此方法传递一个类型为 IActivatedEventArgs 的参数，其中包含描述传递给应用的数据的信息，包括任何语音激活命令的详细信息。

## Handle voice activation in the Customers app

- 1. 在代码和文本编辑器窗口中，将 OnActivated 事件方法添加到 App 类的末尾，如下所示：

Click here to view code image

```
protected override void OnActivated(IActivatedEventArgs args)
{
    base.OnActivated(args);
}
```

此语句调用重写的 OnActivated 方法，以在处理语音激活之前执行所需的任何默认激活处理。

- 2. 将下面以粗体显示的 if 语句块添加到 OnActivated

