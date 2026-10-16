

```
Click="OnButtonClick" />
    <!--etc.-->
</Page>
```

## 使用自定义 .NET 类

要在 XAML 代码中使用自定义 .NET 类，只需在 XAML 中声明 .NET 命名空间，并定义一个 XML 别名即可。为此演示，定义了一个简单的 Person 类，具有 FirstName 和 LastName 属性，如下所示（代码文件 DataLib/Person.cs）：

```
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public override string ToString() => $"{FirstName}
{LastName}";
}
```

> 注意 若要在 WPF 和 UWP 应用中同时使用类型，DataLib 库被创建为便携式库。

在 XAML 中，定义了一个名为 datalib 的 XML 命名空间别名，它映射到程序集 DataLib 中的 .NET 命名空间 DataLib。如果类型位于与窗口相同的程序集中，可以从此声明中删除程序集名称。有了此别名后，就可以通过在元素前加上别名名称来使用此命名空间中的所有类。

在 XAML 代码中，你添加了一个包含 Person 类型项的 ListBox。使用 XAML 属性，你设置 FirstName 和 LastName 属性的值。当你运行应用程序时，ToString 方法的输出会显示在 ListBox 内部（代码文件 XAMLIntroWPF/MainWindow.xaml）：

```
<Window x:Class="XamlIntroWPF.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:datalib="clr-namespace:DataLib;assembly=DataLib"
    Title="XAML Demo" Height="350" Width="525">
    <StackPanel>
        <Button Content="Click Me!" />
        <ListBox>
            <datalib:Person FirstName="Stephanie" LastName="Nagel" />
            <datalib:Person FirstName="Matthias" LastName="Nagel" />
        </ListBox>
    </StackPanel>
</Window>
```

对于 UWP 应用，XAML 声明有所不同，即使用 using 而不是 clr-namespace，并且不需要程序集名称（代码文件 XAMLIntroUWP/MainPage.xaml）：

```
<Page
    x:Class="XamlIntroUWP.MainPage"

xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"

    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:datalib="using:DataLib">
```

> 注意 UWP 应用在别名声明中不使用 clr-namespace 的原因在于，UWP 中的 XAML 既不基于 .NET 也不受其限制。你也可以使用原生 C++ 与 XAML，因此 clr 并不是一个合适的选择。

在 WPF 应用程序中，除了使用 XML 别名定义 .NET 命名空间和程序集名称外，还可以使用库中的 assembly 属性 XmlNsDefinition 将 .NET 命名空间映射到 XML 命名空间。此属性的一个参数定义 XML 命名空间，另一个参数定义 .NET 命名空间。使用此属性，还可以将多个 .NET 命名空间映射到单个 XML 命名空间：

```
[assembly:
XmlnsDefinition("http://www.wrox.com/Schemas/2015","Wrox.ProCSharp:
```

有了此属性后，XAML 代码中的命名空间声明可以更改为映射到 XML 命名空间：

```
<Window x:Class="Wrox.ProCSharp.XAML.MainWindow"

xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"

    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:datalib="http://www.wrox.com/Schemas/2015"
    Title="XAML Demo" Height="350" Width="525">
```

## 将属性设置为属性

只要属性类型可以用字符串表示，或者存在从字符串到属性类型的转换，就可以用属性设置属性。以下代码片段使用属性设置 Button 元素的 Content 和 Background 属性：

```
<Button Content="Click Me!" Background="LightGoldenrodYellow" />
```

在前面的代码片段中，Content 属性的类型为 object，因此接受字符串。Background 属性的类型为 Brush。Brush 类型使用 TypeConverter 属性将 BrushConverter 类定义为转换器类型，该类被此属性注释。
BrushConverter 使用颜色列表从 ConvertFromString 方法返回 SolidColorBrush。

> **注意** *类型转换器* 派生自 `System.ComponentModel` *命名空间* 中的基类 `TypeConverter`。需要转换的类的 *类型* 使用 `TypeConverter` 属性定义 *类型转换器*。WPF 使用许多类型转换器将 XML 属性转换为特定类型，包括 `ColorConverter`、`FontFamilyConverter`、`PathFigureCollectionConverter`、`ThicknessConverter` 和 `GeometryConverter,` *仅举几例。*

## 使用元素作为属性

使用元素语法为属性提供值也是完全可行的。你可以使用子元素 `Button.Background` 设置 `Button` 类的 `Background` 属性。以下代码片段使用与前面使用属性时相同的结果定义 `Button`：

```
```xml
<Button>
    Click Me!
    <Button.Background>
        <SolidColorBrush Color="LightGoldenrodYellow" />
    </Button.Background>
</Button>
```
```

使用元素而不是属性可以让你将更复杂的画刷应用于 `Background` 属性，例如 `LinearGradientBrush`，如下例所示（代码文件 `XAMLSyntax/MainWindow.xaml`）：

```
```xml
<Button>
    Click Me!
    <Button.Background>
        <LinearGradientBrush StartPoint="0.5,0.0" EndPoint="0.5,1.0">
            <GradientStop Offset="0" Color="Yellow" />
            <GradientStop Offset="0.3" Color="Orange" />
            <GradientStop Offset="0.7" Color="Red" />
            <GradientStop Offset="1" Color="DarkRed" />
        </LinearGradientBrush>
    </Button.Background>
</Button>
```
```

> **注意** 在示例中设置内容时，既没有使用 `Content` 属性，也没有使用 `Button.Content` 元素来编写内容；相反，内容直接作为子值写入 `Button` 元素。这是因为 `Button` 类的基类（`ContentControl`）应用了 `ContentProperty` 属性 `[ContentProperty("Content")]`。此属性将 `Content` 属性标记为 `ContentProperty`。这样 XAML 元素的直接子元素就会应用于 `Content` 属性。

## 使用 XAML 中的集合

在包含 `Person` 元素的 `ListBox` 中，你已经看到了 XAML 中的集合。在 `ListBox` 中，项已直接定义为子元素。此外，`LinearGradientBrush` 包含 `GradientStop` 元素的集合。这是因为基类 `ItemsControl` 将 `ContentProperty` 属性设置为类的 `Items` 属性，而 `GradientBrush` 基类将 `ContentProperty` 属性设置为 `GradientStops`。

以下示例显示了一个较长的版本，它通过直接设置 `GradientStops` 属性并将其子元素定义为 `GradientStopCollection` 元素来定义背景：

```
<Button Click="OnButtonClick">
    Click Me!
    <Button.Background>
        <LinearGradientBrush StartPoint="0.5, 0.0" EndPoint="0.5, 1.0">
            <LinearGradientBrush.GradientStops>
                <GradientStopCollection>
                    <GradientStop Offset="0" Color="Yellow" />
                    <GradientStop Offset="0.3" Color="Orange" />
                    <GradientStop Offset="0.7" Color="Red" />
                    <GradientStop Offset="1" Color="DarkRed" />
                </GradientStopCollection>
            </LinearGradientBrush.GradientStops>
        </LinearGradientBrush>
    </Button.Background>
</Button>
```

在 WPF 中，要定义数组，可以使用 `x:Array` 扩展。`x:Array` 扩展具有 `Type` 属性，可让你指定数组项的类型：

```
<Window.Resources>
    <x:Array Type="datalib:Person" x:Key="personArray">
        <datalib:Person FirstName="Stephanie" LastName="Nagel" />
        <datalib:Person FirstName="Matthias" LastName="Nagel" />
    </x:Array>
</Window.Resources>
```

## 依赖属性

XAML 使用依赖属性进行数据绑定、动画、属性更改通知、样式等。依赖属性的原因是什么？假设你创建一个包含 100 个 int 类型属性的类，并在单个表单上实例化该类 100 次。需要多少内存？因为 int 的大小为 4 字节，结果为 4 × 100 × 100 = 40,000 字节。你是否已经查看过 XAML 元素的属性？由于庞大的继承层次结构，XAML 元素定义了数百个属性。属性类型不是简单的 int 类型，而是更复杂的类型。我想你能想象到此类属性会消耗大量内存。然而，通常你只更改其中几个属性的值，而大多数属性保持其默认值，这些默认值对所有实例都是通用的。

