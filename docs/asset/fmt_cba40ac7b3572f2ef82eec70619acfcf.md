
## HyperLink 控件

您可以通过在当前页面上指定其 URL 来指定链接页面的位置。您可以在`HyperLink`控件中使用文本以及图像。文本通过`Text`属性指定，图像通过`ImageUrl`属性指定。默认情况下，当您单击`HyperLink`控件时，超链接内容会显示在新的浏览器窗口中。您可以将`Target`属性设置为窗口或框架的名称，如表 14.11 所列：

**表 14.11：`HyperLink`类的`Target`属性选项**

| Property | Description |
| --- | --- |
| `_blank` | 在没有框架的新窗口中显示超链接内容 |
| `_parent` | 在直接的框架集父级中显示超链接内容 |
| `_self` | 在焦点所在的框架中显示超链接内容 |
| `_top` | 在没有框架的完整窗口中显示超链接内容 |

`HyperLink`类没有非继承的方法或事件。`HyperLink`类值得注意的公共属性在表 14.12 中列出：

**表 14.12：`HyperLink`类值得注意的公共属性**

| Property | Description |
| --- | --- |
| `ImageUrl` | 获取要为`HyperLink`控件显示的图像的路径 |
| `NavigateUrl` | 获取当单击`HyperLink`控件时要链接到的 Web 页面的 URL |
| `Target` | 获取当单击`HyperLink`控件时显示 Web 页面数据的目标窗口 |
| `Text` | 获取`HyperLink`控件的文本标题 |

## HiddenField 控件

`HiddenField`控件用于存储需要在向服务器的回发中保持持久的值。通常，使用视图状态、会话状态和 cookie 来维护 Web 页面的状态。如果这些方法被禁用或不可用，您可以使用`HiddenField`控件来存储状态值。`HiddenField`类的类层次结构如下：

```
System.Object

System.Web.UI.Control

System.Web.UI.WebControls.HiddenField
```

**表 14.13：`HiddenField`类值得注意的公共属性**

| Property | Description |
| --- | --- |
| `EnableTheming` | 获取或设置一个值，指示主题是否应用于`HiddenField`控件 |
| `SkinID` | 获取或设置要应用于`HiddenField`控件的皮肤 |
| `Value` | 获取或设置隐藏字段的值 |

## FileUpload 控件

`FileUpload`控件显示一个文本框和一个浏览按钮，使您能够从本地或远程机器浏览文件以将其上传到 Web 服务器。您可以通过在此控件的文本框中指定要上传文件的完整路径（例如，`D:\MyFiles\Test.txt`）来将文件上传到 Web 服务器。或者，您可以单击浏览按钮，然后在选择文件对话框中定位文件。`FileUpload`类的类层次结构如下：

```
System.Object

  System.Web.UI.Control

    System.Web.UI.WebControls.WebControl

      System.Web.UI.WebControls.FileUpload
```

**表 14.14：`FileUpload`类值得注意的公共属性**

| Property | Description |
| --- | --- |
| `FileBytes` | 获取使用`FileUpload`控件指定的文件的字节数组 |
| `FileContent` | 获取指向使用`FileUpload`控件上传的文件的`Stream`对象 |
| `FileName` | 获取要在客户端上传的文件的名称 |
| `HasFile` | 获取一个值，指示`FileUpload`控件是否包含文件 |
| `PostedFile` | 获取使用`FileUpload`控件上传的文件的底层`HttpPostedFile`对象 |

**表 14.15：`FileUpload`类值得注意的公共方法**

| Method | Description |
| --- | --- |
| `SaveAs()` | 将上传文件的数据保存到 Web 服务器上的指定路径 |

## CheckBox 控件

`CheckBox`控件创建可通过单击选择的复选框。此控件存在于`System.Web.UI.WebControls`命名空间中。`CheckBox`控件显示复选标记，允许用户在`True`或`False`之间切换。`CheckBox`类的类层次结构如下：

```
System.Object

  System.Web.UI.Control

    System.Web.UI.WebControls.WebControl

      System.Web.UI.WebControls.CheckBox
```

**表 14.16：`CheckBox`类值得注意的公共属性**

| Property | Description |
| --- | --- |
| `AutoPostBack` | 获取一个值，显示`CheckBox`状态在单击时是否自动回发到服务器 |
| `CausesValidation` | 获取或设置一个布尔值，显示在单击`CheckBox`控件时是否执行验证 |
| `Checked` | 获取一个值，显示`CheckBox`控件是否被选中 |
| `InputAttributes` | 获取`CheckBox`控件所有渲染的`input`元素的属性集合的引用 |
| `LabelAttributes` | 获取`CheckBox`控件所有渲染的`LABEL`元素的属性集合的引用 |
| `Text` | 获取与`CheckBox`控件关联的文本标签 |
| `TextAlign` | 获取与`CheckBox`控件关联的文本标签的放置位置 |
| `ValidationGroup` | 获取或设置`CheckBox`控件在其回发时将触发验证的控件组 |

**表 14.17：`CheckBox`类值得注意的公共事件**

| Event | Description |
| --- | --- |
| `CheckedChanged` | 当`Checked`属性的值在向服务器的多次发布之间发生变化时发生 |

## CheckBoxList 控件

你可以使用`CheckBoxList`控件一次显示多个复选框作为一列复选框。`CheckBoxList`控件存在于`System.Web.UI.WebControls`命名空间中。当你想将数据源的数据绑定到复选框时，此控件通常很有用。`CheckBoxList`控件通过将这些控件绑定到数据源，在运行时创建多选复选框组。`CheckBoxList`类的继承层次结构如下：

```
System.Object

  System.Web.UI.Control

    System.Web.UI.WebControls.WebControl

      System.Web.UI.WebControls.BaseDataBoundControl

        System.Web.UI.WebControls.DataBoundControl

          System.Web.UI.WebControls.ListControl

            System.Web.UI.WebControls.CheckBoxList
```

**表 14.18：`CheckBoxList`类值得注意的公共属性**

| Property | Description |
| --- | --- |
| `CellPadding` | 获取单元格边框与数据之间的距离，以像素为单位 |
| `CellSpacing` | 获取单元格之间的距离，以像素为单位 |
| `RepeatColumns` | 获取在`CheckBoxList`控件中显示的列数 |
| `RepeatDirection` | 获取一个值，指示控件是垂直还是水平显示 |
| `RepeatLayout` | 获取复选框的布局 |
| `TextAlign` | 获取组内复选框的文本放置位置 |

## RadioButton 控件

与`CheckBox`控件类似，`RadioButton`控件创建一个单选按钮。`RadioButton`控件存在于`System.Web.UI.WebControls`命名空间中。`RadioButton`控件可以分组，其中一次只能选择一个`RadioButton`控件。在 Web Forms 中，你必须将`RadioButton`的`GroupName`属性设置为相同的值以将它们关联到一个组。`RadioButton`类的层次结构如下：

```
System.Object

    System.Web.UI.Control

        System.Web.UI.WebControls.WebControl

            System.Web.UI.WebControls.CheckBox

                System.Web.UI.WebControls.RadioButton
```

**表 14.19：`RadioButton`类值得注意的公共属性**

| Property | Description |
| --- | --- |
| `GroupName` | 获取单选按钮所属组的名称 |

## RadioButtonList 控件

`RadioButtonList`控件将数据显示为一列单选按钮，并为你在单选按钮组中显示单选提供了一种简便的方法。`RadioButtonList`控件存在于`System.Web.UI.WebControls`命名空间中。此控件的一个有用方面是，单选按钮列表可以通过数据绑定在运行时生成。要确定`RadioButton`控件中选中的项，你可以测试列表的`SelectedItem`属性。你也可以使用`SelectedIndex`属性确定选中项的索引。`RadioButtonList`类的继承层次结构如下：

```
System.Object

    System.Web.UI.Control

        System.Web.UI.WebControls.WebControl

            System.Web.UI.WebControls.BaseDataBoundControl

                System.Web.UI.WebControls.DataBoundControl

                    System.Web.UI.WebControls.ListControl

                        System.Web.UI.WebControls.RadioButtonList
```

**表 14.20：`RadioButtonList`类值得注意的公共属性**

| Property | Description |
| --- | --- |
| `CellPadding` | 获取或设置表格单元格边框与内容之间的距离，以像素为单位 |
| `CellSpacing` | 获取或设置表格单元格与单选按钮之间的距离，以像素为单位 |
| `RepeatColumns` | 获取或设置在`RadioButtonList`控件中显示的列数 |
| `RepeatDirection` | 获取或设置组内单选按钮的显示方向 |
| `RepeatLayout` | 获取或设置组内单选按钮的布局 |
| `TextAlign` | 获取或设置单选按钮标题的文本对齐方式 |

> **NOTE**
>
> 在 ASP.NET 4.0 中，`RadioButtonList`和`CheckBoxList`控件已得到改进。在之前的 ASP.NET 版本中，你可以通过为`RepeatLayout`属性指定以下两个值之一来指定控件的布局：
>
> - `Table`: 指定项目以表格结构显示。
> - `Flow`: 指定项目不以表格结构显示。标记代码由`span`元素组成，各个项目由`br`元素分隔。
>
> 现在，在 ASP.NET 4.0 中，可以为`RepeatLayout`属性指定两个新值：
>
> - `UnorderedList`: 指定项目不以表格结构显示。标记代码由包含`li`元素的`ul`元素组成。
> - `OrderedList`: 指定项目不以表格结构显示。标记代码由包含`li`元素的`ol`元素组成。
>
> 你应该注意，如果将`RepeatLayout`属性设置为`OrderedList`或`UnorderedList`，则不能使用`RepeatDirection`属性。如果在这种情况下设置`RepeatDirection`属性，它将在运行时抛出异常。
>
> 你将在本章的 Immediate Solutions 部分学习新`RepeatDirection`属性值的使用。

## ListBox 控件

`ListBox`控件是标准 Web 服务器控件，用于在 Web 页面上运行时从项目列表中选择一个或多个项目。`ListBox`类的继承层次结构为：

```
System.Object

  System.Web.UI.Control

    System.Web.UI.WebControls.WebControl

      System.Web.UI.WebControls.BaseDataBoundControl

        System.Web.UI.WebControls.DataBoundControl

          System.Web.UI.WebControls.ListControl

            System.Web.UI.WebControls.ListBox
```

你可以使用`ListBox`控件的`Rows`属性指定控件的高度。要启用多项选择，你可以将`SelectionMode`属性设置为`ListSelectionMode.Multiple`。你可以在单选`ListBox`控件中借助`SelectedItem`和`SelectedIndex`属性找到选中的项目。`SelectedItem`属性以`ListItem`对象形式返回选中的项目，该对象支持`Text`、`Value`和`Selected`属性。在多选`ListBox`控件中（这意味着我们从单个`ListBox`控件中选择多个项目），循环遍历`ListBox`控件中的选中项目，并使用`SelectedIndex`属性将每个选中项目作为`ListItem`对象返回。

`ListBox`类继承`ListControl`类；此外，它没有任何非继承事件。`ListControl`类也没有任何非继承方法。请注意，`ListControl`类的`Items`属性返回一个`ListItem`对象集合，你可以使用它访问`ListBox`中的项目。`ListBox`类值得注意的公共属性在表 14.21 中列出：

**表 14.21：`ListBox`类值得注意的公共属性**

| Property | Description |
| --- | --- |
| `BorderColor` | 获取或设置控件的边框颜色 |
| `BorderStyle` | 获取或设置控件的边框样式 |
| `BorderWidth` | 获取或设置控件的边框宽度 |
| `Rows` | 获取或设置`ListBox`控件中显示的行数 |
| `SelectionMode` | 获取或设置`ListBox`控件的选择模式 |

## DropDownList 控件

`DropDownList`控件将数据列表显示为下拉列表，你可以从中进行单选。`DropDownList`控件存在于`System.Web.UI.WebControls`命名空间中。你不能在此控件中选择多个项目，因为当你从列表中进行选择时，列表会自动关闭。`DropDownList`类的继承层次结构如下：

```
System.Object

  System.Web.UI.Control

    System.Web.UI.WebControls.WebControl

      System.Web.UI.WebControls.BaseDataBoundControl

        System.Web.UI.WebControls.DataBoundControl

          System.Web.UI.WebControls.ListControl

            System.Web.UI.WebControls.DropDownList
```

