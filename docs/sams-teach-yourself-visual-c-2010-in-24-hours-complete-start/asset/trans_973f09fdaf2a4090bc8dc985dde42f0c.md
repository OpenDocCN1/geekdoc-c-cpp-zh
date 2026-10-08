

## 列表 18.12 绑定到当前项

```xml
// 绑定到整个集合。
<Label Content="{Binding}" />

// 绑定到集合中的当前项。
<Label Content="{Binding Path=/}" />

// 绑定到集合中当前项的 LastName 属性。
<Label Content="{Binding Path=/LastName}" />
```

当像 `Label` 这样不支持 `ItemsSource` 属性的元素绑定到集合视图时，它们会自动绑定到该视图的当前项。`CollectionViewSource` 对象会自动同步当前选定的项，但如果 `ItemsControl` 未绑定到 `CollectionViewSource`，你需要将 `IsSynchronizedWithCurrentItem` 属性设置为 `true` 才能使此功能正常工作。

可以想象，当前项指针对于创建主从样式绑定也非常有用。在这种绑定中，用户界面的一个部分显示整个集合（可能以摘要或简化的形式），而另一部分显示当前项的完整详细信息。

## 使用数据模板

在上一小时的末尾，你学习了如何通过完全更改控件的外观来为你的应用程序设置样式。这些视觉样式仅更改控件的外观；它们并不指定控件如何可视化数据。要更改控件可视化数据的方式，你可以使用 `DataTemplate`。当将 `ItemsControl`（如 `ListBox`）绑定到集合时，这特别有用。

如果没有 `DataTemplate`，`ItemsControl` 在尝试显示集合中的对象时会调用 `ToString`。虽然你可以重写 `ToString` 以提供有意义的字符串表示，但这并不总是最佳方法（或者可能根本不可行）。解决方案是定义一个 `DataTemplate`，它允许你更改 `ItemsControl` 用于显示数据的视觉结构。

列表 18.13 显示了 `PhotoViewer` 应用程序使用的 `DataTemplate`，使得 `ListBox` 控件显示图像的缩略图而不是文件名。

### 列表 18.13 定义 DataTemplate

```xml
<DataTemplate DataType="{x:Type er:Photo}">
    <Grid VerticalAlignment="Center" HorizontalAlignment="Center" Margin="6">
        <!-- 阴影 -->
        <Border HorizontalAlignment="Stretch" VerticalAlignment="Stretch"
                CornerRadius="4" Background="#44000000">
            <Border.RenderTransform>
                <TranslateTransform X="5" Y="5" />
            </Border.RenderTransform>
            <Border.BitmapEffect>
                <BlurBitmapEffect Radius="8" />
            </Border.BitmapEffect>
        </Border>
        <!-- 图像模板 -->
        <Border Padding="4" Background="White" BorderBrush="#22000000"
                BorderThickness="1">
            <StackPanel Orientation="Vertical">
                <Image Source="{Binding Image.Thumbnail}" />
                <Label Content="{Binding Metadata.DateTaken}">
                    <Label.ToolTip>
                        仅限 JPEG 图像...
                    </Label.ToolTip>
                </Label>
            </StackPanel>
        </Border>
    </Grid>
</DataTemplate>
```

在这种情况下，`DataTemplate` 为 `DataType` 属性指定了一个值。这与 `Style` 的 `TargetType` 属性类似，表明该 `DataTemplate` 应被显示该类型对象的任何控件使用。

你還可以指定 `x:Key` 属性，在这种情况下，你需要明确地将模板与控件关联起来。列表 18.14 显示了这样的关联，假设该 `DataTemplate` 有一个值为 `photoTemplate` 的 `x:Key` 属性。

### 列表 18.14 关联 DataTemplate

```xml
<ListBox
    ItemsSource="{Binding}"
    ItemTemplate="{StaticResource photoTemplate}">
```

### 验证数据

如果你的应用程序接受用户输入（大多数应用程序都是如此），你可能需要根据业务规则验证该输入，以确保用户输入了预期的信息。在 WPF 中，验证检查可以基于类型、范围、格式或某些其他特定于应用程序的需求，它们是数据绑定引擎的一部分。

为了添加验证检查，你需要将 `ValidationRules` 与你的 `Binding` 关联起来，如列表 18.15 所示。

### 列表 18.15 将 ValidationRules 与 Binding 关联

```xml
<TextBox Name="LastName">
<TextBox.Text>
<Binding Path="LastName" UpdateSourceTrigger="PropertyChanged">
<Binding.ValidationRules>
<ExceptionValidationRule />
</Binding.ValidationRules>
</Binding>
</TextBox.Text>
</TextBox>
```

如你所见，`ValidationRules` 属性接受一个 `ValidationRule` 对象的集合。`ExceptionValidationRule` 是一个内置验证规则，用于检查在更新绑定源期间抛出的异常。如果源对象实现了 `IDataError` 接口，你可以使用内置的 `DataErrorValidationRule` 来检查由 `IDataError` 实现引发的错误。

> **ValidatesOnException 和 ValidatesOnDataErrors**

作为明确包含 `ExceptionValidationRule` 的替代方案，你可以将 `ValidatesOnExceptions` 属性设置为 `true`。同样地，你可以将 `ValidatesOnDataErrors` 属性设置为 `true`，而不是明确包含 `DataErrorValidationRule`。

为了提供你自己的特定于应用程序的验证规则，你可以从 `ValidationRule` 类派生一个新的类并实现 `Validate` 方法。列表 18.16 显示了 `AddressBook` 应用程序的一个验证规则，它可以验证电话号码。

### 列表 18.16 自定义 ValidationRule

```csharp
class PhoneNumberValidationRule : ValidationRule
{
public override ValidationResult Validate(object value, CultureInfo cultureInfo)
{
string stringValue = value.ToString();
string pattern = @"^((\+?\d+)\s?(\(\d{3}\)\s?\w{3}[-\.\w{4})\s?\w{3}[-\.\w{4}])+";

if (String.IsNullOrEmpty(stringValue) ||
Regex.IsMatch(stringValue, pattern))
{
return ValidationResult.ValidResult;
}
else
{
return new ValidationResult(false, "Value is not a valid phone number.");
}
}
```

**注意！**

### UpdateSourceTrigger 属性

当 **UpdateSourceTrigger** 的值为 **PropertyChanged** 时（如列表 18.15 所示），绑定引擎会在每次按键时更新源值。这也意味着 **ValidationRules** 集合中的每个规则都会在每次按键时进行检查。

虽然确定用户输入了无效值是数据验证的主要用途，但你也可以提供视觉反馈，表明该值无效。为此，你首先需要定义一个 **ControlTemplate**，它定义了控件的视觉和结构外观。例如，列表 18.17 定义了一个 **ControlTemplate**，在包含错误的控件前放置一个红色星号符号。

### 列表 18.17 自定义 ControlTemplate

```xml
<ControlTemplate x:Key="validationTemplate">
<DockPanel>
<TextBlock Foreground="FireBrick" FontSize="18">*</TextBlock>
<AdornedElementPlaceholder />
</DockPanel>
</ControlTemplate>
```

**AdornedElementPlaceholder** 元素指示实际包含错误的控件将被放置的位置。

要使用此 **ControlTemplate**，你需要将 `UIElement` 的 **Validation.ErrorTemplate** 属性设置为自定义的 **ControlTemplate**，如列表 18.18 所示。

### 列表 18.18 设置 Validation.ErrorTemplate 属性

```xml
<TextBox Name="PhoneNumber" 
Validation.ErrorTemplate="{StaticResource validationTemplate}">
<TextBox.Text>
<Binding Path="PersonalInformation.HomePhone" 
UpdateSourceTrigger="PropertyChanged">
<Binding.ValidationRules>
<ExceptionValidationRule />
<sb:PhoneNumberValidationRule />
</Binding.ValidationRules>
</Binding>
</TextBox.Text>
</TextBox>
```

如果你没有指定 **ErrorTemplate**，将使用默认模板。此默认模板在被装饰的控件周围定义了一个红色边框。

## 自己动手

### 验证输入

要为 `AddressBook` 应用程序添加验证规则，请按照以下步骤操作。

- 1. 将列表 18.16 中显示的验证规则添加到 `AddressBook` 应用程序中。
- 2. 在 `AddressBook` 应用程序中添加一个名为 *EmptyStringValidationRule* 的新验证规则，以验证要验证的对象不是空字符串。
- 3. 将列表 18.17 中显示的 `ControlTemplate` 添加到 `ContactEditor.xaml` 文件的 `Window.Resources` 元素中。
- 4. 修改 `ContactEditor.xaml` 文件，使以下元素的绑定设置 *Validation.ErrorTemplate* 属性并包含指定的验证规则：

| 元素 | 验证规则 |
| :--- | :--- |
| 名 (First Name) | *EmptyStringValidationRule* |
| 姓 (Last Name) | *EmptyStringValidationRule* |
| 家庭电话 (Home Phone) | *PhoneNumberValidationRule* |
| 移动电话 (Mobile Phone) | *PhoneNumberValidationRule* |
| 工作电话 (Work Phone) | *PhoneNumberValidationRule* |
| 寻呼机 (Pager) | *PhoneNumberValidationRule* |
| 传真 (Fax) | *PhoneNumberValidationRule* |

- 5. 运行应用程序并点击工具栏上的“添加联系人”按钮以显示 `ContactEditor` 窗体。输入一些无效数据，观察无效字段的视觉表示形式更改为 `ControlTemplate` 定义的样子。

## 摘要

在本小时中，你学习了 WPF 中的数据绑定，并为 `PhotoViewer` 应用程序添加了绑定使其更加完整。接着，你学习了数据转换器如何改变绑定一侧的值，使其成为绑定另一侧所接受的值。然后你学习了如何绑定到集合以及

