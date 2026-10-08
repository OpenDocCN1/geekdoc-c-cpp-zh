
# 第 11 章：标准 Web 控件

```
System.Object
System.Web.UI.Control
System.UI.WebControls.Control
System.UI.WebControls.BaseBoundControl
System.UI.WebControls.DataBoundControl
System.UI.WebControls.ListControl
System.UI.WebControls.DropDownList
```

`DropDown` 类继承自 `ListControl` 类，并且没有非继承的方法或事件。表 11.24 列出了 DropList 类值得注意的属性。

表 11.24: DropDown 类值得注意的属性

| 属性 | 描述 |
| :--- | :--- |
| `BorderColor` | 获取或设置控件的边框颜色 |
| `BorderStyle` | 获取或设置控件的边框样式 |
| `BorderWidth` | 获取或设置控件的边框宽度 |
| `SelectedIndex` | 获取或设置控件中选中项目的索引 |

## BulletedList

`BulletedList` 控件是一种标准的 Web 服务器控件，用于在 Web上上以项目列表的形式显示项目。`BulletedList` 类的层次结构如下：

```
System.Object
System.Web.UI.Control
System.UI.WebControls.Control
System.UI.WebControls.BaseBoundControl
System.UI.WebControls.DataBoundControl
System.UI.WebControls.ListControl
System.UI.WebControls.BulletedList
```

### 深度解析

`BulletedList` 类没有非继承的方法，它继承自 `ListControl` 类。`BulletedList` 类值得关注的公共属性如表 11.25 所示。

表 11.25: BulletedList 类值得关注的公共属性

| 属性 | 说明 |
| :--- | :--- |
| `AutoPostBack` | 获取或设置基类控件的 `AutoPostBack` 属性值 |
| `BulletImageUrl` | 获取或设置 `BulletedList` 控制中每个项目符号的图像路径 |
| `BulletStyle` | 获取或设置 `BulletedList` 控制中符号的样式 |
| `Controls` | 获取该控件的控件集合（`ControlCollection`） |
| `FirstBulletNumber` | 获取或设置有序 `BulletedList` 控制中项目列表开始的数值 |
| `SelectedIndex` | 获取或设置 `BulletedList` 控制中当前选中项的从 0 开始的索引 |
| `SelectedItem` | 获取 `BulletedList` 控制中当前选中项 |
| `SelectedValue` | 获取或设置 `BulletedList` 控制中选中 `ListItem` 的值 |
| `Target` | 获取或设置点击 `BulletedList` 控制中的超链接时显示链接 Web 页面的目标窗口 |
| `Text` | 获取或设置 `BulletedList` 控制的文本 |

`BulletedList` 类值得关注的公共事件如表 11.26 所示：

表 11.26: BulletedList 类值得关注的公共事件

| 事件 |  |
| :--- | :--- |
| `Click` | 点击 `BulletedList` 控制中的按钮时发生 |

要选择在 `BulletedList` 控制中显示项目的类型，可以将 `BulletStyle` 属性设置为由 `BulletStyle` 举举定义的符号类型之一。表 11.27 列出了可用的符号样式：

表 11.27: BulletedList 控制的符号样式

| 符号样式 | 说明 |
| :--- | :--- |
| `NotSet` | 表示未指定的符号样式；浏览器自动设置符号列表的样式 |
| `Numbered` | 代表数字形式的符号 |
| `LowerAlpha` | 代表小写字母形式的符号 |
| `UpperAlpha` | 代表大写字母形式的符号 |
| `LowerRoman` | 代表小写罗马数字形式的符号 |
| `UpperRoman` | 代表大写罗马数字形式的符号 |
| `Disc` | 代表实心圆形式的符号 |
| `Circle` | 代表空心圆形式的符号 |
| `Square` | 代表实心方形形式的符号 |
| `CustomImage` | 代表自定义图像形式的符号 |

要指定 `BulletedList` 控制中列表项目的显示行为，可以将 `DisplayMode` 属性设置为 `Text`、`HyperLink` 和 `LinkButton` 之一。

## 控制

### Image 控件

`Image` 控件是在 Web 页面显示图像的 Web 控件。该控件属于 `System.Web.UI.WebControls` 命名空间。图像的统一定位符（URL）在控件的 `ImageUrl` 属性中设置，图像的对齐通过设置 `Align` 属性来指定。`Image` 类的继承层次如下：

```
System.Object
System.Web.UI.Control
System.Web.ui.webcontrols.WebControl
System.web.ui.webcontrols.Image
```

`Image` 类没有非继承的方法或事件。

`Image` 类值得关注的属性如表 11.28 所示：

表 11.28: Image 类值得关注的属性

| 属性 | 说明 |
| :--- | :--- |
| `AlternateText` | 获取或设置在图像不可用时在控件中显示的备用文本。显示工具提示功能，将其作为工具提示显示 |
| `DescriptionUrl` | 获取或设置详细描述的位置 |
| `Enabled` | 获取或设置控件是否可用 |
| `Font` | 获取或设置字体 |
| `GenerateEmptyAlternateText` | 获取或设置是否生成空备用文本 |
| `Align` | 获取或设置与控件的对齐方式 |
| `ImageUrl` | 获取或设置图像的路径 |

### ImageButton 控件

`ImageButton` 是一个显示图像而非文本的控件。该控件存在于 `System.Web.UI.WebControls` 命名空间中。当你需要根据点击图像来触发操作（例如重定向到页面）时，该控件非常有用。`ImageButton` 类的继承层次如下：

```
System.Object
System.Web.UI.Control
System.Web.ui.webcontrols.WebControl
System.web.ui.webcontrols.ImageButton
```

`ImageButton` 类继承自 `Image` 类且没有非继承的方法。`ImageButton` 类值得关注的属性如表 11.29 所示：

表 11.29: ImageButton 类值得关注的属性

| 属性 | 说明 |
| :--- | :--- |
| `CausesValidation` | 获取或设置在点击 `ImageButton` 时是否执行验证 |
| `CommandArgument` | 获取或设置关于命令的参数 |
| `CommandName` | 获取或设置命令的名称 |
| `Enabled` | 获取或设置控件是否可用 |
| `GenerateEmptyAlternateText` | 获取或设置是否生成空备用文本 |

### 深度解析

表 11.29: ImageButton 类值得关注的属性

| 属性 | 说明 |
| :--- | :--- |
| `OnClick` | 获取或设置点击 `ImageButton` 时执行的客户端脚本 |
| `PostBackUrl` | 获取或设置回传页面的 URL |
| `ValidationGroup` | 获取或设置用于回传的控件组 |

`ImageButton` 类值得关注的公共事件如表 11.30 所示：

表 11.30: ImageButton 类值得关注的公共事件

| 事件 |  |
| :--- | :--- |
| `Click` | 点击 `ImageButton` 控制时发生。此事件会导致页面回传 |
| `Command` | 点击 `ImageButton` 控制时触发 |

### ImageMap 控件

图像映射是 Web 页面上的一个图片，它提供了各种链接（热点），根据用户点击的位置导航到其他页面。设计人员经常在网站中使用图像映射。可以使用 `ImageMap` 控件将图像映射包含在 Web 页面中。`ImageMap` 控件存在于 `System.Web.UI.WebControls` 命名空间。图像映射通常是地图，例如你可以显示地图并定义不同的热区域，然后导航到包含相应信息的页面。

`ImageMap` 控件使用 `ImageUrl` 属性指定要显示的图像路径，并使用 `HotSpots` 属性定义 `ImageMap` 类上的热区域。`ImageMap` 类的继承层次如下：

```
System.Object
System.UI.WebControl
  System.UI.WebControls.WebControl
    System.UI.WebControls.Image
      System.UI.WebControls.ImageMap
```

`ImageMap` 类值得关注的公共属性如表 11.31 所示：

表 11.31: ImageMap 类值得关注的公共属性

| 属性 | 说明 |
| :--- | :--- |
| `Enabled` | 获取或设置控件是否可以响应用户交互 |
| `HotSpotMode` | 获取或设置点击热点对象时 `ImageMap` 控制中热点对象的默认行为 |
| `HotSpots` | 获取代表 `ImageMap` 控制中定义的热区域的热点对象集合 |
| `Target` | 获取或设置点击 `ImageMap` 控制时显示 Web 页面内容的窗口 |

`ImageMap` 类值得关注的公共事件如表 11.32 所示：

表 11.32: ImageMap 类值得关注的公共事件

| 事件 |  |
| :--- | :--- |
| `Click` | 点击 `ImageMap` 控制中的热点对象时发生 |

## 表格控件 (Table)

`Table`控件有助于创建表格。当你想要以表格格式显示数据时，此控件非常有用。`Table`控件存在 `System.Web.UI.WebControls` 命名空间中。Web 设计师经常使用表格来在网页中正确放置元素。你可以根据项目需求，在设计时或运行时创建表格。`Table`控件的层次结构如下：

```
System.Object
System.Web.UI.Control
System.Web.UI.WebControls.WebControl
System.Web.UI.WebControls.Table
```

`Table` 类的重要属性如表 11.33 所示：

表 11.33：Table 类的重要公共属性

| 属性 | 描述 |
| --- | --- |
| `BackImageUrl` | 获取或设置在 `Table` 控件底部显示的背景图像 URL |
| `Caption` | 获取或设置在 `Table` 控件的 HTML caption 元素中渲染的文本 |
| `CaptionAlignment` | 获取或设置 `Table` 控件中 HTML caption 元素的水平或垂直位置 |
| `CellPadding` | 获取或设置单元格与单元格边界之间的空间量 |
| `CellSpacing` | 获取或设置单元格之间的空间量 |
| `GridLines` | 获取或设置在 `Table` 控件中显示的网格样式 |
| `HorizontalAlign` | 获取或设置 `Table` 控件在网页上的水平对齐方式 |
| `Rows` | 获取 `Table` 控件中的行集合 |

## 向导控件 (Wizard)

`Wizard`控件是一种带有用户界面（UI）的控件，用于分多个步骤收集数据并提供导航。你可以使用`Wizard`控件实现线性或非线性导航，例如跳过不必要的步骤或返回到之前完成的步骤以更改某些值。`Wizard`控件可以通过样式、模板和皮肤（skins）进行完全自定义；例如，你可以使用 `StartNavigationTemplate`、`FinalNavigationTemplate`、`HeaderTemplate` 和 `StepNavigationTemplate` 来自定义`Wizard`控件的界面。此外，在 ASP.NET 4.5 中，你可以通过创建 `LayoutTemplate` 并在其中插入 `PlaceHolder` 控件来指定渲染`Wizard`控件的方式。

`Wizard` 控件的继承关系如下：

```
System.Object
System.Web.UI.Control
System.Web.UI.WebControls.CompositeControl
System.Web.UI.WebControls.Wizard
```

`Wizard`控件的重要属性如表 11.34 所示：

表 11.34：Wizard 类的重要公共属性

| 属性 | 描述 |
| --- | --- |
| `ActiveStep` | 获取 `Wizardsteps` 中当前显示给最终用户使用的步骤 |
| `ActiveStepIndex` | 获取或设置当前 `WizardStep` 对象的索引值 |
| `CancelButtonImageUrl` | 获取或设置用于取消按钮的图像 URL |
| `CancelButtonStyle` | 获取样式属性集合的引用，该集合描述取消按钮的外观 |
| `CancelButtonText` | 获取或设置用于取消按钮的说明文字 |
| `CancelButtonType` | 获取或设置渲染为取消按钮的按钮类型 |
| `CancelDestinationUrl` | 获取或设置用户点击取消按钮时重定向到的 URL |
| `CellPadding` | 获取或设置单元格数据与单元格边界之间的空间量 |
| `CellSpacing` | 获取或设置单元格之间的空间 |
| `DisplayCancelButton` | 获取或设置布尔值，显示是否显示取消按钮 |
| `DisplaySidebar` | 获取或设置布尔值，显示是否显示右侧侧边栏区域 |
| `FinishCompleteImageUrl` | 获取或设置用于完成按钮的图像 URL |
| `FinishCompleteButtonStyle` | 获取 `Style` 对象的引用，该对象描述完成按钮的设置 |
| `FinishCompleteText` | 获取或设置用于完成按钮的文本 |
| `FinishCompleteType` | 获取或设置渲染为完成按钮的按钮类型 |
| `FinishDestinationUrl` | 获取或设置用户点击完成按钮时重定向到的 URL |
| `NavigationTemplate` | 获取或设置用于在 Finish 步骤显示导航区域的模板 |
| `FinishPreviousImageUrl` | 获取或设置用于 Finish 步骤“上一个”按钮的图像 URL |
| `FinishPreviousButtonStyle` | 获取 `Style` 对象的引用，描述 Finish 步骤中“上一个”按钮的设置 |
| `FinishPreviousText` | 获取或设置用于 Finish 步骤“上一个”按钮的文本 |
| `FinishPreviousButton` | 获取或设置渲染为 Finish 步骤“上一个”按钮的按钮类型 |
| `HeaderStyle` | 获取 `Style` 对象的引用，定义控件头部区域的设置 |
| `HeaderTemplate` | 获取或设置用于显示控件头部区域的模板 |
| `HeaderText` | 获取或设置用于控件头部区域的文本说明文字 |
| `NavigationButtonStyle` | 获取 `Style` 对象的引用，描述控件导航区域中按钮的设置 |
| `NavigationStyle` | 获取 `Style` 对象的引用，描述控件导航区域的设置 |
| `SidebarButtonStyle` | 获取 `Style` 对象的引用，描述侧边栏上按钮的设置 |
| `SidebarStyle` | 获取 `Style` 对象的引用，描述控件侧边栏区域的设置 |
| `SidebarTemplate` | 获取或设置用于显示控件侧边栏区域的模板 |
| `SkipLinkText` | 获取或设置值，用于屏幕阅读器跳过侧边栏的内容 |
| `StartNavigationTemplate` | 获取或设置用于显示 `Wizard` 起始导航区域的模板 |
| `StartNextImageUrl` | 获取或设置用于 Start 步骤“下一步”按钮的图像 URL |
| `StartNextButtonStyle` | 获取 `Style` 对象的引用，描述 Start 步骤中“下一步”按钮的设置 |
| `StartNextText` | 获取或设置用于 Start 步骤“下一步”按钮的说明文字 |
| `StartNextButtonType` | 获取或设置渲染为 Start 步骤“下一步”按钮的按钮类型 |
| `StepNavigationTemplate` | 获取或设置用于除 Finish 或 Complete 步骤以外的 `WizardBase` 派对象导航区域的模板 |
| `StepNextImageUrl` | 获取或设置用于“下一步”按钮的图像 URL |
| `StepNextButtonStyle` | 获取 `Style` 对象的引用，描述“下一步”按钮的设置 |
| `StepNextButtonText` | 获取或设置用于“下一步”按钮的说明文字 |
