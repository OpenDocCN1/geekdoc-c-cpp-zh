
在上述代码片段中，`Height`、`Name` 和 `Content` 属性是使用属性元素语法设置的。这些属性被指定为 XAML 元素，并作为 `Button` 元素的子元素。在此以及 WPF 控件的许多其他情况下，`Content` 属性取代了 Windows Forms 应用程序中存在的 `Text` 属性。

此时，您可能想知道究竟是将属性设置为特性还是元素。请注意，这两种方法会产生相同的输出。然而，在希望 XAML 代码清晰简洁的情况下，可以将属性设置为特性。另一方面，如果属性是复杂对象类型（如枚举），则可以使用属性元素语法，这会产生更长的 XAML 代码。

> **注意**
>
> 在 WPF 中，属性值可以是任何类型的对象，而不一定是包含在双引号内的字符串类型。对于分配给属性的非字符串值，XAML 解析器会自动执行类型转换，该转换由 `TypeConverter` 类的实例（即类型转换器）执行。请注意，并非所有属性都支持类型转换，对于此类属性，设置不正确的值可能会导致错误。您可以使用属性元素语法来防止任何错误的执行。

## 标记扩展

到目前为止，WPF 属性都是使用直接和显式值设置的。然而，在某些情况下，您可能不希望将属性设置为字符串或数值，而是希望将属性设置为对特定对象的引用。针对这种情况，WPF 提供了标记扩展。标记扩展是一种将属性值设置为对象引用的方法。它还允许您将属性的值分配延迟到运行时，或将属性绑定到某个值。

标记扩展提供了一种更简单、灵活且高效的方式，通过特性以及属性元素语法向属性赋值。在 WPF 中，有多个标记扩展类可帮助您将属性设置为不同类型的值。标记扩展类继承自 `System.Windows.Markup.MarkupExtension` 类，并扩展了不同类型的标记扩展。表 9.8 列出了 XAML 中可用的不同标记扩展类：

### 表 9.8：XAML 中的标记扩展类

| 标记扩展类 | 说明 |
| --- | --- |
| `BindingBase` | 允许您为给定属性指定数据绑定值。 |
| `TemplateBindingExtension` | 允许您指定控件的属性值，该值指定给其控件模板。 |
| `StaticResourceExtension` | 允许您指定一个现有资源，该资源有助于确定属性的值。 |
| `DynamicResourceExtension` | 允许您通过将给定资源的引用延迟到运行时来设置属性值。 |
| `RelativeSource` | 允许您为绑定属性指定相对源。换句话说，它指定绑定源相对于绑定目标的位置。 |
| `ArrayExtension` | 允许您创建 XAML 对象的数组。 |
| `NullExtension` | 允许您将 `null` 值设置为属性。 |
| `StaticExtension` | 允许您将静态数据成员指定为属性的值。 |
| `TypeExtension` | 允许您为指定数据类型指定 `Type` 对象。 |

#### 注意

> 标记扩展类以单词 `Extension` 作为后缀。例如，`StaticResourceExtension` 是一个标记扩展类的名称。当您使用标记扩展类来设置属性值时，会省略单词 `Extension`。此外，以 `x:` 为前缀的标记扩展类属于 XAML 命名空间，而不以 `x:` 为前缀的标记扩展类存在于默认的 WPF 命名空间中。

如前所述，标记扩展类派生自 `MarkupExtension` 类，该类包含 `ProvideValue()` 方法。此方法负责在评估标记扩展后返回要分配给属性的对象。`ProvideValue()` 方法返回的对象取决于您提供给标记扩展的输入。输入传递给标记扩展类的带参数的非默认构造函数。

标记扩展的特征在于其语法与 XAML 内容的其余部分非常不同。您可以将标记扩展作为特性或属性元素提供。如果要将标记扩展作为特性提供，则需要将其括在花括号（`{ }`）中。左花括号后面是标记扩展类的字符串标记。字符串标记后面是空格，然后是标记扩展的输入。考虑以下代码片段：

```xml
<Button Margin="100" Name="button1" Content="welcome" Style="{StaticResource mybackground}"/>
```

在上述代码片段中，`Button` 元素中使用了 `StaticResource` 标记扩展来为其 `Style` 属性设置值。当评估标记扩展时，`mybackground` 被传递给 `StaticResourceExtension` 类的非默认构造函数。

如果要将标记扩展作为属性元素提供，则需要像任何其他 XAML 元素一样将其括在尖括号（`< >`）中。标记扩展成为属性的子元素。您将在本书后面学习更多关于各个标记扩展的内容。

让我们在下一节中探讨 WPF 属性。

## WPF 属性

在本章前面，您简要了解了 WPF 的属性以及如何通过 XAML 特性和元素来实现它们。属性在 WPF 中具有重要意义，因为它们易于使用且易于验证。WPF 类和 XAML 元素具有全面的属性集合，您可以使用这些属性来操作类和元素。除了传统的 CLR 属性外，WPF 还包括依赖属性和附加属性。

### 依赖属性

在本章前面，您简要了解了 `DependencyObject` 和 `DependencyProperty` 类。这些类在 WPF 属性系统中起着关键作用。WPF 属性系统允许您通过将现有 CLR 属性支持为依赖属性来扩展它们。依赖属性是 WPF 特有的，指的是那些依赖各种因素或输入（如数据绑定、动画、资源和样式）来确定其值的属性。大多数 WPF 属性都是依赖属性，因为它们支持许多复杂和高级的功能。

WPF 类提供了各种依赖属性。依赖属性可以分为以下几类：

- 只读依赖属性 – 指只读且无法修改的依赖属性。当您希望依赖属性的值只设置一次时，只读依赖属性非常有用。当您希望某个值仅受一个输入影响而不受其他输入影响时，也可以使用只读依赖属性。
- 集合类型依赖属性 – 指其值为集合类型的依赖属性。

所有依赖属性都是 `DependencyProperty` 类的实例。该类通过允许您创建其对象并注册到 WPF 属性系统来支持 CLR 属性。`DependencyProperty` 类包含几个属性和方法，可帮助您在 WPF 中实现和使用依赖属性。表 9.9 列出了 `DependencyProperty` 类的值得注意的属性：

#### 表 9.9：DependencyProperty 类的值得注意的属性

| 属性 | 说明 |
| --- | --- |
| `DefaultMetadata` | 检索特定依赖属性的默认元数据。 |
| `GlobalIndex` | 检索唯一标识依赖属性的索引。该索引会自动创建和分配。 |
| `Name` | 检索特定依赖属性的名称。 |
| `OwnerType` | 检索在其中创建和注册给定依赖属性的对象类型。 |
| `PropertyType` | 检索给定依赖属性的值类型。 |
| `ReadOnly` | 允许您指定依赖属性是否为只读。 |
| `ValidateValueCallback` | 检索特定依赖属性的验证回调的名称。 |

表 9.10 列出了 `DependencyProperty` 类的值得注意的方法：

#### 表 9.10：DependencyProperty 类的值得注意的方法

| 方法 | 说明 |
| --- | --- |
| `AddOwner` | 允许您为现有依赖属性添加另一个所有者 |
| `GetMetadata` | 检索特定依赖属性的元数据 |
| `IsValidType` | 允许您检查给定值是否可接受，具体取决于依赖属性或其任何派生类型的类型 |
| `IsValidValue` | 允许您检查给定值是否可接受，具体取决于依赖属性的类型，并且还位于可接受的值范围内 |
| `OverrideMetadata` | 当依赖属性存在于另一个类型时，允许您提供替代元数据 |
| `Register` | 允许您向 WPF 属性系统注册依赖属性 |

#### 表 9.10：DependencyProperty 类的注目方法

| 方法 | 描述 |
| --- | --- |
| `RegisterAttached` | 允许你使用 WPF 属性系统注册一个附加属性 |
| `RegisterAttachedReadOnly` | 允许你注册一个只读附加属性 |
| `RegisterReadOnly` | 允许你注册一个只读依赖属性 |
| `ToString` | 检索依赖属性的字符串等价物 |

在 WPF 中工作时，你可以使用众多属性。这些属性大多数是依赖属性，尽管你可以像使用常规 CLR 属性一样访问和使用它们。如前所述，依赖属性是 `DependencyProperty` 类的对象实现，但它们被包装为 CLR 属性以便于轻松便捷地访问。你可以通过属性或属性元素语法在 XAML 中使用依赖属性，如以下代码片段所示：

```xml
<Button Height="25" Width="150" Name="button1" Background="Orange">Dependency Property</Button>
```

在前面的代码片段中，`Height`、`Width`、`Name` 和 `Background` 属性是 `Button` 类的依赖属性。你也可以在代码隐藏文件中设置这些属性，如以下代码片段所示：

```csharp
Button button1 = new Button();
button1.Height = 25;
button1.Width = 150;
button1.Background = Brushes.Orange;
```

让我们在依赖属性的上下文中学习以下内容：

- 依赖属性值的优先级
- 属性值继承
- 依赖属性验证和强制回调
- 依赖属性元数据
- 自定义依赖属性

#### 依赖属性值的优先级

如你所知，依赖属性的值受各种因素或输入的影响。例如，依赖属性的值可以通过对样式资源的引用、数据绑定或来自父元素来设置。这就是为什么确定为依赖属性实际设置哪个值变得至关重要。在这种情况下，依赖属性的优先级变得必不可少。表 9.11 列出了根据输入类型分配依赖属性的优先级（从高到低）：

#### 表 9.11：依赖属性的最高到最低优先级

| 输入 | 描述 |
| --- | --- |
| 属性强制 | 应用通过属性强制设置的值。 |
| 动画 | 应用通过正在运行的动画设置的值。 |
| 本地值 | 应用直接在 XAML 或代码隐藏文件中设置的值。 |
| `TemplatedParent` 元素 | 应用通过控件或数据模板的 `Setter` 属性设置的值。 |
| 样式 | 应用通过 `Style` 属性隐式设置的值。 |
| 样式触发器 | 应用通过非默认样式触发器设置的值。 |
| 模板触发器 | 应用通过模板触发器设置的值。 |
| 样式设置器 | 应用通过样式的 `Setter` 属性设置的值。 |
| 主题样式 | 应用通过默认主题样式设置的值。在默认样式中，通过触发器设置的值的优先级高于通过默认样式的 `Setter` 属性设置的值。 |
| 继承值 | 应用通过属性值继承设置的值，即值从父元素继承。 |
| 元数据值 | 应用通过依赖属性的属性元数据设置的值。 |

让我们举一个例子来演示依赖属性值的优先级是如何工作的。考虑清单 9.5 中给出的代码：

**清单 9.5：演示依赖属性值的优先级**

```xml
<Window x:Class="PrecedenceDependencyProperty.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
    <Window.Resources>
        <Style TargetType="Button">
            <Setter Property="Background" Value="Green"/>
            <Style.Triggers>
                <Trigger Property="IsMouseOver" Value="True">
                    <Setter Property="Background" Value="Red"/>
                </Trigger>
            </Style.Triggers>
        </Style>
    </Window.Resources>
    <Grid>
        <Button Name="button1" Height="25" Margin="50" Content="Button1" Background="Orange" VerticalAlignment="Top"/>
        <Button Name="button2" Height="50" Margin="20" Content="Button2" VerticalAlignment="Center"/>
    </Grid>
</Window>
```

在清单 9.5 中，你可以看到名为 `PrecedenceDependencyProperty` 的独立 WPF 应用程序的 XAML 代码。该应用程序的窗口有一个样式资源，该资源应用于应用程序中的所有按钮。在样式资源中，按钮的依赖属性 `Background` 被设置为 `Green`。样式资源还包含一个触发器，当你将鼠标悬停在按钮上时，该触发器会将 `Background` 属性设置为 `Red`。

如清单 9.5 所示，网格有两个按钮，名为 `button1` 和 `button2`。`button1` 的 `Background` 属性被设置为 `Orange`。由于本地设置的值的优先级高于样式资源；因此，`button1` 的 `Background` 属性为 `Orange` 而不是 `Green`。然而，`button2` 没有直接将 `Background` 属性设置为本地值；因此，它的有效值为 `Green`。此外，当你将鼠标悬停在 `button2` 上时，`button2` 的 `Background` 属性被设置为 `Red`。这是因为在样式资源中定义的样式触发器的优先级高于样式设置器（将 `Background=Green`）。

> **注意**
>
> 你将在第 10 章《使用 WPF 4.0 控件、资源、样式、模板和命令》中详细了解样式、触发器和模板。

#### 属性值继承

如你所知，WPF 应用程序中的元素被视为层次树中的节点，一个元素嵌套在另一个元素内部。在大多数情况下，元素的属性也适用于其子元素。现在，假设你必须在元素上设置依赖属性的值，并且希望此值也适用于子元素。在这种情况下，你需要启用属性值继承，它指的是元素继承其父元素上注册的依赖属性值的过程。属性值继承在 WPF 中默认未启用。但是，要启用属性值继承，你需要更改属性元数据。你将在本章后面学习有关属性元数据的内容。

#### 依赖属性验证和强制回调

WPF 还提供验证回调来验证依赖属性的值。验证回调可以在依赖属性的值以编程方式更改并且属性元数据被覆盖时调用。验证回调适用于检查特定值是否在特定范围内。

验证回调是静态方法，它接受一个对象作为其参数并返回一个布尔值，表示该值的有效性。如果该值对依赖属性有效且可接受，则返回 `true`；否则返回 `false`。如果验证回调返回 `false`，则会发生异常。`ValidateValueCallback` 委托采用验证回调的参数，它表示依赖属性的验证回调。该委托本身在注册依赖属性时作为参数提供。验证回调方法的语法如下：

```csharp
public static type validationCallbackMethod(object value)
{
    //validation logic
}
```

在前面的语法中：

- `public`、`static`、`object` — 表示 C# 关键字
- `type` — 表示依赖属性的类型
- `validationCallbackMethod` — 表示验证回调方法的名称，该名称作为参数传递给 `ValidateValueCallback` 委托
- `value` — 表示要验证的值

你还可以通过强制回调将依赖属性的值强制为特定值或值范围。你可能还希望依赖属性的值根据其他属性的变化而变化。在这种情况下，你可以连同强制回调一起使用属性更改回调。强制和依赖属性的变化被实现为静态方法，它们分别作为 `CoerceValueCallback` 和 `PropertyChangedCallback` 委托的参数在指定属性元数据时传递。请注意，如果强制的建议值不被依赖属性接受，则回调方法返回一个特殊值，称为 `UnsetValue`。在这种情况下，提出的建议值将被丢弃，并且属性被设置回原始值。

强制值回调方法的语法如下：

```csharp
private static object coerceCallbackMethod(DependencyObject dObject, object value)
{
    //coercion logic
}
```

在前面的语法中：

- `private`、`static`、`object`、`DependencyObject` — 表示 C# 关键字
- `coerceCallbackMethod` — 表示强制回调方法的名称，该名称作为参数传递给 `CoerceValueCallback` 委托
- `dObject` — 表示依赖属性的所有者
- `value` — 表示要验证然后强制的值

属性更改回调方法的语法如下：

```csharp
private static void propertyChangedMethod(DependencyObject dObject,
    DependencyPropertyChangedEventArgs eArgs)
{
    //property changed logic
}
```

在前面的语法中：

- `private`、`static`、`void`、`DependencyObject`、`DependencyPropertyChangedEventArgs` – 表示 C# 关键字
