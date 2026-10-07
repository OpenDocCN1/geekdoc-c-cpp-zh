

# 空间控件 | 89

```xml
<FontSize="12">superscripts</Run>
and <Run BaselineAlignment="Subscript">
<FontSize="12">superscripts</Run>
<LineBreak/>
<Run Foreground="Red" FontWeight="Bold">
<Run.Background>
<LinearGradientBrush>
<GradientStop Offset="0" Color="White"/>
<GradientStop Offset="1" Color="Orange"/>
</LinearGradientBrush>
</Run.Background>
你可以为 Run 赋予不同的文本属性，例如
前景色颜色和背景颜色。
</Run>
</TextBlock>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_126_0.png)

# 提示框 (ToolTip)

ToolTip 为另一个对象显示工具提示框。图 5-13 显示了一个程序为位于鼠标下的“First Name”（名字）文本框显示工具提示框。

虽然你可以通过构建 ToolTip 对象来提供控件工具提示，但更简单的方法是像下面直接设置控件的 ToolTip 属性：

```xml
<TextBox Margin="80,10,12,0" VerticalAlignment="Top"
Text="Prop" Tool="The customer's first name
Name="txtFirstName" Height="21.96" />
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_126_1.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_126_2.png)

图 5-13

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_126_3.png)

# 空间控件 (SPATIAL CONTROLS)

空间控件具有重要的空间组件。某些控件，如 BulletDecorator 和 GroupBox，为其他控件提供空间布局和装饰。其他的控件，如 ListView 和 ListView，则使用空间定位来显示对象之间的关系。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_126_4.png)

图 5-14

# 边框 (Border)

Border 用于控制边框或背景。从某种意义上说它是空间控件，因为它创建了一个容纳子元素的空间。虽然这似乎是一项小成就，但在窗口上创建单独区域对于定义控件组非常有用。例如，如果窗口包含许多单选按钮或复选框，用 Border 将它们分组可以使窗口更容易阅读和理解。

该控件只能有一个小的子元素，但该元素可以是像 Grid 或 StackPanel这样的容器，因此这并没太大限制。

下表总结了 Border 最常用的属性：

| 属性 | 用途 |
| --- | --- |
| Background | 控件的背景画刷 |
| BorderBrush | 用于绘制边框边缘的画刷 |
| BorderThickness | 决定边框边缘的厚度。如果这是一个值，则所有四边都使用相同的厚度 |
| CornerRadius | 决定边框圆角的曲半径。如果这是一个值，则所有角都使用相同的半径。正角默认为 0。 |

以下 XAML 代码创建了图 5-14 所示的 Border：

```xml
<Border HorizontalAlignment="Center" VerticalAlignment="Center"
  Width="150" Height="100"
  BorderBrush="#FFFF0000" BorderThickness="5">
  <Border.Effect>
    <DropShadowBitmapEffect/>
  </Border.Effect>
  <Border.Background>
    <LinearGradientBrush EndPoint="0.5,0.1" StartPoint="0.5,0.0">
      <GradientStop Color="#FFFF00FF" Offset="0" />
      <GradientStop Color="#FF0000FF" Offset="1" />
    </LinearGradientBrush>
  </Border.Background>
  <TextBlock Width="100" Height="50" FontWeight="Bold"
    TextWrapping="Wrap" TextAlignment="Center"
    Text="This TextBlock is contained inside the Border."/>
</Border>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_127_0.png)

图 5-14

# 项目符号装饰器 (BulletDecorator)

BulletDecorator 在项目符号列表中显示一个项目和符号。该控件只能有一个子元素（符号除外），但该元素可以是像 Grid 或 StackPanel 这样的容器，因此这并不是真正的限制。

BulletDecorator 最重要的属性是 Bullet，它应该包含用作项目符号的对象。通常，这应该是看起来像符号的东西，例如小图像或字符，但在理论上，它可以是像 label 或 border 之其他内容。

以下 XAML 代码创建了图 5-15 所示项目符号列表中的第一个项目。三个 BulletDecorator 控件包含在一个 StackPanel 中以形成列表。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_128_0.png)

```xml
<BulletDecorator>
  <BulletDecorator.Bullet>
    <Image Width="20" Height="20"
      Source="Bullet.bmp" Stretch="None"
      HorizontalAlignment="Left" VerticalAlignment="Center">
      <Image.BitmapEffect>
        <GroupShadowBitmapEffect/>
      </Image.BitmapEffect>
    </Image>
  </BulletDecorator.Bullet>
  <Label Content="Choice 1" Foreground="Red"/>
</BulletDecorator>
```

图 5-15

# 分组框 (GroupBox)

GroupBox 显示标题和环绕子元素的边框。就像 Border 一样，GroupBox 用于在窗口中创建不同的区域。GroupBox 的 Foreground 属性用于绘制标题文本，Background 属性用于填充 GroupBox。

| 边框 (BORDERS) |
| --- |
| 因为某些原因，如果 BorderThickness 大于 2，GroupBox 会被填充 |
| 注意可以通过设置 BorderThickness 来隐藏边框 |

第 5 章 内容控件 (CONTENT CONTROLS)

以下 XAML 代码创建了图 5-16 所示的 GroupBox。GroupBox 包含了 Label 和 TextBox 控件。

```xml
<GroupBox Header="Customer" Margin="5" BorderBrush="#D5EE">
  <Grid>
</GroupBox>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_129_0.png)

图 5-16

# 列表 (ListView)

ListView 在具有可调整列的布局中显示一组数据。最常见的布局是图 5-17 所示的视图。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_129_1.png)

图 5-17

在网格布局中显示一组数据有时有用，ListView 的真正威力在于它可以从数据库或列表等源显示数据。数据将在第 18 章详细介绍；C# 代码显示了 ListView 如何定义 BookInfo 类。这里显示了 Author 属性的代码。

```csharp
public class BookInfo
{
    // 初始化新对象的字段。
    public BookInfo(string new_Author, string new_Title,
        string new_Year, string new_Price)
    {
        Author = new_Author;
        Title = new_Title;
        Year = new_Year;
        Price = new_Price;
    }

    private String m_Author;
    public string Author
    {
        get { return m_Author; }
        set { m_Author = value; }
    }
    // 其他属性的代码省略
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_130_0.png)

当程序启动时，它使用以下代码创建一个包含显示数据的 BookInfo ObservableCollection。将 ListView 控件的 DataContext 属性设置为集合，以便控件访问所有数据。

```csharp
// 创建书籍列表
ObservableCollection<BookInfo> books = new ObservableCollection<BookInfo>();
books.Add(new BookInfo("Daniel Pinkwater", "5 Novels", "2005", "3.56"));
books.Add(new BookInfo("Glen Cook", "Garret Files", "2007", "6.99"));
books.Add(new BookInfo("Simon R. Green", "The Man With The Golden Core", "2008", "7.99"));
books.Add(new BookInfo("Tad Williams", "The Name of the Flowers", "2004", "8.99"));
books.Add(new BookInfo("Tom Holt", "You Don't Have to Ever Work Here, but it Helps", "2007", "10.00"));

// 将 ListView 的数据上下文设置为此列表
lvbooks.DataContext = books;
```

除了为 ListView 分配 Name 和 Background 等属性外，XAML 代码必须告诉它显示哪些数据。以下 XAML 代码创建了图 5-7 所示的 ListView：

```xml
<ListView Name="lvwPeople"
Background="x:Null"
ItemsSource="{Binding}">
    <Grid>
        <GridColumn Header="Author" Width="100"
        DisplayMemberBinding="{Binding Path=Author}"/>
        <GridColumn Header="Title" Width="300">
```

