
你可以创建自定义的附加属性。要做到这一点，所有者父元素需要继承 `DependencyObject` 类，并将附加属性声明为其他元素可用而非父元素本身可用。声明一个 `DependencyProperty` 类型的字段来创建附加属性，然后使用 `RegisterAttached()` 方法进行注册。你还需要通过两个静态方法实现该属性的 getter 和 setter。附加属性 getter 方法的语法如下：

## 深度解析

```csharp
public static type GetPropertyName (type target) {
    //return statement
}
```

在上述语法中：

- `public`, `static`—代表 C# 关键字。
- `type`—代表一个有效类型。
- `GetPropertyName`—代表实现附加属性 getter 访问器的方法名称。注意 `GetPropertyName` 中的 `PropertyName` 代表的是附加属性的实际名称；因此，方法名根据属性的不同而变化。例如，如果附加属性名称为 Center；那么实现其 getter 的静态方法命名为 `Center`。
- `target`—代表获取附加属性值的对象。

注意附加属性的 get 需要一个返回语句。

```csharp
附加属性 setter 访问器的语法如下：
public static type SetPropertyName (type target, type value) {
    //statements
}
```

在上述语法中：

- `public`, `static`—代表 C# 关键字。
- `type`—代表一个有效类型。
- `SetPropertyName`—代表实现附加属性 setter 访问器的方法名称。注意 `SetPropertyName` 中的 `PropertyName` 代表附加属性的实际名称；然而，方法名根据属性的不同而变化。例如，如果属性名为 Center，那么实现其 setter 的静态方法命名为 `SetCenter`。
- `value`—代表要在附加属性上设置的值。

你可以通过当前类的属性来访问附加属性。当你访问附加属性时，它需要用所有者父元素的名称进行限定。考虑一个 Grid 元素包含 Grid 元素的示例。

## 附加属性：创建附加属性

要创建一个附加属性，你使用 `RegisterAttached()` 方法而不是 `Register()` 方法。如列表 8.8 所示：

### 列表 8.8：创建一个附加属性

```csharp
public class CustomGrid : UIElement
{
    public static readonly DependencyProperty CellHeightProperty;
    static CustomGrid()
    {
        CellHeightProperty = DependencyProperty.RegisterAttached("Height", typeof(int), typeof(CustomGrid), null);
    }
    public static void SetHeight(FrameworkElement element, int value)
    {
        element.SetValue(CellHeightProperty, value);
    }
    public static int GetHeight(FrameworkElement element)
    {
        return (int)element.GetValue(CellHeightProperty);
    }
}
```

在列表 8.8 中，你可以看到 `CustomGrid` 添加了一个新成员。在 `myGrid` 中，注册了一个静态只读的 `DependencyProperty` `CellHeightProperty`。`myGrid` 还有一个静态构造函数，在其中注册了 `CellHeightProperty`。

## WPF 事件

## 路由事件

如之前所述，WPF 具有许多元素。这些元素以树的形式表示，包含一个根节点（Window 或 Page）以及根内部的其它元素。嵌套层数没有限制。除了根元素外，所有元素都可以有多个嵌套元素。这些元素中的大多数具有基本功能，例如鼠标和键盘事件。这些事件在 WPF 中被定义为路由事件（routed events）。路由事件与传统的 CLR 事件不同，因为路由事件允许你在多个元素上引发事件。路由事件源于一个元素，但可以沿着元素树向上或向下遍历。随着路由事件的传递，它会在根元素和源元素之间的元素上被处理，并且可以在这些元素中的每一个上被处理。你也可以选择在某个元素上处理路由事件并停止该事件的遍历。

## 深度解析

路由事件（Routed events）属于 WPF 事件系统，并由 `RoutedEvent` 类支持。表 8.14 列出了 `RoutedEvent` 类的一些值得关注的属性。

| 属性 | 描述 |
| --- | --- |
| Name | 获取路由事件的名称 |
| HandlerType | 获取路由事件的句程序类型 |
| OwnerType | 获取最初注册路由事件的所有者类型 |
| RoutingStrategy | 获取路由事件的路由策略 |

由于路由事件是在根元素和源元素之间的路径上触发的，你可以使用路由事件在这些元素之间传递事件信息。事件（以及事件信息）的遍历方向取决于路由事件所使用的路由策略。现在，让我们来看 WPF 路由事件的路由策略。

## 路由策略

在 WPF 中，路由事件根据其路由策略，在元素之间向上或向下导航。路由策略是事件在元素之间被触发和遍历的方式。这些路由策略通过 `RoutingStrategy` 枚举的值来指定。这些值如下：

- 直接事件（Direct events）
- 隧道事件（Tunneling events）
- 冒泡事件（Bubbling events）

让我们逐一学习这些。

## 直接事件

直接事件指的是那些直接应用于其产生或触发的元素上的事件。这些事件与你在 Windows Forms 应用程序中处理过的 CLR 事件类似。这意味着直接事件仅在源元素上触发和处理，而不会通过元素树中的其他元素路由。

## 隧道事件

隧道事件指的是那些源于某个元素，但在根元素或父元素上触发并可能被处理的事件。换句话说，隧道事件从根元素向触发事件的子元素触发，即从外部元素向内部元素触发。隧道事件也被预览事件（preview events），它们的名称以 `Preview` 开头，如代码列表 8.9 所示。

### 代码列表 8.9 隧道事件的遍历

```xml
<xml Class="MyApplication.xaml"
xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MyApplication" Height="300" Width="525">
  <Grid MouseButton PreviewMouseRightButton="MouseEventHandler">
    <Grid>
      <Button Name="button1" Height="25" Width="75" Content="button" Click="Button_Click" />
      <Button Name="button2" Height="25" Width="150" Content="button" MouseButton="MouseEventHandler" />
      <Button Name="button3" Height="25" Width="100" Content="button3" />
    </Grid>
  </Grid>
</xml>
```

## 第 8 章：介绍 Windows Presentation Foundation

`PreviewMouseRightButtonUp="MouseEventHandler"/>`

</xml>

在 8.9 中，你可以看到 `PreviewMouseRightButtonUp` 事件在所有元素中都与其句程序 `MouseClickHandler` 关联。`PreviewMouseRightButtonUp` 事件是一种隧道事件，所有派自 `UIElement` 的元素可用。每当你点击任何元素时，`PreviewMouseRightButtonUp` 事件都会在根元素上发生并向下隧道到源元素。图 8.24 提供了 `PreviewMouseRightButtonUp` 事件遍历的视觉表示：

![](img/17af790174c480761404624aeed9b30b_349_0.png)

冒泡事件指的是在某个元素上发生，并在直到根元素的所有父元素上被触发并可能被处理的事件。换句话说，冒泡事件按照层级顺序从子元素向根元素触发。例如，考虑代码列表 8.10 中的代码：

### 代码列表 8.10: 冒泡事件

```xml
<Window Class="MyApplication.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xml"
Title="MainWindow" Height="320" Width="525"
MouseRightButtonUp="MouseEventHandler">
<Grid Name="grid1" MouseRightButtonUp="MouseEventHandler">
<Button Name="button1" Height="25" Content="Button"
Margin="10,10,0,0"
MouseRightButtonUp="MouseEventHandler"/>
<Button Name="button2" Height="25" Width="150" Margin="0,0,0,0"
MouseRightButtonUp="MouseEventHandler"/>
<Grid Name="grid2" Height="100" Width="100"
MouseRightButtonUp="MouseEventHandler">
<TextBox Name="textBox1" Text="textBox" Height="25" Margin="0,0,45,60"
MouseRightButtonUp="MouseEventHandler"/>
<TextBox Name="textBox2" Text="textBox" Height="25" Margin="45,60,0,0"
MouseRightButtonUp="MouseEventHandler"/>
</Grid>
</Grid>
</Window>
```

```xml
<MouseButton Name="button" Height="25" Content="button3" Margin="100,220,100,10">
MouseRightButtonUp="MouseRightEventHandler" />
</Grid>
<Window>
```

在代码列表 8.10 中，你可以看到 `MouseRightButtonUp` 事件在所有元素中都与其句程序 `MouseRightEventHandler` 关联。`MouseRightButtonUp` 事件是一种冒泡路由事件，所有派自 `UIElement` 类的元素可用。当你点击任何元素时，事件会在源元素上触发并遍历到根元素。图 8.25 显示了当事件最初在文本框元素上触发时，遍历情况：

![](img/17af790174c480761404624aeed9b30b_350_0.png)

图 8.25：`MouseRightButtonUp` 路由事件的遍历

## 路由事件的句程序

正如你所学的，路由事件遍历元素树。它们在源元素到根元素（或反之）的每个元素级别上被触发和处理。WPF 提供了系列路由事件。定义事件句程序的语法在后台代码文件中所示：

```csharp
void handlerName(object sender, RoutedEventArgs e) {
    // 逻辑
}
```

- `sender`：代表触发事件的对象。
- `e`：代表事件数据。
- `handlerName`：处理事件的方法名称。

...以将句程序与事件关联。例如，`Click` 事件是一个附加事件，它属于

# 深入探讨

通过 `Button` 类，并被其派生类和元素继承，例如 `Button` 和 `ToggleButton` 类。"grid" 请考虑以下代码片段

```xml
<Grid Name="grid">
  <Button Click="button_click"
        Height="25" Name="button1" VerticalAlignment="Top"
        Margin="0,30,0,0"></Button>
  <ToggleButton Height="25" Name="ToggleButton"
        VerticalAlignment="Center"></ToggleButton>
  <Button Height="25" Name="button2" VerticalAlignment="Bottom"
        Margin="0,30,0,0"></Button>
</Grid>
```

在上述代码片段中，`Click` 事件与 `Grid` 元素关联，该元素是名为 `button1` 的元素以及一个名为 `toggleButton` 的 `ToggleButton` 的元素。

注意，`Grid` 中的 `Click` 事件是通过将事件属性（`Click`）限定拥有该事件的类名（`ButtonBase`）来指定的。`Grid` 中的名称和事件之间通过点 `.` 隔开。当任何按钮或切换按钮被点击时，就会调用事件处理程序。事实上，如果将任何派自 `ButtonBase` 类的元素添加到网格中并点击其中任何一个，事件将以这种方式处理。你可以为子元素设置一个公共处理程序。注意，`Grid` 元素并没有定义 `Click` 事件，它代表它处理其子元素的 `Click` 事件。

事件在功能上通过 `RegisteredEvent` 类的实例抛出。在本版本中，事件通过 `RegisteredEvent` 方法进行注册。然而，附加事件（attached events）不具有 CLR 事件，而是使用公共静态方法来添加和删除事件处理程序。为附加事件添加处理程序的静态方法语法如下：

```csharp
public static void addAttachedEventHandler(EventHandler handler)
{
    // add event handler logic
}
```
