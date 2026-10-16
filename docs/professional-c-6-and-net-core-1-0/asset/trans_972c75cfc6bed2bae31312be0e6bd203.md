

编译绑定的特性。

你可以使用编译数据绑定作为 Binding 标记扩展的更快替代方案。只有少数情况下需要旧的绑定语法——例如，在属性更改时触发绑定，而不是在焦点更改时触发。我相信，随着编译绑定在未来的版本中得到进一步增强，这种情况将会改变。目前，这还不足以成为完全不用编译绑定的理由，因为你可以将编译绑定与 Binding 标记表达式混合使用。

第 31 章介绍了使用 x:Bind 代替 Binding 的编译绑定新语法，代码会被编译，你甚至可以得到编译器错误。

由于编译绑定侧重于性能，默认模式是 OneTime。如果你需要根据代码中的更改来更新用户界面，则需要显式地将模式设置为 OneWay。若要从 UI 更新源，则需要设置 TwoWay 模式。编译绑定使用与 Binding 表达式相同的模式，但默认值不同。

由于第 31 章已经讨论过编译绑定，本章只介绍编译绑定的一些特殊功能，例如在资源内部使用它，以及控制绑定生命周期。

## 编译绑定生命周期

使用编译绑定时，代码由绑定生成。你也可以通过编程方式影响绑定的生命周期。

让我们从一个简单的 Book 类型开始，该类型绑定自用户界面（代码文件 CompiledBindingSample/Models/Book.cs）：

```
public class Book : BindableBase
{
    public int BookId { get; set; }
    private string _title;

    public string Title
    {
        get { return _title; }
        set { SetProperty(ref _title, value); }
    }

    public string Publisher { get; set; }

    public override string ToString() => Title;
}
```

在页面类中，创建了一个只读属性 Book，它返回一个 Book 实例。Book 实例的值可以更改，而 Book 实例本身是只读的（代码文件 CompiledBindingSample/Views/LifetimeSample.xaml.cs）：

```
public Book Book { get; } = new Book
{
```

```
Title ="Professional C# 6",
Publisher ="Wrox Press"
};
```

在 XAML 代码中，Title 属性以 OneWay 模式绑定到 TextBlock 的 Text 属性，而 Publisher 在未指定模式的情况下绑定，这意味着它是 OneTime 绑定（代码文件 CompiledBindingSample/Views/LifetimeSample.xaml）：

```
<StackPanel>
    <TextBlock Text="{x:Bind Book.Title, Mode=OneWay}" />
    <TextBlock Text="{x:Bind Book.Publisher}" />
</StackPanel>
```

接下来，多个 AppBarButton 控件被绑定以更改编译绑定的生命周期。其中一个按钮的 Click 事件绑定到 OnChangeBook 方法。此方法更改图书的标题。如果你尝试这样做，标题会立即更新，因为完成了一次 OneTime 绑定（代码文件 CompiledBindingSample/Views/LifetimeSample.xaml.cs）：

```
public void OnChangeBook()
{
    Book.Title ="Professional C# 6 and .NET Core 5";
}
```

但是，你可以停止绑定的跟踪。使用页面的 Bindings 属性（如果你使用编译绑定，则会创建此属性）调用 StopTracking 方法，会移除所有绑定侦听器。如果在调用 OnChangeBook 方法之前调用此方法，则图书的更新不会反映在用户界面中：

```
private void OnStopTracking()
{
    Bindings.StopTracking();
}
```

若要从绑定的源显式更新用户界面，可以调用 Update 方法。调用此方法不仅会反映 OneWay 或 TwoWay 绑定中的更改，还会反映 OneTime 绑定中的更改：

```
private void OnUpdateBinding()
{
    Bindings.Update();
}
```

要将侦听器重新置于适当位置，以便对用户界面进行即时更新，需要调用 Initialize 方法。

Initialize、Update 和 StopTracking 是使用编译绑定控制生命周期的三个重要方法。

## 使用资源创建编译数据模板

使用编译绑定定义数据模板很简单；你只需为数据模板指定 x:DataType 属性，因为这样

```
RequestedTheme="Light">
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <styles:DataTemplates />
        </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
</Application.Resources>
</Application>
```

一切就绪后，可以像往常一样引用数据模板——例如，使用 ListBox 的 ItemTemplate（代码文件 CompiledBindingSample/Views/BooksListPage.xaml）：

```
<ListBox ItemTemplate="{StaticResource BookTemplate}" ItemsSource="{x:Bind Books}" Margin="8" />
```

## 控件

本书无法涵盖 UWP 提供的所有控件。但是，它们的使用很简单，当你知道如何使用其中一些控件时，使用其他控件并不困难。许多控件与 WPF 控件有相似之处，因此你可以在第 34 章中阅读更多关于控件的信息。

### TextBox 控件

对于 UWP 控件，值得一提的特殊功能是 TextBox 控件上的 Header 属性。在本章前面，你已经了解了如何使用 RelativePanel 排列编辑表单。在该示例中，TextBox 控件与 TextBlock 控件结合使用。通常，应在 TextBox 中输入的信息通过此文本输入控件附近的标签来描述。TextBlock 控件在 RelativePanel 的示例中起到了这个作用。还有另一种向 TextBox 添加信息的方法。当你使用 TextBox 控件的 Header 属性时，无需定义单独的 TextBlock 控件。填充 Header 属性即可。Header 属性的值会显示在 TextBox 附近（参见图 32.26）。

![](img/3d365b72b289213a91ade7eb366b8f35_1231_0.png)

图 32.26

当你设置 InputScope 属性时，可以指定显示哪个屏幕键盘。图 32.27 显示了 Windows 屏幕键盘，其中 InputScope 设置为 Formula，如以下代码片段所示。使用此键盘，你可以看到一些特定于公式的键（代码文件 ControlsSamples/Views/TextSample.xaml）：

```
{
 xmlRacers = XElement.Load(stream);
}
_racers = xmlRacers.Elements("Racer").Select(r => new Racer
{
 FirstName = r.Element("Firstname").Value,
 LastName = r.Element("Lastname").Value,
 Country = r.Element("Country").Value
}).ToList();
```

Racer 类包含 FirstName、LastName 和 Country 属性，以及 ToString 方法的重载（代码文件 ControlsSamples/Models/Racer.cs）：

```csharp
public class Racer
{
 public string FirstName { get; set; }
 public string LastName { get; set; }
 public string Country { get; set; }
 public override string ToString() => $"{FirstName} {LastName}, {Country}";
}
```

只要 AutoSuggestBox 的文本发生更改，就会调用 OnTextChanged 事件。接收到的参数是 AutoSuggestBox 本身（发送者）和 AutoSuggestBoxTextChangedEventArgs。通过 AutoSuggestBoxTextChangedEventArgs，更改原因显示在 Reason 属性中。可能的原因包括 UserInput、ProgrammaticChange 和 SuggestionChosen。仅在原因为 UserInput 时，才需要向用户提供建议。此处还会进行检查，以确保用户至少输入了两个字符。用户输入通过访问 AutoSuggestBox 的 Text 属性来获取。此文本用于根据输入字符串查询名字、姓氏和国家。查询结果被分配给 AutoSuggestBox 的 ItemsSource 属性（代码文件 ControlsSamples/Views/AutoSuggestSample.xaml.cs）：

```csharp
private void OnTextChanged(AutoSuggestBox sender,
 AutoSuggestBoxTextChangedEventArgs args)
{
 if (args.Reason == AutoSuggestionBoxTextChangeReason.UserInput
 &&
 sender.Text.Length >= 2)
 {
 string input = sender.Text;
 var q = _racers.Where(
 r => r.FirstName.StartsWith(input,
 StringComparison.CurrentCultureIgnoreCase))
 .OrderBy(r => r.FirstName).ThenBy(r => r.LastName)
 .ThenBy(r => r.Country).ToArray();
 if (q.Length == 0)
 {
 q = _racers.Where(r => r.LastName.StartsWith(input,
 StringComparison.CurrentCultureIgnoreCase))
 .OrderBy(r => r.LastName).ThenBy(r => r.FirstName)
 .ThenBy(r => r.Country).ToArray();
 if (q.Length == 0)
 {
 q = _racers.Where(r => r.FirstName.StartsWith(input,
 StringComparison.CurrentCultureIgnoreCase) || r.LastName.StartsWith(input,
 StringComparison.CurrentCultureIgnoreCase))
 .OrderBy(r => r.FirstName).ThenBy(r => r.LastName)
 .ThenBy(r => r.Country).ToArray();
 }
 }
 }
}
```

