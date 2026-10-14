
此文件定义了`Customers`命名空间中的类型。页面由名为`MainPage`的类实现，它继承自`Page`类。`Page`类实现了 UWP 应用的 XAML 页面的默认功能，因此您只需在`MainPage`类中编写定义应用特定逻辑的代码即可。

1. 返回“设计视图”窗口中的`MainPage.xaml`文件。如果您查看页面的 XAML 标记，您会注意到`<Page>`标签包含以下属性：

```
x:Class="Customers.MainPage"
```

此属性将定义页面布局的 XAML 标记与提供页面逻辑的`MainPage`类连接起来。

这就是简单 UWP 应用的基本管道。当然，使图形应用有价值的是它向用户呈现信息的方式。这并不总是看起来那么简单。设计一个有吸引力且易于使用的图形界面需要专业技能，并非所有开发人员都具备（我知道，因为我自己也不具备）。然而，许多拥有这些技能的平面设计师并不是程序员，因此尽管他们可能能够设计出精彩的用户界面，但可能无法实现使其有用的逻辑。幸运的是，Visual Studio 2015 使您可以将用户界面设计与业务逻辑分离，以便平面设计师和开发人员可以合作构建一个外观很酷且运行良好的应用。开发人员所要做的就是专注于应用的基本布局，让平面设计师提供样式。

## Implementing a scalable user interface

为 UWP 应用布局用户界面的关键是了解如何使其缩放并适应用户可能运行应用的设备的不同形态因素。在以下练习中，您将研究如何实现这种缩放。

## Lay out the page for the Customers app

1. 在“设计视图”窗口顶部的工具栏中，注意可让您选择设计表面分辨率和形态因素的下拉列表框，以及可让您为支持旋转的设备（平板电脑和手机支持；台式机不支持）选择方向（纵向或横向）的一对按钮。其目的是您可以快速查看用户界面在不同设备上的外观。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_709_0.png)

默认布局为纵向的 5 英寸智能手机。在下拉列表框中，选择 13.3" Desktop (1280 x 720) 100% scale。请注意，此形态因素默认为横向方向。

2. 查看`MainPage`页面的 XAML 标记。

页面包含一个`Grid`控件：

Click here to view code image

```
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

</Grid>
```

### Note

不必担心`Grid`控件的`Background`属性的指定方式。这是使用样式的示例，您将在本章后面学习如何使用样式。

理解`Grid`控件的工作原理对于构建可缩放和灵活的用户界面至关重要。`Page`元素只能包含一个 single item, and if you want, you can replace the `Grid` control with a `Button`, as shown in the example that follows:

### Note

Don’t type the following code. It is shown for illustrative purposes only.

Click here to view code image

```
<Page

    ...

    <Button Content="Click Me"/>

</Page>
```

However, the resulting app is probably not very useful—a form that contains a button and that displays nothing else is unlikely to win an award as the world’s greatest app. If you attempt to add a second control, such as a `TextBox`, to the page, your code will not compile and the errors shown in the following image will occur:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_710_0.png)

The purpose of the `Grid` control is to facilitate adding multiple items to a page. The `Grid` control is an example of a container control; it can contain a number of other controls, and you can specify the position of these other controls within the grid. Other container controls are also available. For example, the `StackPanel` control automatically places the controls it contains in a vertical arrangement, with each control positioned directly below its immediate predecessor.

In this app, you will use a `Grid` to hold the controls necessary for a user to be able to enter and view data for a customer.

3. Add a `TextBlock` control to the page, either by dragging it from the Toolbox or by typing the text `<TextBlock />` directly into the XAML pane, on the blank line after the opening `<Grid>` tag, like this:

Click here to view code image

```
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <TextBlock />

</Grid>
```

### Tip

if the Toolbox does not appear, click Toolbox on the View menu, and it should be displayed in the toolbar to the left. Also, note that you can type the code for a control directly into the XAML window for a page; you do not have to drag controls from the Toolbox.

4. This `TextBlock` provides the title for the page. Set the properties of the `TextBlock` control by using the values in the following table:

| Property | Value |
|---|---|
| `HorizontalAlignment` | `Left` |
| `Margin` | `400,90,0,0` |
| `TextWrapping` | `Wrap` |
| `Text` | Adventure Works Customers |
| `VerticalAlignment` | `Top` |
| `FontSize` | `50` |

You can set these properties by using the Properties window or by typing the equivalent XAML markup into the XAML window, as shown here in bold:

Click here to view code image

```
<TextBlock HorizontalAlignment="Left" Margin="400,90,0,0" TextWrapping="Wrap" Text="Adventure Works Customers" VerticalAlignment="Top"
FontSize="50"/>
```

The resulting text should appear in the Design View window, like this:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_712_0.png)

Notice that when you drag a control from the Toolbox to a form, connectors appear that specify the distance of two of the sides of the control from the edge of the container control in which it is placed. In the preceding example, these connectors for the `TextBlock` control are labeled with the values 400 (from the left edge of the grid) and 90 (from the top edge of the grid). At run time, if the `Grid` control is resized, the `TextBlock` will move to retain these distances, which in this case might cause the distance of the `TextBlock` in pixels from the right and bottom edges of the `Grid` to change. You can specify the edge or edges to which a control is anchored by setting the `HorizontalAlignment` and `VerticalAlignment` properties. The `Margin` property specifies the distance from the anchored edges. Again, in this example, the `HorizontalAlignment` property of the `TextBlock` is set to `Left` and the `VerticalAlignment` property is set to `Top`, which is why the control is anchored to the left and top edges of the grid. The `Margin` property contains four values that specify the distance of the left, top, right, and bottom sides (in that order) of the control from the corresponding edge of the container. If one side of a control is not anchored to an edge of the container, you can set the corresponding value in the `Margin` property to 0.

5. Add four more `TextBlock` controls to the page. These `TextBlock` controls are labels that help the user identify the data that is displayed on the page. Use the values in the following table to set the properties of these controls:

| Control | Property | Value |
|---|---|---|
| First Label | `HorizontalAlignment` | `Left` |
|  | `Margin` | `330,190,0,0` |
|  | `TextWrapping` | `Wrap` |
|  | `Text` | `ID` |
|  | `VerticalAlignment` | `Top` |
|  | `FontSize` | `20` |
| Second Label | `HorizontalAlignment` | `Left` |
|  | `Margin` | `460,190,0,0` |
|  | `TextWrapping` | `Wrap` |
|  | `Text` | `Title` |
|  | `VerticalAlignment` | `Top` |
|  | `FontSize` | `20` |
| Third Label | `HorizontalAlignment` | `Left` |
|  | `Margin` | `620,190,0,0` |
|  | `TextWrapping` | `Wrap` |
|  | `Text` | `First Name` |
|  | `VerticalAlignment` | `Top` |
|  | `FontSize` | `20` |
| Fourth Label | `HorizontalAlignment` | `Left` |
|  | `Margin` | `975,190,0,0` |
|  | `TextWrapping` | `Wrap` |
|  | `Text` | `Last Name` |
|  | `VerticalAlignment` | `Top` |
|  | `FontSize` | `20` |

As before, you can either drag the controls from the Toolbox and use the Properties window to set their properties, or you can type the following XAML markup into the XAML pane, after the existing `TextBlock` control and before the closing `</Grid>` tag:

Click here to view code image

```
<TextBlock HorizontalAlignment="Left" Margin="330,190,0,0" TextWrapping="Wrap" Text="ID" VerticalAlignment="Top" FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="460,190,0,0" TextWrapping="Wrap" Text="Title" VerticalAlignment="Top" FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="620,190,0,0" TextWrapping="Wrap" Text="First Name" VerticalAlignment="Top" FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="975,190,0,0" TextWrapping="Wrap" Text="Last Name" VerticalAlignment="Top" FontSize="20"/>
```
