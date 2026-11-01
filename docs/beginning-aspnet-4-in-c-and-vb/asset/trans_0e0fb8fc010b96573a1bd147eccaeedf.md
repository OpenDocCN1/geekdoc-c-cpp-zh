
> 另一个自定义错误消息的选项是注册到 Validation 类的 Error 事件。这里必须将属性 NotifyOnValidationError 设置为 true。

错误信息本身可以从 Validation 类的 Errors 集合中访问。为了在 TextBox 的 ToolTip 中显示错误信息，你可以创建如下的属性触发器。一旦 Validation 类的 HasError 属性被设置为 True，触发器就会被激活。该触发器设置 TextBox 的 ToolTip 属性：

```
<Style TargetType="{x:Type TextBox}">
    <Style.Triggers>
        <Trigger Property="Validation.HasError" Value="True">
            <Setter Property="ToolTip"
                Value="{Binding RelativeSource=Self,
                    Path=(Validation.Errors)[0].ErrorContent}" />
        </Trigger>
    </Style.Triggers>
</Style>
```

## 数据错误信息

处理错误的另一种方式是让 .NET 对象实现 IDataErrorInfo 接口。

现在将 SomeData 类改为实现 IDataErrorInfo 接口。该接口定义了 Error 属性和一个带字符串参数的索引器。在数据绑定过程中进行 WPF 验证时，会调用索引器，并将要验证的属性名称作为 columnName 参数传入。通过该实现，可以验证值是否有效，如果无效则返回错误字符串。此处对 Value2 属性进行验证，该属性使用 C# 3.0 简单属性语法实现：

```
public class SomeData : IDataErrorInfo
{
    //...

    public int Value2 { get; set; }

    string IDataErrorInfo.Error
    {
        get
        {
            return null;
        }
    }

    string IDataErrorInfo.this[string columnName]
    {
        get
        {
            if (columnName == "Value2")
            {
                if (this.Value2 < 0 || this.Value2 > 80)
                    return "age must not be less than 0 or greater than 80";
            }
            return null;
        }
    }
}
```

![](img/d7d2ffa0a76feaab821930e95daace93_1121_0.png)

如果将 Binding 类的 ValidatesOnDataErrors 属性设置为 true，则在绑定期间会使用 IDataErrorInfo 接口。在这里，当 TextBox 被更改时，绑定机制会调用该接口的索引器，并将 Value2 传递给 columnName 变量：

```
<Label Margin="5" Grid.Row="1" Grid.Column="0" >Value2:</Label>
<TextBox Margin="5" Grid.Row="1" Grid.Column="1"
Text="{Binding Path=Value2, ValidatesOnDataErrors=True}" />
```

*代码片段 ValidationDemo/MainWindow.xaml*

## 自定义验证规则

为了对验证进行更多控制，你可以实现自定义验证规则。实现自定义验证规则的类需要从基类 ValidationRule 派生。在前两个示例中，也已经使用了验证规则。从抽象基类 ValidationRule 派生的两个类是 DataErrorValidationRule 和 ExceptionValidationRule。DataErrorValidationRule 通过设置 ValidatesOnDataErrors 属性来激活，并使用 IDataErrorInfo 接口；ExceptionValidationRule 处理异常，通过设置 ValidatesOnException 属性来激活。

这里实现了一个验证规则，用于验证正则表达式。RegularExpressionValidationRule 类派生自基类 ValidationRule，并重写了基类定义的抽象方法 Validate()。在实现中，使用来自命名空间 System.Text.RegularExpressions 的 RegEx 类来验证由 Expression 属性定义的正则表达式：

```
public class RegularExpressionValidationRule: ValidationRule
{
    public string Expression { get; set; }
    public string ErrorMessage { get; set; }

    public override ValidationResult Validate(object value,
        CultureInfo cultureInfo)
    {
        ValidationResult result = null;
        if (value != null)
        {
            Regex regex = new Regex(Expression);
            bool isMatch = regex.IsMatch(value.ToString());
            result = new ValidationResult(isMatch, isMatch ?
                null: ErrorMessage);
        }
        return result;
    }
}
```

![](img/d7d2ffa0a76feaab821930e95daace93_1121_1.png)

![](img/d7d2ffa0a76feaab821930e95daace93_1125_0.png)

## 图 36-13

> ADO.NET Entity Framework 在第 31 章“ADO.NET Entity Framework”中介绍。

通过 XAML 代码声明了一个 TreeView。TreeView 派生自基类 ItemsControl，可以使用 ItemsSource 属性绑定到列表。ItemsSource 绑定到数据上下文。数据上下文在代码隐藏文件中分配，稍后你会看到。当然，这也可以使用 ObjectDataProvider 完成。为了为分层数据定义自定义显示，定义了 HierarchicalDataTemplate 元素。这里的数据模板通过 DataType 属性为特定的数据类型定义。第一个 HierarchicalDataTemplate 是 Championship 类的模板，将该类的 Year 属性绑定到 TextBlock 的 Text 属性。ItemsSource 属性定义了数据模板本身的绑定，以定义数据层次结构中的下一级。如果 Championship 类的 Races 属性返回一个集合，你可以直接将 ItemsSource 属性绑定到 Races。但是，由于该属性返回 Lazy<T> 对象，因此绑定到 Races.Value。Lazy<T> 类的优点将在本章后面讨论。

第二个 HierarchicalDataTemplate 元素定义了 F1Race 类的模板，并绑定该类的 Country 和 Date 属性。对于 Date 属性，在绑定中定义了 StringFormat。层次结构的下一级通过将 ItemsSource 绑定到 Results.Value 来定义。

F1RaceResult 类没有子集合，因此层次结构到此结束。对于这种数据类型，定义了一个普通的 DataTemplate 来绑定 Position、Racer 和 Car 属性：

```
<UserControl x:Class="FormulaDemo.TreeUC"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:local="clr-namespace:FormulaDemo"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="300">
    <Grid>
        <TreeView ItemsSource="{Binding}">
            <TreeView.Resources>
                <HierarchicalDataTemplate DataType="{x:Type local:Championship}" ItemsSource="{Binding Races.Value}">
                    <TextBlock Text="{Binding Year}" />
                </HierarchicalDataTemplate>

                <HierarchicalDataTemplate DataType="{x:Type local:F1Race}" ItemsSource="{Binding Results.Value}">
                    <StackPanel Orientation="Horizontal">
                        <TextBlock Text="{Binding Country}" Margin="5,0,5,0" />
                        <TextBlock Text="{Binding Path=Date, StringFormat=d }" Margin="5,0,5,0" />
                    </StackPanel>
                </HierarchicalDataTemplate>

                <DataTemplate DataType="{x:Type local:F1RaceResult}">
                    <StackPanel Orientation="Horizontal">
                        <TextBlock Text="{Binding Position}" Margin="5,0,5,0" />
                        <TextBlock Text="{Binding Racer}" Margin="5,0,0,0" />
                        <TextBlock Text=", " />
                        <TextBlock Text="{Binding Car}" />
                    </StackPanel>
                </DataTemplate>
            </TreeView.Resources>
        </TreeView>
    </Grid>
</UserControl>
```

代码片段 Formula1Demo/TreeUC.xaml

现在来看填充分层控件的代码。在 XAML 代码的代码隐藏文件中，DataContext 被赋值给 Years 属性。Years 属性使用 LINQ 查询（而不是 ADO.NET Entity Framework 数据上下文）来获取数据库中所有 Formula-1 比赛的年份，并为每一年创建一个新的 Championship 对象。通过 Championship 类的实例，设置 Year 属性。该类还有一个 Races 属性，用于返回该年份的比赛；但是，该信息尚未填充。

![](img/d7d2ffa0a76feaab821930e95daace93_1126_0.png)

```
using System.Collections.Generic;
using System.Linq;
using System.Windows.Controls;

namespace Formula1Demo
{
    public partial class TreeUC : UserControl
    {
        private Formula1Entities data = new Formula1Entities();

        public TreeUC()
        {
            InitializeComponent();
            this.DataContext = Years;
        }
    }
```

