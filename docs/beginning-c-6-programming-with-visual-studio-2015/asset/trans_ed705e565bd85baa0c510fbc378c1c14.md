
```
public static DependencyProperty MyStringProperty =
DependencyProperty.Register(
"MyString",
typeof(string),
typeof(MyClass),
new FrameworkPropertyMetadata("Default value"));
```

到目前为止，你已经了解了三种可以指定的回调方法，分别用于属性更改通知、属性强制转换和属性值验证。与依赖属性本身一样，这些回调都必须实现为公共静态方法。每个回调都有特定的返回类型和参数列表，你必须在回调方法中使用。

现在让我们回到正轨，继续开发 Karli Cards 的游戏客户端。在下面的“试一试”中，你将创建一个用户控件，用于在应用程序中表示一张扑克牌。

## 试一试 用户控件：KarliCards Gui.CardControl.xaml

返回到上一个“试一试”中的 KarliCards Gui 项目。

- 1. 本示例使用你在第13章创建的 CardLib 项目，因此必须将其添加到解决方案中。首先在“解决方案资源管理器”中右键单击解决方案名称，选择“添加现有项目”，浏览并选择第13章代码示例中的 `Ch13CardLib.csproj` 文件。
- 2. 在 KarliCards Gui 项目中右键单击“引用”，选择“添加引用”，以添加对 Ch13CardLib 项目的引用。在左侧树中单击“项目”下的“解决方案”，选择 Ch13CardLib，单击“确定”。
- 3. 向 KarliCards Gui 项目添加一个名为 `CardControl` 的新用户控件，并修改 `CardControl.xaml` 中的代码如下：

```
<UserControl x:Class="KarliCards_Gui.CardControl"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:local="clr-namespace:KarliCards_Gui"
mc:Ignorable="d"
Height="154" Width="100" Name ="UserControl">
<UserControl.Resources>
<local:RankNameConverter x:Key="rankConverter"/>
<DataTemplate x:Key="SuitTemplate">
<TextBlock Text="{Binding}"/>
</DataTemplate>
<Style TargetType="Image" x:Key="SuitImage">
<Style.Triggers>
<DataTrigger Binding="{Binding ElementName=UserControl, Path=Suit}" Value="Club">
<Setter Property="Source" Value="Images/Clubs.png" />
</DataTrigger>
<DataTrigger Binding="{Binding ElementName=UserControl, Path=Suit}" Value="Heart">
<Setter Property="Source" Value="Images/Hearts.png" />
</DataTrigger>
```

```
</Image>
<Path Fill="#FFFFFFFF" Stretch="Fill" Stroke="{x:Null}"
Margin="0,0,35.218,-0.077" Data="F1 M10.5,51 L145.16457,51 C116.5986,
76.731148 115.63518,132.69684 121.63533,149.34013 133.45299,
182.120218 152.15821,195.69803 161.79765,200.07669 L110.5,200 C103.59644,
200 98.194,187.5 98,187.5 L98,63.5 C98,56.596439 103.59644,51 110.5,51 z">
<Path.OpacityMask>
<LinearGradientBrush EndPoint="0.957,1.127" StartPoint="0,-0.06">
<GradientStop Color="#FF000000" Offset="0"/>
<GradientStop Color="#00FFFFFF" Offset="1"/>
</LinearGradientBrush>
</Path.OpacityMask>
</Path>
</Grid>
</UserControl>
```

### 4. 向类添加三个依赖属性：

```
public static DependencyProperty SuitProperty = DependencyProperty.Register(
"Suit",
typeof(Ch13CardLib.Suit),
typeof(CardControl),
new PropertyMetadata(Ch13CardLib.Suit.Club,
new PropertyChangedCallback(OnSuitChanged)));
public static DependencyProperty RankProperty = DependencyProperty.Register(
"Rank",
typeof(Ch13CardLib.Rank),
typeof(CardControl),
new PropertyMetadata(Ch13CardLib.Rank.Ace));
public static DependencyProperty IsFaceUpProperty = DependencyProperty.Register(
"IsFaceUp",
typeof(bool),
typeof(CardControl),
new PropertyMetadata(true, new PropertyChangedCallback(OnIsFaceUpChanged)));
public bool IsFaceUp
{
 get { return (bool)GetValue(IsFaceUpProperty); }
 set { SetValue(IsFaceUpProperty, value); }
}
public Ch13CardLib.Suit Suit
{
 get { return (Ch13CardLib.Suit)GetValue(SuitProperty); }
 set { SetValue(SuitProperty, value); }
}
public Ch13CardLib.Rank Rank
{
 get { return (Ch13CardLib.Rank)GetValue(RankProperty); }
 set { SetValue(RankProperty, value); }
}
```

### 5. 向类添加更改事件处理程序：

```
public static void OnSuitChanged(DependencyObject source,
 DependencyPropertyChangedEventArgs args)
{
var control = source as CardControl;
control.SetTextColor();
}
private static void OnIsFaceUpChanged(DependencyObject source,
    DependencyPropertyChangedEventArgs args)
{
    var control = source as CardControl;
    control.RankLabel.Visibility = control.SuitLabel.Visibility =
        control.RankLabelInverted.Visibility =
        control.TopRightImage.Visibility =
        control.BottomLeftImage.Visibility = control.IsFaceUp ?
        Visibility.Visible : Visibility.Hidden;
}
```

### 6. 向类添加一个属性：

```
private Ch13CardLib.Card _card;
public Ch13CardLib.Card Card
{
    get { return _card; }
    private set { _card = value; Suit = _card.suit; Rank = _card.rank; }
}
```

### 7. 添加一个用于设置文本颜色的辅助方法，并重载构造函数以接收一个 Card 对象：

```
public CardControl(Ch13CardLib.Card card)
{
    InitializeComponent();
    Card = card;
}
private void SetTextColor()
{
    var color = (Suit == Ch13CardLib.Suit.Club || Suit == Ch13CardLib.Suit.Spade) ?
        new SolidColorBrush(Color.FromRgb(0, 0, 0)) :
        new SolidColorBrush(Color.FromRgb(255, 0, 0));
    RankLabel.Foreground = SuitLabel.Foreground = RankLabelInverted.Foreground =
        color;
}
```

### 8. 通过在项目中添加新类来添加新的值转换器。将其命名为 `RankNameConverter.cs` 并添加以下代码：

```
using System;
using System.Windows;
using System.Windows.Data;
namespace KarliCards_Gui
{
    [ValueConversion(typeof(Ch13CardLib.Rank), typeof(string))]
    public class RankNameConverter : IValueConverter
    {
        public object Convert(object value, Type targetType,
            object parameter, System.Globalization.CultureInfo culture)
        {
int source = (int)value;
if (source == 1 || source > 10)
{
    switch (source)
    {
        case 1:
            return "Ace";
        case 11:
            return "Jack";
        case 12:
            return "Queen";
        case 13:
            return "King";
        default:
            return DependencyProperty.UnsetValue;
    }
}
else
    return source.ToString();
}
public object ConvertBack(object value, Type targetType, object parameter, System.Globalization.CultureInfo culture)
{
    return DependencyProperty.UnsetValue;
}
}
```

### 9. 转到 `GameClient.xaml.cs` 代码隐藏文件，如下修改构造函数：

```
public GameClient()
{
    InitializeComponent();
    var position = new Point(15, 15);
    for (var i = 0; i < 4; i++)
    {
        var suit = (Ch13CardLib.Suit)i;
        position.Y = 15;
        for (int rank = 1; rank < 14; rank++)
        {
            position.Y += 30;
            var card = new CardControl(new Ch13CardLib.Card((Ch13CardLib.Suit)suit, (Ch13CardLib.Rank)rank));
            card.VerticalAlignment = VerticalAlignment.Top;
            card.HorizontalAlignment = HorizontalAlignment.Left;
            card.Margin = new Thickness(position.X, position.Y, 0, 0);
            contentGrid.Children.Add(card);
        }
        position.X += 112;
    }
}
```

### 10. 运行应用程序。结果如图15-3所示。

稍后你将查看这些属性的实现。现在只需知道它们是来自你在第10章开始构建的 CardLib 项目中的枚举。

这三个标签显示扑克牌的点数和花色。尽管它们绑定到不同的属性，但有许多共同之处。它们必须根据绑定属性的值以红色或黑色显示文本。在本示例中，颜色是在 Rank 更改时引发的事件中设置的，但你也可以使用触发器来实现：

```
<Label x:Name="SuitLabel"
Content="{Binding Path=Suit, ElementName=UserControl, Mode=Default}"
ContentTemplate="{DynamicResource SuitTemplate}" HorizontalAlignment="Center"
VerticalAlignment="Center" Margin="8,51,8,60" />
```

绑定属性值时，还可以通过数据模板指定如何呈现绑定内容。在本示例中，数据模板是 `SuitTemplate`，作为动态资源引用（尽管在这种情况下，静态资源绑定也完全可以）。此模板在用户控件的资源部分定义如下：

```
<UserControl.Resources>
    <DataTemplate x:Key="SuitTemplate">
        <TextBlock Text="{Binding}"/>
    </DataTemplate>
</UserControl.Resources>
```

因此，Suit 的字符串值被用作 TextBlock 控件的 Text 属性。同样的 DataTemplate 定义也复用于两个点数标签。Suit 是一个枚举，枚举中值的名称会自动转换为字符串，显示在 Text 属性中。

两个点数标签在绑定中包含一个值转换器。

```
<Label x:Name="RankLabel" Grid.ZIndex="1"
Content="{Binding Path=Rank, ElementName=UserControl, Mode=Default,
Converter={StaticResource ResourceKey=rankConverter}}"
ContentTemplate="{DynamicResource SuitTemplate}"
HorizontalAlignment="Left" VerticalAlignment="Top"
Margin="8,8,0,0" />
```

该转换器通过以下声明包含在 UserControl 资源中：

<local:RankNameConverter x:Key="rankConverter"/>

如果移除值转换器，控件仍然可以正常工作。你会看到 Ace、2、3、4 等。你还会看到枚举值的名称被转换为字符串——Ace、Deuce、Three、Four 等。虽然这在技术上是正确的，但看起来不太合适，因此你将值转换为数字和字符串的组合。

最后要注意的是 RankLabel 上的 `Grid.ZIndex="1"` 属性赋值。控件在 Grid 或 Canvas 上的 ZIndex 决定了保存该控件的可视层。如果两个或多个控件占据相同空间，则可以使用 ZIndex 将其中一个强制移到前面。通常所有控件的 ZIndex 都为 0，因此将单个控件设置为 1 意味着它被移到前面。这是必要的，因为路径的模糊效果原本会遮挡文本。
