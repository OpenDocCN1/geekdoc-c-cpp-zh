
```
NotifyPropertyChanged("Make");
}
}
public string Model
{
    get { return _model; }
    set
    {
        if (_model != value)
        {
            _model = value;
            NotifyPropertyChanged("Model");
        }
    }
}
```

## 11. 再次运行应用程序。

现在，当你单击“使用代码隐藏更改数据上下文值”按钮时，更改后的值会自动反映到 TextBox 元素中。这是由于 TwoWay 绑定模式以及 INotifyPropertyChanged 的实现共同作用的结果。（见图 3-3。）

![](img/80ff26f06fc9ab951e1cd4257b867366_635_0.png)

图 3-3：
使用 INotifyPropertyChanged 的 TwoWay 数据绑定。

## 验证数据

验证用户提供给您的任何输入是一种良好做法。人无完人，而且有些人可能完全怀有恶意。WPF 提供了用于数据验证和错误通知的内置框架。通过在你的类上实现 IDataErrorInfo 接口，即可使用该框架。

你可以向上一节 Binding Sample2 中已创建的 Car 类添加验证。

## 元素绑定

在本章中，你将 Label 和 TextBox 控件绑定到基础对象的属性。你并不限于这种场景；几乎可以绑定任何内容，从基元变量到从其他 UIElement 中获取的属性值。元素绑定在 Binding 表达式中尤其有自己专门的组件。例如，假设窗口中有一个 TextBox 和一个 Label 控件。你希望 Label 的 Content 随 TextBox 的 Text 属性值变化而自动更新。用于在 TextBox 和 Label 之间完成元素绑定的 XAML 代码类似于

```
<Label x:Name="lblCarMake"
    Content="{Binding
        ElementName=txtCarMake,
        Path=Text}">
    <TextBox x:Name="txtCarMake"
        Width=200 Height=25 />
```

定义此绑定的 C# 代码类似于

```
Binding b = new
Binding("Text");
b.ElementName = "txtCarMake";
BindingOperations.
SetBinding(lblCarMake, Label.
ContentProperty, b);
```

![](img/80ff26f06fc9ab951e1cd4257b867366_636_0.png)

完整解决方案可在网上的 BindingSample2-Validation 项目中获取。

只需按照以下步骤向你的 Car 类添加验证：

- 1. 打开 Car.cs 文件，编辑该类，使其还实现 IDataErrorInfo 接口，如下所示：

```
public class Car : INotifyPropertyChanged, IDataErrorInfo
```

实现此接口会向 Car 类添加以下方法：

```
public string Error
{
    get { throw new NotImplementedException(); }
}

public string this[string columnName]
{
    get { throw new NotImplementedException(); }
}
```

- 2. 编辑 Error 属性的 Get 方法，使其返回 null。

现在是时候向 Car 对象的属性添加一些验证规则了。Car 的 Make 和 Model 属性应强制执行这样的规则：它们的长度必须始终至少为三个字符。public string this[string columnName] 方法由数据绑定引擎使用，以便在对象属性更改时，根据属性名（也就是方法签名中 columnName 的含义）验证对象属性。此方法返回与被编辑属性相关的任何错误消息。

3. 要定义并强制执行这些规则，请编辑 public string this[string columnName] 方法，如下所示：

```
public string this[string columnName]
{
    get {
        string retval = null;
        if (columnName == "Make")
        {
            if (String.IsNullOrEmpty(this._make)
                || this._make.Length < 3)
            {
                retval = "Car Make must be at least 3 " +
                    "characters in length";
            }
        }
        if (columnName == "Model")
        {
            if (String.IsNullOrEmpty(this._model)
                || this._model.Length < 3)
            {
                retval = "Car Model must be at least 3 " +
                    "characters in length";
            }
        }
        return retval;
    }
}
```

在 MainWindow.xaml 中，Make 和 Model 属性绑定到用户界面中的 TextBox 控件。

4. 要使输入到 TextBox 中的文本能够根据基础属性上定义的约束进行验证，请编辑每个 TextBox 中的绑定表达式，如下所示：

```
<TextBox x:Name="txtCarMake" VerticalAlignment="Top"
Text="{Binding Path=Make, Mode=TwoWay,
UpdateSourceTrigger=PropertyChanged,
ValidatesOnDataErrors=True,
ValidatesOnExceptions=True}"
Width="200" Height="25" />

<TextBox x:Name="txtCarModel" VerticalAlignment="Top"
Text="{Binding Path=Model, Mode=TwoWay,
UpdateSourceTrigger=PropertyChanged,
ValidatesOnDataErrors=True,
ValidatesOnExceptions=True}"
Width="200" Height="25" />
```

UpdateSourceTrigger 用于确定何时进行验证调用。在此示例中，验证会在文本更改时进行，并在基础对象属性触发 PropertyChanged 事件时被触发。

ValidatesOnDataErrors 使 IDataErrorInfo 验证方法能够在该属性上被调用。

![](img/80ff26f06fc9ab951e1cd4257b867366_637_0.png)

如果基础数据源抛出异常，ValidatesOnExceptions 会将 TextBox 标记为无效；例如，当你有一个整数属性而用户输入了字符串时，WPF 会自动抛出“输入字符串的格式不正确”异常。

5. 运行示例，并清除 Make 和 Model 这两个 TextBox 控件中的所有文本。

你会看到 TextBox 控件现在以红色呈现：当你重新向 TextBox 输入文本时，一旦达到三个字符，红色边框就会消失。图 3-4 显示了处于无效状态的 Make 文本框。

图 3-4：
使用 IDataErrorInfo 接口的简单数据验证。

![](img/80ff26f06fc9ab951e1cd4257b867366_638_0.png)

红色边框足以指示发生了错误，但对用户来说用处不大，因为他们并未被告知错误的详细信息。显示错误的一种简单方法是在 TextBox 上添加工具提示。为此，请向 Window 添加一个 Style 资源，定义一个在数据处于无效状态时触发工具提示的样式。

6. 将以下 XAML 直接添加到 MainWindow.xaml 顶部的 Window 标签下方，如下所示：

```
<Window.Resources>
    <Style x:Key="errorAwareTextBox" TargetType="{x:Type TextBox}">
        <Style.Triggers>
            <Trigger Property="Validation.HasError" Value="true">
                <Setter Property="ToolTip" Value="{Binding RelativeSource={x:Static RelativeSource.Self}, Path=(Validation.Errors)[0].ErrorContent}"/>
            </Trigger>
        </Style.Triggers>
    </Style>
</Window.Resources>
```

7. 向你的 TextBox 添加 Style 属性，如下所示：

```
Style="{StaticResource ResourceKey=errorAwareTextBox}"
```

现在，当你运行应用程序并清除 TextBox 控件中的文本时，TextBox 会显示包含实际错误消息的工具提示。（见图 3-5。）

![](img/80ff26f06fc9ab951e1cd4257b867366_639_0.png)

图 3-5：
使用样式显示错误消息。

## 转换数据

WPF 为你提供了让用户界面直观易用的能力。有时，这意味着允许用户以对他们有意义的不同格式输入数据，并由你负责将其输入的数据转换为数据源允许的格式。反之亦然；你可能希望将数据源中的数据转换为对用户更直观的形式。此类转换的一个常见用例是日期值的字符串表示形式，或者你希望显示红色或绿色圆圈而不是 True 或 False 值。

WPF 通过提供一个名为 IValueConverter 的简单接口使数据转换变得容易。此接口包含两个方法：

- ♦ **Convert：** 此方法从数据源获取值，并将其塑造成要在屏幕上向用户显示的形式。
- ♦ **ConvertBack：** 此方法执行相反的操作——它从用户界面获取值，并将其塑造成数据源所期望的形式。

需要注意的是，使用这些方法时，你不必受限于被绑定值的数据类型。例如，被绑定的数据源属性可以是 Date 数据类型，而 Convert 方法仍可向用户界面返回字符串值。

为了演示此功能，请创建一个名为 BindingSample3 的新 WPF 应用程序项目。该项目是一个仪表板应用程序，可以显示
