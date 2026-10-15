

虽然通过 XAML 特性设置属性简单、简洁且直观，但 WPF 提供了另一种方式，即属性元素语法。在属性元素语法中，可以通过将属性指定为元素而不是特性来设置属性。属性元素语法使用以下语法来设置属性：

```
<element_name.property_name [attribute1_name="value1" attribute2_name="value2"...
attributeN_name="valueN"]>property_value</element_name.property_name>
```

在上述语法中，设置属性时使用了以下选项：

- element_name – 指定属性所属元素的名称
- property_name – 指定属性的名称
- attribute1_name, attribute2_name, ... attributeN_name – 指定属性可能包含的任何特性的名称
- value1, value2,... valueN – 指定特性的值
- property_value – 指定属性的值

从上述语法可以看出，属性名使用点运算符（.）限定其所属元素的名称。您可能还会注意到，属性被括在尖括号中，并具有开始和结束标签。请注意，如果属性本身具有自己的属性，则这些属性可以进一步在属性元素语法中表示。

以下代码片段显示了 Button 类的属性：

```
<Button>
  <Button.Height>23</Button.Height>
  <Button.Name>button1</Button.Name>
  <Button.Content>Welcome</Button.Content>
</Button>
```

在上述代码片段中，Height、Name 和 Content 属性是使用属性元素语法设置的。这些属性被指定为 XAML 元素，并作为 Button 元素的子元素。在此以及 WPF 控件的许多其他情况下，Content 属性取代了 Windows Forms 应用程序中存在的 Text 属性。

此时，您可能想知道究竟是将属性设置为特性还是元素。请注意，这两种方法会产生相同的输出。然而，在希望 XAML 代码清晰简洁的情况下，可以将属性设置为特性。另一方面，如果属性是复杂对象类型（如枚举），则可以使用属性元素语法，这会产生更长的 XAML 代码。

> **注意**
> 在 WPF 中，属性值可以是任何类型的对象，而不一定是包含在双引号内的字符串类型。对于分配给属性的非字符串值，XAML 解析器会自动执行类型转换，该转换由 TypeConverter 类的实例（即类型转换器）执行。请注意，并非所有属性都支持类型转换，对于此类属性，设置不正确的值可能会导致错误。您可以使用属性元素语法来防止任何错误的执行。

## 标记扩展

到目前为止，WPF 属性都是使用直接和显式值设置的。然而，在某些情况下，您可能不希望将属性设置为字符串或数值，而是希望将属性设置为对特定对象的引用。针对这种情况，WPF 提供了标记扩展。标记扩展是一种将属性值设置为对象引用的方法。它还允许您将属性的值分配延迟到运行时，或将属性绑定到某个值。

标记扩展提供了一种更简单、灵活且高效的方式，通过特性以及属性元素语法向属性赋值。在 WPF 中，有多个标记扩展类可帮助您将属性设置为不同类型的值。标记扩展类继承自 System.Windows.Markup.MarkupExtension 类，并扩展了不同类型的标记扩展。表 9.8 列出了 XAML 中可用的不同标记扩展类：

## 表 9.8：XAML 中的标记扩展类

| 标记扩展类 | 说明 |
|---|---|
| BindingBase | 允许您为给定属性指定数据绑定值。 |
| TemplateBindingExtension | 允许您指定控件的属性值，该值指定给其控件模板。 |
| StaticResourceExtension | 允许您指定一个现有资源，该资源有助于确定属性的值。 |
| DynamicResourceExtension | 允许您通过将给定资源的引用延迟到运行时来设置属性值。 |
| RelativeSource | 允许您为绑定属性指定相对源。换句话说，它指定绑定源相对于绑定目标的位置。 |
| ArrayExtension | 允许您创建 XAML 对象的数组。 |
| NullExtension | 允许您将 null 值设置为属性。 |
| StaticExtension | 允许您将静态数据成员指定为属性的值。 |
| TypeExtension | 允许您为指定数据类型指定 Type 对象。 |

## 注意

> 标记扩展类以单词 Extension 作为后缀。例如，StaticResourceExtension 是一个标记扩展类的名称。当您使用标记扩展类来设置属性值时，会省略单词 Extension。此外，以 x: 为前缀的标记扩展类属于 XAML 命名空间，而不以 x: 为前缀的标记扩展类存在于默认的 WPF 命名空间中。

如前所述，标记扩展类派生自 MarkupExtension 类，该类包含 ProvideValue() 方法。此方法负责在评估标记扩展后返回要分配给属性的对象。ProvideValue() 方法返回的对象取决于您提供给标记扩展的输入。输入传递给标记扩展类的带参数的非默认构造函数。

标记扩展的特征在于其语法与 XAML 内容的其余部分非常不同。您可以将标记扩展作为特性或属性元素提供。如果要将标记扩展作为特性提供，则需要将其括在花括号（{ }）中。左花括号后面是标记扩展类的字符串标记。字符串标记后面是空格，然后是标记扩展的输入。考虑以下代码片段：

```
<Button Margin="100" Name="button1" Content="welcome" Style="{StaticResource mybackground}"/>
```

在上述代码片段中，Button 元素中使用了 StaticResource 标记扩展来为其 Style 属性设置值。当评估标记扩展时，mybackground 被传递给 StaticResourceExtension 类的非默认构造函数。

如果要将标记扩展作为属性元素提供，则需要像任何其他 XAML 元素一样将其括在尖括号（< >）中。标记扩展成为属性的子元素。您将在本书后面学习更多关于各个标记扩展的内容。

让我们在下一节中探讨 WPF 属性。

## WPF 属性

在本章前面，您简要了解了 WPF 的属性以及如何通过 XAML 特性和元素来实现它们。属性在 WPF 中具有重要意义，因为它们易于使用且易于验证。WPF 类和 XAML 元素具有全面的属性集合，您可以使用这些属性来操作类和元素。除了传统的 CLR 属性外，WPF 还包括依赖属性和附加属性。

## 依赖属性

在本章前面，您简要了解了 DependencyObject 和 DependencyProperty 类。这些类在 WPF 属性系统中起着关键作用。WPF 属性系统允许您通过将现有 CLR 属性支持为依赖属性来扩展它们。依赖属性是 WPF 特有的，指的是那些依赖各种因素或输入（如数据绑定、动画、资源和样式）来确定其值的属性。大多数 WPF 属性都是依赖属性，因为它们支持许多复杂和高级的功能。

WPF 类提供了各种依赖属性。依赖属性可以分为以下几类：

- 只读依赖属性 – 指只读且无法修改的依赖属性。当您希望依赖属性的值只设置一次时，只读依赖属性非常有用。当您希望某个值仅受一个输入影响而不受其他输入影响时，也可以使用只读依赖属性。
- 集合类型依赖属性 – 指其值为集合类型的依赖属性。

所有依赖属性都是 DependencyProperty 类的实例。该类通过允许您创建其对象并注册到 WPF 属性系统来支持 CLR 属性。DependencyProperty 类包含几个属性和方法，可帮助您在 WPF 中实现和使用依赖属性。表 9.9 列出了 DependencyProperty 类的值得注意的属性：

表 9.9：DependencyProperty 类的值得注意的属性

| 属性 | 说明 |
|---|---|
| DefaultMetadata | 检索特定依赖属性的默认元数据。 |
| GlobalIndex | 检索唯一标识依赖属性的索引。该索引会自动创建和分配。 |
| Name | 检索特定依赖属性的名称。 |
| OwnerType | 检索在其中创建和注册给定依赖属性的对象类型。 |
| PropertyType | 检索给定依赖属性的值类型。 |
| ReadOnly | 允许您指定依赖属性是否为只读。 |
| ValidateValueCallback | 检索特定依赖属性的验证回调的名称。 |

表 9.10 列出了 DependencyProperty 类的值得注意的方法：

表 9.10：DependencyProperty 类的值得注意的方法

| 方法 | 说明 |
|---|---|
| AddOwner | 允许您为现有依赖属性添加另一个所有者 |
| GetMetadata | 检索特定依赖属性的元数据 |
| IsValidType | 允许您检查给定值是否可接受，具体取决于依赖属性或其任何派生类型的类型 |
| IsValidValue | 允许您检查给定值是否可接受，具体取决于依赖属性的类型，并且还位于可接受的值范围内 |
| OverrideMetadata | 当依赖属性存在于另一个类型时，允许您提供替代元数据 |
| Register | 允许您向 WPF 属性系统注册依赖属性 |

