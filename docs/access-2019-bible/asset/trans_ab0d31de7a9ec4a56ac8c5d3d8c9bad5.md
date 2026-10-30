

## 图22.7

对 Access 项目进行数字签名。

![](img/1e45673ab6eca9d20e67635ff5b9b318_755_0.png)

### 注意

在应用程序经过全面测试并且你预期不会再对其进行任何更改之前，请勿对 Access 项目进行签名。修改项目中的任何代码都会导致数字签名失效。

### 提示

为防止用户对项目中的代码进行未经授权的更改，请务必锁定项目并设置项目密码。

## 信任中心

信任中心是你可以找到 Access 安全和隐私设置的地方。要显示信任中心，请单击“文件”按钮，然后单击“选项”以打开“Access 选项”对话框。选择“信任中心”选项卡，然后单击“信任中心设置”。

以下是每个部分及其控制内容的说明：

- **受信任的发布者：** 显示受信任的发布者列表——即你在遇到可能不安全的宏时单击“信任来自此发布者的所有文档”的 Office 发布者。要从该列表中删除发布者，请选择该发布者并单击“删除”。受信任的发布者必须具有未过期的有效数字签名。

- **受信任位置：** 显示计算机或网络上受信任位置的列表。在此部分中，你可以添加、删除或修改计算机上始终包含受信任文件的文件夹。受信任位置中的任何文件都可以在不受信任中心检查的情况下打开。你还可以选择不允许网络工作位置，以及禁用所有受信任位置并接受已签名的文件。

- **受信任的文档：** 当选中“受信任的文档”时，Access 应用程序的名称会被添加到用户计算机系统注册表中的一个特殊区域。之后，每次使用该应用程序时，它都会被识别为受信任的文档，应用程序的所有宏、代码和其他元素都会启用，而不会中断用户的工作流程。

- 受信任的加载项目录：“受信任的加载项目录”部分允许你添加、删除或修改所信任的 SharePoint 目录。

- 加载项：允许你设置 Access 处理加载项的方式。你可以选择加载项是否需要来自受信任来源的数字签名，以及是否对未签名的加载项显示通知。你也可以选择禁用所有加载项，这可能会削弱功能。

- ActiveX 设置：允许你设置 ActiveX 控件的安全级别。

- 宏设置：允许你设置不在受信任位置中的宏的安全设置。（有关宏设置的更多信息，请参阅前面关于沙盒模式的部分。）

- 消息栏：允许你设置是否显示警告你有关被阻止内容的消息栏，或者从不显示有关被阻止内容的信息。

- 隐私选项：允许你选择 Microsoft Office Online 如何与你的计算机通信。你可以设置选项以使用 Microsoft Office Online 获取帮助、在启动时显示特色链接、下载文件以确定系统问题，以及注册“客户体验改善计划”。

## 多操作宏

宏的真正强大之处在于单击按钮即可执行多个操作。创建一个运行一系列操作查询的宏，比在导航窗格中双击每个操作查询更好——你可能会忘记运行其中一个，或者可能会以错误的顺序运行它们。

对于下一个示例，Chapter22.accdb 包含两个删除查询，用于从两个不同的表中删除数据：tblContacts_Backup 和 tblProducts_Backup。Chapter22.accdb 还包含两个追加查询，用于将记录从 tblContacts 和 tblProducts 复制到备份表中。

mcrBackupContactsAndProducts 宏（也可在 Chapter 22.accdb 示例数据库中找到）自动运行这四个查询，以便我们能够备份 tblContacts 表和 tblProducts 表中的数据。

表22.1 显示了 mcrBackupContactsAndProducts 的宏操作和操作参数（其中一部分如图22.8所示）。

> 注意
> 如果所有操作未出现在“操作”下拉列表中，请单击功能区“宏工具设计”选项卡“显示/隐藏”组中的“显示所有操作”命令。某些宏操作需要受信任的数据库或通过安全设置启用宏。此外，某些宏操作被认为是不安全的，因为它们会修改数据库中的数据或执行可能因使用不当而对应用程序造成损害的操作。被认为不安全的宏操作会在宏设计器中以警告图标（看起来像包含感叹号的黄色三角形）指示。默认情况下，Access 仅显示不受安全设置影响而运行的可信宏操作。

## 图22.8

mcrBackupContactsAndProducts 将数据从活动表归档到备份表中。

![](img/1e45673ab6eca9d20e67635ff5b9b318_757_0.png)

## 表22.1 mcrBackupContactsAndProducts

| 操作 | 操作参数 | 操作参数设置 |
|---|---|---|
| DisplayHourglassPointer | Hourglass On | Yes |
| SetWarnings | Warnings On | No |
| Echo | Echo On | No |
|  | Status Bar Text | Step 1: Deleting Data |
| OpenQuery | Query Name | qryDeleteContactsBackup |
|  | View | Datasheet |
|  | Data Mode | Edit |
| OpenQuery | Query Name | qryDeleteProductsBackup |
|  | View | Datasheet |
|  | Data Mode | Edit |
| Echo | Echo On | No |
|  | Status Bar Text | Step 2: Appending Data |
| OpenQuery | Query Name | qryAppendContactsBackup |
|  | View | Datasheet |
|  | Data Mode | Edit |
| OpenQuery | Query Name | qryAppendProductsBackup |
|  | View | Datasheet |
|  | Data Mode | Edit |
| Echo | Echo On | Yes |
|  | Status Bar Text | <Leave Blank> |
| SetWarnings | Warnings On | Yes |
| DisplayHourglassPointer | Hourglass On | No |
| MessageBox | Message | Contacts and Products have been archived. |
|  | Beep | Yes |
|  | Type | Information |
|  | Title | Finished Archiving |

该宏的核心是四个 OpenQuery 操作，它们运行四个操作查询。qryDeleteContactsBackup 和 qryDeleteProductsBackup 清除 tblContacts_Backup 和 tblProducts_Backup 的内容，以便将当前数据复制到其中。qryAppendContactsBackup 和 qryAppendProductsBackup 将 tblContacts 和 tblProducts 中的数据追加到备份表中。

当你看图22.8时，会注意到宏中一些操作（特别是 SetWarnings 和 Echo）旁边的警告图标。这些图标仅表示相关操作可能不安全，可能需要进一步检查。

下面是该宏执行的操作的详细介绍：

- DisplayHourglassPointer：此操作使用 Hourglass On 参数将光标更改为沙漏或指针。对于可能需要一段时间才能运行完的宏，请在宏开始时将此参数设置为 Yes，并在宏结束时设置为 No。请务必记住在宏结束时设置沙漏关闭；否则，沙漏光标将无限期保持。

- SetWarnings：此操作使用 Warnings On 参数打开或关闭系统消息。运行操作查询时，系统会提示你确认是否确实要运行该操作查询，询问是否可以删除这 58 条记录，然后对下一个操作查询再次询问。在宏开始时将 Warnings On 设置为 No，以关闭这些消息。将 Warnings On 设置为 No 的效果是自动单击警告的默认按钮（通常为“确定”或“是”）。不要忘记在宏结束时将警告重新设置为 Yes。一旦警告被关闭，在重新启用警告之前，用户不会收到 Access 关于重要操作（如删除记录）的确认消息。

- Echo：实际上，Echo 命令会“冻结”屏幕，使用户不会察觉到宏执行的活动。如果你希望隐藏宏的结果，请将 Echo On 参数设置为 No；如果希望显示结果，则设置为 Yes。设置 Status Bar Text 参数可向用户提示正在发生的事情。这在运行时间较长的宏中非常有用，可以了解宏在过程中的位置。

