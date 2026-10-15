

前面的代码片段还包含了另外两个方法，IsValidHeight() 和 IsValidWidth()。这两个方法是在 BoxHeight 和 BoxWidth 属性需要验证时被调用的验证方法。通常，验证方法是在值被强制转换之后调用的。

现在，你需要注册 Box 类的依赖属性。在这种情况下，依赖属性是在 Box 类的静态构造函数中注册的，如以下代码片段所示：

```
static Box() {
    FrameworkPropertyMetadata myBoxHeightMetadata = new FrameworkPropertyMetadata(5);
    FrameworkPropertyMetadata myBoxWidthMetadata = new FrameworkPropertyMetadata(5);
    FrameworkPropertyMetadata squareBoxMetadata = new FrameworkPropertyMetadata
        (false, FrameworkPropertyMetadataOptions.None, new
        PropertyChangedCallback(IsSquareBoxTrue), new
        CoerceValueCallback(myBoxHeightSquare));
    BoxHeightProperty = DependencyProperty.Register("BoxHeight", typeof(int), typeof(Box),
        myBoxHeightMetadata, new ValidateValueCallback(IsValidHeight));
    BoxWidthProperty = DependencyProperty.Register("BoxWidth", typeof(int), typeof(Box),
        myBoxWidthMetadata, new ValidateValueCallback(IsValidWidth));
    IsSquareProperty = DependencyProperty.Register("IsSquare", typeof(Boolean),
        typeof(Box), squareBoxMetadata);
}
```

在前面的代码片段中，Box 类的静态构造函数包含三个 FrameworkPropertyMetadata 类的对象，用于配置三个依赖属性的元数据。myBoxHeightMetadata 和 myBoxWidthMetadata 对象使用 5 作为 BoxHeight 和 BoxWidth 属性的默认值进行实例化。squareBoxMetadata 对象指定 false 作为默认值，并为 IsSquare 属性指定属性更改和强制值回调方法。

Listing 9.5 中的最后三个语句使用 DependencyProperty 类的 Register() 方法注册 BoxHeight、BoxWidth 和 IsSquare 依赖属性。Register() 方法的第一个参数是依赖属性的实际名称（不带 Property 后缀）。第二个参数是属性值的类型；第三个参数是所有者类型（包含依赖属性的类）；第四个参数是属性元数据对象；第五个参数是 validate value callback() 方法。

现在剩下的唯一事情就是用 CLR 包装器包装依赖属性并实现 get 和 set 访问器。你可以通过在 Box 类中添加以下代码片段来做到这一点：

```
public int BoxHeight
{
    get { return (int)GetValue(BoxHeightProperty); }
    set { SetValue(BoxHeightProperty, value); }
}
public int BoxWidth
{
    get { return (int)GetValue(BoxWidthProperty); }
    set { SetValue(BoxWidthProperty, value); }
}
public Boolean IsSquare
{
    get { return (Boolean)GetValue(IsSquareProperty); }
    set { SetValue(IsSquareProperty, value); }
}
```

在前面的代码片段中，BoxHeight、BoxWidth 和 IsSquare 依赖属性被实现为 CLR 属性，它们的 get 和 set 访问器调用 GetValue() 和 SetValue() 方法。

你现在可以在 XAML 或代码隐藏文件中将这些依赖属性作为 CLR 属性访问。

> NOTE
> 如果你想重置依赖属性的值，那么你可以使用 ClearValue() 方法。使用此方法，依赖属性不一定会变回属性元数据中指定的默认值。事实上，依赖属性回退到的值取决于当时可用的输入。

让我们继续学习一种特定类型的依赖属性，即附加属性。

## Attached Properties

附加属性是指你可以访问并设置给任何子对象或元素的依赖属性。附加属性帮助子元素向父元素提供有关其外观和呈现的信息。元素的附加属性可用于其所有子元素，每个子元素可以为同一个附加属性设置不同的值。

请注意，附加属性是在父或拥有元素中作为依赖属性实现的，并且可以在 XAML 和代码隐藏文件中访问。但是，除了样式触发器中的某些情况外，你不能在 XAML 中检索附加属性的值。与其他依赖属性不同，附加属性不会被包装在 CLR 属性中，因为它们必须可访问所有元素（父元素以及子元素）。这些元素应该能够分配不同的值。附加属性的一些示例包括 Grid 元素的 Row 和 Column 属性。

你也可以创建用户定义的附加属性。为此，父或拥有元素需要继承 DependencyObject 类，除非附加属性仅适用于其他元素而不适用于父元素。声明 DependencyProperty 类型的字段以创建附加属性，然后使用 RegisterAttached() 方法进行注册。你还需要通过两个静态方法实现属性的 get 和 set 访问器。附加属性的 get 访问器方法的语法如下：

```
public static type GetPropertyName (type target) {
    //return statement
}
```

在前面的语法中：
- public, static—表示 C# 关键字。
- type—表示有效类型。
- GetPropertyName—表示实现附加属性的 get 访问器方法的方法名。请注意，GetPropertyName 中的 PropertyName 表示附加属性的实际名称；因此，方法名称根据属性名称而变化。例如，如果附加属性的名称为 Center；那么实现其 get 访问器的静态方法命名为 GetCenter。
- target—表示获取附加属性值的对象或元素。

请注意，附加属性的 get 访问器需要有 return 语句。

附加属性的 set 访问器的语法如下：

```
public static type SetPropertyName( type target, type value) {
    //statements
}
```

在前面的语法中：
- public, static—表示 C# 关键字
- type—表示有效类型
- SetPropertyName—表示实现附加属性的 set 访问器方法的方法名。请注意，SetPropertyName 中的 PropertyName 表示附加属性的实际名称；因此，方法名称根据属性名称而变化。例如，如果附加属性名为 Center，则实现其 set 访问器的静态方法命名为 SetCenter。
- target—表示要设置附加属性的对象或元素。
- value—表示要设置到附加属性上的值。

你可以将附加属性作为子元素的属性访问。当你访问附加属性时，它需要用父或拥有元素的名称限定。考虑一个示例，Grid 元素有一个 Button 元素作为其子元素。那么 Grid 元素的 Row 和 Column 属性是附加属性，可用于 Grid 以及 Button 元素。现在，Button 元素可以访问 Row 和 Column 属性，如以下代码片段所示：

```
<Button Height="25" Width="150" Name="button1" Grid.Row="1" Grid.Column="1">Attached Property</Button>
```

在前面的代码片段中，你可以看到 Row 和 Column 属性是用拥有元素的名称限定或前缀，即 Grid.Row 和 Grid.Column。附加属性的值在双引号内指定，就像在 XAML 中设置其他属性一样。

你也可以通过属性元素语法访问附加属性。例如，Grid 元素的 Row 和 Column 附加属性可在 Button 元素中访问，如以下代码片段所示：

```
<Button>
<Button.Height>25</Button.Height>
<Button.Width>150</Button.Width>
<Button.Name>button1</Button.Name>
<Button.Content>Attached Property</Button.Content>
<Grid.Row>1</Grid.Row>
<Grid.Column>1</Grid.Column>
</Button>
```

在前面的代码片段中，与 Button 元素的其他属性（例如 Height 和 Width）不同，Row 和 Column 属性没有用 Button 元素限定。但是，这两个属性是用 Grid 元素限定的，Grid 元素是附加属性的所有者类型。

与自定义依赖属性类似，你也可以拥有自定义附加属性。创建自定义附加属性的过程与创建依赖属性相同。但是存在某些差异，首先，你使用 RegisterAttached() 方法而不是 Register() 方法来注册自定义附加属性，其次，你不需要将自定义附加属性包装在 CLR 属性中。让我们学习如何创建自定义附加属性。为此，首先创建一个名为 CustomGridAttachedProperty 的独立 WPF 应用程序（也在 CD 上提供）。现在，在应用程序的代码隐藏文件中，在 CustomGridAttachedProperty 命名空间中添加以下代码片段：

```
public class myGrid : UIElement {
public static readonly DependencyProperty CellHeightProperty;
static myGrid() {
CellHeightProperty = DependencyProperty.RegisterAttached("CellHeight",
typeof(int), typeof(myGrid));
}
public static void SetCellHeight(FrameworkElement element, int value) {
element.SetValue(CellHeightProperty, value);
}
public static int GetCellHeight(FrameworkElement element) {
return (int)element.GetValue(CellHeightProperty);
}
}
```

在前面的代码片段中，你可以看到在 CustomGridAttachedProperty 命名空间中添加了一个名为 myGrid 的新类。在 myGrid 类中，声明了一个名为 CellHeightProperty 的静态只读 DependencyProperty 字段。myGrid 类还具有一个静态构造函数，在其中将 CellHeightProperty 依赖属性字段注册为附加属性。为了返回和设置 CellHeight 属性的值，定义了两个方法 GetCellHeight() 和 SetCellHeight()。你现在可以通过用所有者的名称限定它，即 myGrid，来使用 CellHeight 附加属性。

除了属性之外，事件在处理 WPF 应用程序时也起着重要作用。现在，让我们继续学习 WPF 事件。

## WPF Events

在 Windows Forms 应用程序中，你已经使用过事件。你了解到事件如何指示不同操作的发生，以及事件处理程序如何允许你在特定事件发生时控制应用程序的行为。WPF 在事件和事件处理领域有显著的变化或改进。类似

