
| Command | 当按钮控件被点击时触发。此事件帮助你在 Web 页面上创建多个控件，然后通过程序确定点击了哪个按钮控件 |

按钮控件用于在 Web 页面上创建推送按钮。你可以使用提交按钮或 `Button` 控件。`Button` 控件默认是提交按钮。

# 深入解析

| 属性 | 描述 |
| --- | --- |
| `AutoCompleteType` | 获取或设置一个指示 `TextBox` 控件自动补全行为的值 |
| `AutoPostBack` | 获取或设置一个值，指示 `TextBox` 控件在失去焦点时是否发生向服务器的自动回传 |
| `CausesValidation` | 获取或设置一个值，指示当 `TextBox` 控件在发生回传事件时被设置为验证客户端或服务器时，是否执行验证 |
| `Columns` | 获取或设置文本框中字符的显示宽度 |
| `MaxLength` | 获取或设置文本框中允许的最大字符数 |
| `ReadOnly` | 获取或设置一个值，指示 `TextBox` 是否可以被更改 |
| `Rows` | 获取或设置多行文本框中显示的行数 |
| `Text` | 获取或设置 `TextBox` 控件的文本 |
| `TextMode` | 获取或设置 `TextBox` 控件的行为模式（单行、多行或密码） |
| `ValidationGroup` | 获取或设置当 `TextBox` 控件回传到服务器时，由 `TextBox` 控件对其进行验证的控件组 |
| `Wrap` | 获取或设置一个值，指示多行文本框中的文本是否换行 |

`TextBox` 类的事件列在表 11.9 中：

| 事件 | 描述 |
| --- | --- |
| `TextChanged` | 当用户更改 `TextBox` 控件的文本时发生 |

# Label 控件

`Label` 控件用于显示用户无法编辑的文本。该控件存在于 `System.Web.Controls` 命名空间中。`Label` 类的层次结构如下：

+   * `System.Object`
  * `System.Web.Controls.WebControl`
  * `System.Web.UI.Controls.Label`

`Label` 类中值得关注的公共属性列在表 11.10 中：

| 属性 | 描述 |
| --- | --- |
| `AccessKey` | 指定访问键，允许您导航到 Web 服务器控件 |
| `AssociatedID` | 获取或设置与 `Label` 控件关联的控件的标识 |
| `BackColor` | 指定 `Label` 控件的背景颜色 |
| `Border` | 指定 `Label` 控件的边框颜色 |
| `Border` | 指定 `Label` 控件的边框样式 |
| `BorderRadius` | 指定 `Label` 控件的边框宽度 |
| `Font` | 获取字体属性 |
| `ForeColor` | 指定文本颜色 |
| `Height` | 指定 `Label` 控件的高度 |
| `Text` | 获取或设置在 `Label` 中显示的文本 |
| `Width` | 指定 `Label` 控件的宽度 |

471

# 第 11 章：标准 Web 控件

## HyperLink 控件

`HyperLink` 控件用于创建指向另一个 Web 页面的链接，该页面可以是您的 Web 应用程序中的页面，也可以是万维网上的任何地方。`HyperLink` 控件存在于 `System.Web.WebControls` 命名空间中。`HyperLink` 类的继承层次结构如下：

```
System.Object
System.Web.UI.WebControls
System.Web.UI.WebControls.HyperLink
```

您可以在当前页面上通过 URL 指定链接页的位置。您可以在 `HyperLink` 控件中使用文本或图像。文本通过 `Text` 属性指定，图像通过 `Image` 属性指定。默认情况下，当您点击 `HyperLink` 时，链接的内容将在新的浏览器窗口中显示。您可以设置 `Target` 属性来指定窗口或框架的名称，如表 11:11 所示。

| 表 11:11：HyperLink 类的 Target 属性选项 |
| 属性 | 描述 |
| --- | --- |
| `_blank` | 在无框架的新窗口中显示链接内容 |
| `_parent` | 在直接父级框架中显示链接内容 |
| `self` | 在当前框架中显示链接内容 |
| `_top` | 在无框架的全窗口中显示链接内容 |
| `_search` | 在搜索页面中显示链接内容 |

`HyperLink` 类没有非派产生的方法或事件。`HyperLink` 类中值得关注的属性列在表 11:12 中。

| 表 11:12：HyperLink 类的值得关注的属性 |
| 属性 | 描述 |
| --- | --- |
| `ImageUrl` | 获取用于 `HyperLink` 控件显示的图像的路径 |
| `NavigateUrl` | 获取点击 `HyperLink` 控件时链接到 Web 页面的 URL |
| `Target` | 获取点击 `HyperLink` 控件时显示 Web 页面的目标窗口 |
| `Text` | 获取 `HyperLink` 控件的文本说明 |

## LinkButton 控件

`LinkButton` 控件是另一种标准 Web 控件，用于将当前 Web 页面链接到其他 Web 页面。`HyperLink` 控件和 `LinkButton` 控件之间的区别在于，前者用于导航到浏览器或 Web 页面，而后者还可以借助控件的 `Click` 和 `Command` 事件执行某些其他操作。`LinkButton` 类的继承层次结构如下：

```
System.Object
System.Web.UI.WebControls
System.Web.UI.WebControls.LinkButton
```

`LinkButton` 类没有非派产生的方法。`LinkButton` 类中值得关注的属性列在表 11:13 中。

| 表 11:13：LinkButton 类的值得关注的公共属性 |
| 属性 | 描述 |
| --- | --- |
| `CausesValidation` | 获取一个值，显示在点击 `LinkButton` 控件时是否执行验证 |
| `CommandArgument` | 获取传递给 `Command` 事件的可选参数 |

### 深入解析

| 表 13：LinkButton 类的值得关注属性 |
| 属性 | 描述 |
| --- | --- |
| `CommandName` | 获取与 `LinkButton` 控件关联的命令名称。该值与 `CommandArgument` 属性一起传递给命令事件处理器 |
| `OnClient` | 获取在触发时执行的客户端脚本 |
| `PostBackURL` | 获取点击 `LinkButton` 控件时所在页面的 URL |
| `Text` | 获取 `LinkButton` 控件上的文本说明 |
| `ValidationGroup` | 获取 `LinkButton` 控件回传到服务器时对其进行验证的控件组 |

`LinkButton` 控件值得关注的公共事件列在表 11.14 中。

| 表 11.14：LinkButton 类的值得关注事件 |
| 事件 | 描述 |
| --- | --- |
| `Click` | 点击 `LinkButton` 且关联命令名称时触发 |
| `Command` | 点击 `LinkButton` 且关联命令名称时触发 |

### Literal 控件

与 `Label` 类似，`Literal` 控件是另一种在 Web 页面上显示文本的服务器控件。在 ASP.NET 中，您可以通过 `Literal` 控件在容器内部添加 HTML 代码，而无需切换 `.aspx` 页面。`Literal` 控件存在于 `System.UI.WebControls` 命名空间中。该类的层次结构如下：

```
System.Object
System.web.ui.WebControls.Literal
```

表 11.15 列出了 `Literal` 类值得关注的公共属性：

| 表 11.15：Literal 类的值得关注的公共属性 |
| 属性 | 描述 |
| --- | --- |
| `Mode` | 获取或设置一个枚举值，指定 `Literal` 中内容的渲染方式 |
| `Text` | 获取或设置在 `Literal` 中显示的说明 |

可以使用 `Literal` 控件的 `Text` 属性进行设置。该控件在 Web 页面上没有任何视觉外观。

### Placeholder 控件

`Placeholder` 控件作为一个容器，持有运行时在 Web 页面上显示的控件。它产生产生视觉输出。`Placeholder` 控件的类层次结构如下：

```
System.Object
System.web.ui.WebControls.PlaceHolder
```

`Placeholder` 类中值得关注的公共属性列在表 11.16 中。

| 表 11.16：Placeholder 类的公共属性 |
| 属性 | 描述 |
| --- | --- |
| `EnableTheming` | 获取或设置一个值，指示主题是否应用于 `Placeholder` 控件 |

## 第 1 章：标准 Web 控件

### HiddenField 控件

`HiddenField` 控件存储一个跨越向服务器提交（post）的值。通常情况下，使用视图状态（view-state）、会话状态（session-state）和 Cookie 来维护 Web 页面的状态。如果这些方法被禁用或不可用，你可以使用 `HiddenField` 控件来存储状态值。`HiddenField` 类的层次结构如下：

```
System.Object
System.web.UI.Control
System.web.UI.Controls.hiddenField
```

表 11.17 列出了 `HiddenField` 类值得注意的属性：

| 属性 | 描述 |
| :--- | :--- |
| `EnableTheming` | 获取或设置一个值，指示是否将主题应用于 `HiddenField` 控件 |
| `SkinID` | 获取或设置应用于 `HiddenField` 控件的皮肤 ID |
| `Value` | 获取或设置隐藏字段的值 |

### FileUpload 控件

`FileUpload` 控件由一个文本框和一个浏览（Browse）按钮组成，允许从本地或远程机器浏览文件并上传到 Web 服务器。可以通过在文本框提供提供上传文件的完整路径（例如 `MyFileUpload.txt`）来上传文件。另一方面，也可以点击浏览按钮并在“选择”对话框中定位文件来选择文件。`FileUpload` 类的层次结构如下：

```
System.Object
System.web.UI.Control
System.web.UI.Controls.FileUpload
```

表 11.18 列出了 `FileUpload` 类值得注意的属性：

| 属性 | 描述 |
| :--- | :--- |
| `FileBytes` | 获取使用 `FileUpload` 控件指定的文件中的字节数组 |
| `FileContent` | 获取一个指向要使用 `FileUpload` 控件上传的文件的 Stream 对象 |
| `FileName` | 获取使用 `FileUpload` 控件的客户端上的文件名 |
| `HasFile` | 获取一个值，指示 `FileUpload` 控件是否包含文件 |
| `PostedFile` | 为使用 `FileUpload` 控件上传的文件返回其底层的 `PostedFile` 对象 |

表 11.19 列出了 `FileUpload` 类值得注意的方法：

| 方法 | 描述 |
| :--- | :--- |
| `Saves` | 将已上传的数据保存到 Web 服务器上的指定路径上 |

### CheckBox 控件

`CheckBox` 控件创建一个可以通过点击选择的复选框。该控件存在于 `System.Web.UIControls` 命名空间中。`CheckBox` 控件显示复选框，允许用户在 True 或 False 值之间进行切换。`CheckBox` 类的层次结构如下：

```
System.Object
System.web.UI.Control
System.web.UI.Controls.WebControl
System.web.UI.Controls.CheckBox
```

#### 深度解析

表 11.20 列出了 `CheckBox` 类值得注意的公共属性：

| 表 11.20: CheckBox 类值得注意的公共属性 |
| 属性 | 描述 |
| :--- | :--- |
| `AutoPostBack` | 获取或设置一个值，显示在点击时 `CheckState` 是否会自动回传到服务器 |
| `CausesValidation` | 如果在 `CheckBox` 控件被控制时是否执行验证，则获取或设置一个布尔值 |
| `Checked` | 获取或设置一个值，显示 `CheckBox` 控件是否被选中 |
| `InputAttributes` | 获取 `CheckBox` 控件所有渲染的输入元素属性集合的引用 |
| `LabelAttributes` | 获取 `CheckBox` 控件所有渲染的 `LABEL` 元素属性集合的引用 |
| `Text` | 获取或设置与 `CheckBox` 控件关联的文本标签 |
| `TextAlign` | 获取或设置 `CheckBox` 控件中文本标签的位置 |
| `ValidationGroup` | 获取或设置在回传时 `CheckBox` 控件将导致触发验证的控件组 |

表 11.21 列出了 `CheckBox` 类值得注意的公共事件：

| 表 11.21: CheckBox 类值得注意的公共事件 |
| 事件 | 描述 |
| :--- | :--- |
| `Changed` | 当 `CheckBox` 属性的值在多次向服务器提交之间发生变化时触发 |

### RadioButton 控件

与 `CheckBox` 类似，`RadioButton` 控制单个按钮。`RadioButton` 存在于 `System.UI.WebControls` 命名空间中。`RadioButton` 可以进行分组，一次只能选择一个 `RadioButton` 控件。在 Web Forms 中，你必须将 `RadioButton` 的 `GroupName` 属性设置为相同的值以将它们关联为一组。`RadioButton` 类的层次结构如下：

```
System.Object
System.UI.Control
System.UI.WebControls.WebControl
System.UI.WebControls.CheckBox
System.UI.WebControls.RadioButton
```

该类也继承自 `CheckBox` 类。表 11.22 列出了 `RadioButton` 类值得注意的公共属性：

| 表 11.22: RadioButton 类值得注意的公共属性 |
| 属性 | 描述 |
| --- | --- |
| `GroupName` | 获取单选按钮所属组的名称 |

### ListBox 控件

`ListBox` 是一种标准的服务器控件，用于在运行时从 Web 上的项目列表中选择一个或多个项目。`ListBox` 类的继承层次结构为：

```
System.Object
System.UI.Control
System.UI.WebControls.WebControl
System.UI.WebControls.BaseBoundControl
System.UI.WebControls.DataBoundControl
System.UI.WebControls.ListControl
System.UI.WebControls.ListBox
```

## 第 11 章：标准 Web 控件

`ListBox` 的 `Rows` 属性可以用于指定控件的高度。将 `SelectionMode` 属性设置为 `ListSelectionMode.Multiple` 以启用多项选择。你可以通过 `SelectedItem` 和 `SelectedIndex` 属性在单选择 `ListBox` 中找到选中的项目。`SelectedItem` 属性将选中项目作为 `ListItem` 对象返回，该对象支持 `Text`、`Value` 和属性。在多选择 `ListBox` 中（这意味着我们从单个 `ListBox` 中选择多个项目），循环遍历 `ListBox` 控件中的选定项目并返回每个项目作为 `ListItem`。设置 `Selection` 属性可以清除选择。

`ListBox` 继承自 `ListControl` 类；此外，它没有任何非继承的方法。注意 `ListControl` 的项返回一个 `ListItem` 对象集合，你可以使用它来访问 `ListBox` 中的项目。表 11.23 列出了 `ListBox` 类值得注意的属性。

表 11.23: ListBox 注意的属性

| 属性 | 描述 |
| :--- | :--- |
| `Border` | 获取或设置控件的边框颜色 |
| `Border` | 获取或设置控件的边框样式 |
| `Border` | 获取或设置控件的边框宽度 |
| `Rows` | 获取或设置在 `ListBox` 中显示的行数 |
| `SelectionMode` | 获取或设置 `ListBox` 的选择模式 |

### DropList

`DropList` 控件以下拉列表的形式显示数据列表，你可以从中进行选择。`DropList` 控件存在于 `System.Web.UIControls` 命名空间中。你不能在此控件中选择多个项目，因为你从列表中做出选择后列表会自动关闭。`DropList` 类的继承层次结构如下：
