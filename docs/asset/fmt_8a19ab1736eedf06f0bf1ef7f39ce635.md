
使用 OFR 提供了一个画布，它不仅仅是在主要焦点旁边可见；OFR 提供了一个非常可配置的 UI，使你能够扩展或替换与 Outlook 中典型组件关联的默认界面。由于电子邮件已成为普遍的办公和家庭通信工具，能够自定义此媒介中关键业务数据的呈现方式是强大的。

开始时，创建一个名为 `ProVB_OFR` 的新 Outlook 加载项项目。 （此处未显示新建项目对话框或模板运行后 Visual Studio 中的初始视图的屏幕截图，因为 Outlook 加载项看起来与前面讨论的 Excel 加载项非常相似。）你将进入加载项的代码视图，其中包含 `Startup` 和 `Shutdown` 事件处理程序。

此时，将你的 OFR 添加到项目中。右键单击你的项目并从上下文菜单中选择 `Add` 选项以打开 `Add New Item` 对话框。如前所述，前往 Office 类别以查看可用模板，在那里你会找到一个 Outlook Form Region 模板（见图 25-26）。为其取一个有意义的名称，例如 `AdjoiningOFR`，以反映你将创建的表单区域类型。

![](img/d99870e80390742f93963da7be0b2e61_874_0.png)

FIGURE 25-26

### FIGURE 25-28

### 新建 Outlook 表单区域

选择要创建的表单区域类型

表单区域的类型决定了在 Outlook 中打开项目时表单区域出现的的位置。

### 你要创建哪种类型的表单区域？

- Separate

  在表单中添加一个新页面。

- Adjoining

  追加到表单底部。

- Replacement

  替换表单的默认页面。

- Replace-all

  替换整个表单。

![](img/d99870e80390742f93963da7be0b2e61_876_0.png)

< Previous   Next >   Finish   Cancel

### FIGURE 25-29

### 新建 Outlook 表单区域

标识将显示此表单区域的邮件类别

你可以将表单区域与标准或自定义邮件类别关联。

### 哪些标准邮件类别将显示此表单区域？

- Appointment (`IPM.Appointment`)
- Contact (`IPM.Contact`)
- Distribution List (`IPM.DistList`)
- Journal Entry (`IPM.Activity`)
- Mail Message (`IPM.Note`)
- Post (`IPM.Post`)
- RSS (`IPM.Post.RSS`)
- Task (`IPM.Task`)

要标识自定义邮件类别，请键入自定义邮件类别名称（例如：`IPM.Post.Contoso`）。用分号分隔多个邮件类别名称。

### 哪些自定义邮件类别将显示此表单区域？

< Previous   Next >   Finish   Cancel

请注意，图 25-29 显示的是你在选择了 Replacement 或 Replace-all OFR 类型时该对话框的外观。如前所述，这些表单类型会替换底层类别。在图 25-29 中，每个内置类别都已被禁用，因此你无法要求将更改应用于其中一种现有类型。相反，你唯一的选项是定义自定义类别或类别；最佳做法是定义单个类别。

此自定义邮件类别是你将在自定义加载项中定义的类别。为了更好地解释正在发生的情况，让我们以邮件消息为例。通常，当 Outlook 接收到邮件消息时，该消息会被分配到类别 `IPM.Note`。`IPM.Note` 类提供了你在 Outlook 中查看消息时看到的所有典型显示元素。如果你创建了一个替换表单，那么当该表单被发送时，它会被标记为不是典型消息，而是你自定义类别的一个实例。

换句话说，消息的发送方需要知道为此类型的 OFR 使用的类别名称。理论上，这就是发送方需要知道的全部内容——然而，那只是理论上。只要初始消息发送到 Microsoft Exchange Server，Replacement 和 Replace-all 表单类型就能正常工作。但是，如果你试图从例如 SharePoint 触发消息，就会出现问题。通常，在安装和配置 SharePoint 时，电子邮件选项会被设置成 SharePoint 处理自己的消息。但是，SharePoint 不允许发送具有自定义消息类型的消息，因此当你的代码尝试从 SharePoint 内部触发此自定义消息类型时，只有在你将 SharePoint 服务器配置为与 Exchange Server 通信时，消息才会被发送。

Replacement 和 Replace-all 表单还有其他独特功能。积极的一面是，与修改现有对象类型的 OFR 不同，Replacement 和 Replace-all 表单仅在接收到该特定类别的消息时才会被实例化。如本节后面所述，Adjoining 和 Separate 表单需要添加自定义代码来筛选何时应显示该 OFR。

Replacement 和 Replace-all 表单的另一个优点是，它们能让你更好地控制消息内容。底层正文中的任何文本都会被隐藏，这意味着你可以在消息正文中嵌入稍后将在表单中使用的信息。此外，这些表单类型还会隐藏附件，因此可以例如封入包含应用程序数据的 XML 文件，然后在打开消息时检索和处理此数据。

然而，对于本示例，你正在创建一个新的 Adjoining OFR，因此使用 Previous 按钮两次返回到图 25-28 所示的屏幕。将你的 OFR 类型从 Replacement 改为 Adjoining 并单击 Next。这应该会带你到图 25-30 所示的屏幕。在这里，你可以为你的 OFR 提供一个显示名称。为了看到此效果的影响，将单词 An 放在你的类名称开头，以便你能够看到此值的使用位置。

此对话框中的三个复选框代表此 OFR 在 Outlook 中默认可用的情况。在第一种情况下，至少你可能不希望接受该默认值。“Inspectors that are in compose mode” 使你能够确定创建新消息或联系人的人是否也应默认看到你的 OFR 区域。

尽管该设置适用于所有 OFR 类型，但实际上它并不适用于 Replacement 和 Replace-all。对于 Replacement 和 Replace-all 表单，Outlook 不会自动将其作为创建新消息的选项提供。相反，用户需要访问 File 菜单并选择 Forms 选项来告诉 Outlook 他们正尝试发送由自定义类型定义的消息。

### FIGURE 25-30

然而，对于 Separate 和 Adjoining 表单，如果你保持选中此项，Outlook 将自动将你的自定义区域添加到标准的新消息、联系人、约会等窗口中。如果你的用户不会向该 OFR 中输入数据而它仅用于显示，这可能会变得相当烦人。因此，在许多情况下，你会清除第一个复选框。但是，如果你正在自定义联系人以捕获和更新新的数据元素，你可能希望保留此复选框选中。

至于图 25-30 中的另外两个复选框，它们指的是显示你的自定义 OFR，通常这些保持选中状态，以便你的 OFR 可见以显示数据。

单击 Next 会带你到图 25-31 所示的对话框。此对话框使你能够从 Outlook 中使用的任何标准类别中进行选择。目标是使你能够为其中一个或多个类别创建一个自定义 OFR，尽管通常你只会选择一个。现在，只选择 Mail Message 并单击 Finish 以完成 OFR 的创建并返回到 Visual Studio。

返回 Visual Studio 后，你将进入 `AdjoiningOFR` 用户控件的设计器。对了，你再次使用的是一个 Windows 窗体用户控件，该控件已被 VSTO 团队自定义以提供你在前面向导中定义的功能。此时你可以打开工具箱并将控件拖放到表单上。

![](img/d99870e80390742f93963da7be0b2e61_879_0.png)

### FIGURE 25-31

图 25-32 说明了你可以做的一些更改，以便你的表单既可见又具有一些可操作的简单元素。图 25-32 所示的用户控件已分配了新的背景颜色，并在表单上拖放了两个标签控件。`Label1` 的字体已更改为更大尺寸，背景更改为白色。`Label1` 中的默认文本现在为零。`Label1` 左侧是 `Label2`，其文本已更新为“Attachment Count”。

![](img/d99870e80390742f93963da7be0b2e61_879_1.png)

### FIGURE 25-32

你还没有编写任何实际代码，所以现在是测试应用程序的好时机。使用 `F5` 构建并运行它。构建完成后，Outlook 将自动打开。你应该会看到与图 25-33 所示类似的内容。

![](img/d99870e80390742f93963da7be0b2e61_880_0.png)

### FIGURE 25-33

请注意，即使是两天前收到的原始 Outlook 测试消息，现在也包含了你的自定义 OFR。事实上，你会发现你打开的每条消息都包含 OFR——这很容易变得烦人，因为在实际应用程序中你的 OFR 可能只针对单一消息类型。同样，如果你选择创建新消息，它又出现了——一个仅包含显示信息的 OFR。在你对该区域对 Outlook 的影响感到满意后，关闭 Outlook 并返回 Visual Studio。

图 25-34 提供了你的 OFR 默认生成代码的视图。你的目标是完成两个任务：首先，使此 OFR 仅在关联的消息包含一个或多个附件时显示。其次，更新 `Label1` 以在 OFR 中显示附件数量。

首先要注意的是 Form Region Factory 代码块，它已被折叠。实际上有三个生成的 方法，而你希望放置自定义逻辑以指定何时应显示此 OFR 的方法就隐藏在这个代码块内部。展开后，如以下代码所示，你不仅拥有 `AdjoiningOFR` 类，而且在这个折叠块内部还有一个第二个 partial 类定义，它定义了一个工厂的实现以创建你的 OFR 作为工厂的一部分。工厂是一种众所周知的软件模式，其中调用应用程序可能不知道正在创建哪个类的细节，但只知道基类 OFR 以及在基类级别公开的方法和属性。

![](img/d99870e80390742f93963da7be0b2e61_881_0.png)

### 图 25-34

软件模式不在本章讨论范围内，但简而言之，工厂模式表明会有一个 `FormRegionInitializing` 事件处理程序，并且调用应用程序将能够根据每个 OFR 中实现的工厂创建几种不同类型的 OFR。代码如下：

```
Public Class AdjoiningOFR
#Region "Form Region Factory"
    <Microsoft.Office.Tools.Outlook.FormRegionMessageClass>
    (Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute.Note) _
    <Microsoft.Office.Tools.Outlook.FormRegionName("ProVB_OFR.AdjoiningOFR")> _
    Partial Public Class AdjoiningOFRFactory

        ' Occurs before the form region is initialized.
        ' To prevent the form region from appearing, set e.Cancel to true.
        ' Use e.OutlookItem to get a reference to the current Outlook item.
        Private Sub AdjoiningOFRFactory_FormRegionInitializing( _
                ByVal sender As Object, _
                ByVal e As _
                    Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs) _
                Handles Me.FormRegionInitializing

        End Sub

    End Class

#End Region

    'Occurs before the form region is displayed.
    'Use Me.OutlookItem to get a reference to the current Outlook item.
    'Use Me.OutlookFormRegion to get a reference to the form region.
    Private Sub AdjoiningOFR_FormRegionShowing(ByVal sender As Object, _
```

```
ByVal e As System.EventArgs) _
Handles MyBase.FormRegionShowing

End Sub
'Occurs when the form region is closed.
'Use Me.OutlookItem to get a reference to the current Outlook item.
'Use Me.OutlookFormRegion to get a reference to the form region.
Private Sub AdjoiningOFR_FormRegionClosed(ByVal sender As Object, _
    ByVal e As System.EventArgs) _
    Handles MyBase.FormRegionClosed

End Sub

End Class
```

代码片段来自 `AdjoiningOFR.vb`

为了防止 OFR 被显示，你需要在 `FormRegionInitializing` 事件处理程序中添加自定义代码。在这种情况下，你只需要确定消息是否有一个或多个附件。如果没有任何附件，则希望 OFR 保持隐藏：

```
Private Sub AdjoiningOFRFactory_FormRegionInitializing( _
    ByVal sender As Object, _
ByVal e As Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs) _
    Handles Me.FormRegionInitializing

    Try
        Dim mail = CType(e.OutlookItem, Outlook.MailItem)
        If Not mail.Attachments.Count > 0 Then
            e.Cancel = True
            Return
        End If
    Catch
        e.Cancel = True
    End Try
End Sub
```

代码片段来自 `AdjoiningOFR.vb`

前面的代码演示了筛选 OFR 的一些关键要素。首先要注意的是，你可以通过从参数 `e` 中检索 `OutlookItem` 对象来访问传入的电子邮件消息。当然，你需要转换该项，因为它是作为 `Object` 类型传递的。完成此操作后，你就可以完全访问 Outlook 对象模型中有关电子邮件消息的内容。因此，你可以快速确定附件的数量；如果没有附件，则可以将 `Cancel` 属性设置为 `True`。

下一个任务是将消息中的附件数量放入 OFR 中。这是一项相当简单的任务。与在代码即将创建 OFR 时决定是否显示 OFR 不同，你影响所显示内容的能力要等到调用 `FormRegionShowing` 事件处理程序时才会发生。在下面的代码块中，不是从参数中检索当前电子邮件对象，而是从 OFR 的成员值之一获取：

```
Private Sub AdjoiningOFR_FormRegionShowing(ByVal sender As Object, _
    ByVal e As System.EventArgs) _
    Handles MyBase.FormRegionShowing

    Dim mail = CType(Me.OutlookItem, Outlook.MailItem)
    Me.Label1.Text = mail.Attachments.Count
End Sub
```

代码片段来自 `AdjoiningOFR.vb`

因此，获取附件数量并将其赋值给标签内容的代码归结为两行自定义代码。此时，你可以重新运行应用程序来测试代码。一旦 Outlook 打开，你应该会看到以前为所有消息显示的 `AnAdjoiningPane` 现在消失了，除非是在带有附件的消息的情况下。

这意味着当你现在创建新消息时，OFR 仍然不会显示。但是，如果你添加附件，然后在发送前保存该消息，你可以重新打开已保存的消息，会看到 OFR 显示。请记住，是否显示 OFR 的决定发生在 OFR 创建期间，并且一旦 OFR 被隐藏，在对象保持打开状态时你无法更改该设置。

### 小结

本章介绍了 VSTO 及其许多新特性。文中并没有花大量时间讨论如何向用户控件添加控件和逻辑，而是重点介绍了如何使用自定义任务窗格或操作窗格，以及如何利用诸如内容控件之类的新功能。

VSTO 不仅仅是一组简单的扩展，来镜像你在 VBA 中能做的事情。事实上，VSTO 扩展了 Office 系统中的每个客户端，并提供了多个模板。它使 Word 和 Excel 具有灵活性，可以在文档级进行自定义，或者通过创建自定义加载项进行自定义；如果你确实在文档级进行自定义，它还可以选择与文档中已有的任何 VBA 代码进行互操作。
