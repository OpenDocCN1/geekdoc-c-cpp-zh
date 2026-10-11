
```
<Trigger IsPressed="True">
  <Setter TargetName="ellipseLeftHighlight" Property="Opacity" Value="0"/>
  <Setter TargetName="ellipseRightHighlight" Property="Opacity" Value="0.75"/>
  <Setter TargetName="content" Property="BitmapEffect" Value="StaticResource bmePressed"/>
</Trigger>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_316_0.png)

### EllipseButton (椭圆按钮)

此代码使用一些 `Setter` 执行以下操作：

- 通过设置 `Opacity = 0` 隐藏左上角高亮。
- 通过设置 `Opacity = 0.75` 显示右下角高亮。
- 为 `ContentPresenter` 提供名为 `bmePressed` 的 `OuterGlowmapEffect`，该效果定义在模板的 `Resources` 部分，它比 `MouseOver` 效果具有更大的光晕（Glow），因此 `ContentPresenter` 的光晕更大。对比图 15-10 和 15-11 就可以看到差异。

后续代码中模板的其他触发器工作原理类似：

```
<Trigger Property="IsDefault" Value="True">
  <Setter TargetName="content" Property="Opacity" Value="0.15"/>
  <Setter TargetName="edgeHighlight" Property="Stroke" Value="StaticResource brDefaultEdgeHighlight"/>
</Trigger>
<!-- Default -->
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_316_1.png)

```
<Trigger Property="IsDefault" Value="False">
  <Setter TargetName="edgeHighlight" Property="Stroke" Value="StaticResource brEdgeHighlight"/>
</Trigger>
<!-- Not defaulted. -->
```

```
<Trigger Property="IsEnabled" Value="False">
  <Setter TargetName="content" Property="Opacity" Value="0.6"/>
</Trigger>
<!-- Disabled. This comes last so it gets precedence. -->
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_317_0.png)

这些触发器非常直观，为控件提供新的 `Stroke`（描边）值并调整 `Opacity`（不透明度）值。

## 模板技巧 3-

- 使用 `BlurEffect` 使对象看起来具有三维感（带有模糊高亮的边缘）
- 使用 `Opacity 0` 使半透明高亮
- 使用颜色变为透明的画刷使高亮消失
- 使用从透明变为颜色的画刷使其在多处可见
- 为不同状态使用不同的画刷（普通与默认的高亮）
- 为不同状态使用不同的 `BitmapEffects`（`MouseOver` 的较小光晕和 `Pressed` 的较大光晕）
- 对画刷变换进行动画处理

## 研究模板

为了有效地构建模板，你需要了解控件为你提供了什么，以及你需要为其提供什么。你还需要确定控件提供了哪些事件，以便知道如何让它采取行动。

例如，WPF 提供了一系列事件，包括 `MouseEnter`、`MouseOver`、`MouseLeftDown`、`Pressed` 和 `Click`。如果你正在编写按钮模板，可以使用哪些事件来更改按钮的外观？按钮为你提供了哪些属性，哪些是你需要实现的？

之前的节描述的按钮模板使用了 `MouseOver`、`IsPressed`、`IsEnabled`、`IsFocused` 和 `IsDefault` 属性。无论向模板中添加什么控件，`Button` 类都定义了基本的按钮行为。

正如本章前面的“模板绑定”部分所述，模板还可以读取底层控件提供的某些属性值。例如，`Button` 类提供了 `Background`、`BorderBrush` 和 `BorderThickness` 属性，模板可以通过模板绑定读取这些属性。`Button` 还继承了 `Width` 和 `Height` 等属性，你也可以通过模板绑定读取。

那么，如何学习可用的属性和模板？

很好的来源是微软的“Control Styles and Templates”网页（`mdn.microsoft.com/cc2875(vs.9).aspx`）。该页面提供了指向其他描述可用功能的链接。

例如，“Button Styles and Templates”页面列出了按钮的状态和属性，并告诉如何获取它们。例如，`Pressed` 状态（可以通过 `IsPressed` 属性读取）告诉我们按钮何时被按下。

这些网页还显示了控件使用的默认模板。按钮控件的默认模板有 84 行，且相当复杂。有些则更长、复杂得多。

`ShowTemplate` 程序使用以下代码来显示 `Target` 控制的模板：

```csharp
private void btnTemplate_Click(object sender, RoutedEventArgs e)
{
    XmlWriterSettings writer_settings = new XmlWriterSettings();
    writer_settings.Indent = true;
    writer_settings.IndentChars = " ";
    writer_settings.NewLineOnAttributes = true;

    StringBuilder sb = new StringBuilder();
    XmlWriter xml_writer = XmlWriter.Create(sb, writer_settings);
    XmlWriter.Save(Target.Template, xml_writer);

    txtResult.Text = sb.ToString();
}
```

`ShowTemplate`

这段代码的关键在于 `XmlWriter` 类，它的方法可以从像控件或模板这样的 WPF 对象中提取 XAML。

代码开始时初始化一个 `XmlWriterSettings` 对象，以使写入器生成格式化良好的输出。如果你不这样做，代码将以单行 XAML 的形式出现，没有换行符或缩进。

程序随后创建了一个 `StringBuilder` 来存储结果文本。它使用写入器设置来创建一个附加到 `StringBuilder` 的 `XmlWriter`。

代码调用 `XmlWriter` 类的静态 `Save` 方法，将 `Target` 控件 `Template` 属性的 XAML 表示写入 `StringBuilder`。

程序最后通过在其 `TextBox` `txtResult` 中显示结果而结束。

在找到控件的默认模板后，你可以修改它以创建你自己的模板，从而更改控件的外观。这让你的模板行为与默认模板完全相同，但在你想要更改的地方除外。

## 总结

属性和样式允许你以浅层的方式更改控件的外观。模板允许你更根本地更改控件，改变组成控件的各个，并改变它对事件和属性值变化的响应方式。通过使用模板，你可以为你的应用程序提供独特的视觉和感受。

下一章将解释与样式和模板紧密相关的两个主题：主题（Themes）和皮肤（Skins）。皮肤允许应用程序更改其整个外观，有时甚至是根本性的改变。它们允许你根据自己的即时需求或心情来更改应用程序。

主题在控件、窗口甚至独立的应用程序之间提供了一种统一的外观。通过提供共同的外观和感受，主题可以让即使是不相关的程序看起来也像属于同一个系统。

# 第16 章

## 主题与皮肤

WPF 允许你构建具有引人注目的、独特外观的应用程序。通过使用阴影、部分透明和透明掩罩等相对简单的技术，你可以创建一个引人注目的界面，为即使是最普通的应用程序增添趣味和兴奋感。

属性允许你更改控件的外观。它们允许你更改视觉特征，如控件的颜色、大小、位置和内容。资源和样式允许你封装这些更改，以便你将它们同时应用于许多控件。

模板允许你通过更改构成控件的部件来改变控件的行为。它们允许你从根本上更改按钮、`ListBox`、菜单和其他控件的外观和行为，同时允许它们执行其核心功能。

主题和皮肤将所有想法整合在一起，允许你轻松地更改整个应用程序的外观和行为，以适应用户的需求和心情。

## 主题

有些开发者交替使用主题和皮肤，但我做的区分是：皮肤适用于单个应用程序（或应用程序的一部分），而主题则适用于多个应用程序。

更准确地说，主题是一个统一的方案，有助于确定多个应用程序的外观和行为。最常见的主题是由 Windows 提供的。Windows 7 提供了以下主题：

- `Aero`
- `Classic`
- `Luna`（包含 `Homestead`, `Metallic` 和 `Normal` 版本）
- `Royale`

### 使用系统主题

图 16-1 所示的 `ShowThemes` 示例程序显示了使用 Windows 7 自带主题的控件。差异非常微妙，你需要仔细观察才能看到每个主题中的变化。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_321_0.png)

图 16-1

如果你不使用属性、样式或模板来更改控件的外观或行为，它将使用系统当前主题定义的值。在图 16-1 中，你可以看到“默认”组中的控件与使用 `Aero` 主题的控件具有相同的外观。这是因为在我运行程序时，系统选择了 `Aero`。

要更改 Windows 7 中的系统主题，请打开“控制面板”。在“外观和个性化”下点击“更改主题”。在图 16-2 所示的对话框中，点击你想要的主题。

在截取图 16-1 的屏幕后，我按照这些步骤在不关闭 `ShowThemes` 程序的情况下将系统主题更改为 Windows Classic。程序自动检测到系统主题的变化，并相应地重绘了自己。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_321_1.png)

FIGURE 16-2

图 16-3 显示了结果。如果你仔细看，你会发现“默认”组中的控件与使用 Classic 主题的控件外观一致。

主题 | 285

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_322_0.png)

图 16-3

如果你仔细比较 16-1 和 16-3，你会发现即使是默认主题，程序看起来也略有不同。

### 使用特定主题

通常，你不需要使用属性、样式或模板来更改控件的外观或行为，它会使用系统当前主题的值。

> 更改主题
>
> 这种技术在测试应用程序在特定主题下的外观时，可能比强制用户使用主题更有用。
>
> 用户用户可能由于某些原因选择特定主题。例如，视力受损的用户可能会选择高对比度主题来让程序更容易看。
>
> 如果你更改主题，他们可能无法使用你的应用程序。

要在 Visual Studio 中使用特定主题，请新建 WPF 项目。在引用选项卡上选择你想使用的的主题并点击确定。图 16-4 显示了选择了 `Aero`、`Classic`、`Luna` 和 `Royale` 主题的引用对话框。

接下来，在资源字典中使用 `MergedDictionaries` 对象来加载主题。该主题将适用于任何应该修改的控件。

# 286 | 第16 章 主题与皮肤

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_323_0.png)

FIGURE 16-4

例如，下面的代码显示了程序如何使用 `Luna Metallic` 主题。 16-1 和 16-3 中的每组控件都包含在 `StackPanel` 中。每个 `StackPanel` 一个加载其主题的 `ResourceDictionary`。

```xml
<StackPanel>
  <StackPanel.Resources>
    <ResourceDictionary>
      <ResourceDictionary.MergedDictionaries>
        <ResourceDictionary Source="/PresentationFramework.Luna;component/themes/luna.metallic.xaml" />
      </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
  </StackPanel.Resources>
  <Label Style={StaticResource Style} Content="luna.metallic"/>
  <Button Margin="10" Content="Click Me"/>
  <CheckBox Margin="10" Content="Check Me"/>
  <RadioButton Margin="10" Content="Press Me"/>
</StackPanel>
```

可在 Wprox.com 下载

`ShowThemes`

注意 `ResourceDictionary.Source` 属性的特殊语法。`PresentationFramework Luna` 是包含库的 WPF，而 `Source` 的其余部分给出了库中的主题。

### 主题限制

我在让 Expression Blend 使用特定主题方面一直不太顺利。它似乎在寻找 `ResourceDictionary` 的 `Source` 属性所使用的 DLL 文件时遇到困难。我在运行编译后的可执行文件也同样不太顺利。

这些问题可能会在后续版本中得到修复，但目前我使用这种技术在带有 Visual Studio 的程序中查看程序在不同主题下的外观。如果你发现了如何让这些在 Expression Blend 中运行的方法，请发送邮件至 `RodStephens@vb-helper.com`，我会将你的解决方案发布在书籍的网页上。

## 皮肤 (SKINS)

主题允许程序自动更改以匹配系统其他部分的显示。选择特定主题可以让程序刻意地改变其外观，但通常这是没有必要的。`Luna Metallic` 和 `Aero Normal` 主题之间的差异非常微小，如果可以让程序使用系统默认主题，就没有理由强迫用户使用其中一个。

皮肤要有趣得多。皮肤是一套封装好的外观和行为，可以为应用程序（或应用程序的部分）提供独特的外观，同时允许其提供核心功能。

皮肤与主题在某些方面相似，因为它们定义了应用程序的外观和行为，但它们对应用程序外观的改变通常比图 16-1 和 16-3 所示的更大。与其统一系统上运行的所有应用程序，皮肤提供的更大变化可以使应用程序脱颖而出。皮肤区分了应用程序，让用户一眼就能区分不同的应用程序。

例如，图 16-5 和 16-6 显示了 `ResourceDictionaries` 示例程序（在第 12 章中描述）显示的两种不同外观。这两幅图中的程序是同一个，并且包含相同的控件——只是根据不同的颜色、字体等进行了微调布局。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_324_0.png)

图 16-5

# 第 16 章 主与皮肤

![](img/c9b2d394f4fc2f7e27666a0a6fa9c2f6_325_0.png)

图 16-6

接下来的章节将描述皮肤，并解释了在 WPF 中实现它们的几种方法。

> **工作量警告**
>
> 请注意，制作皮肤是一项工作量的工作！取决于你使用的技术，它可能并不复杂，但可能会非常耗时。
>
> WPF 提供了许多工具来创建吸引人的用户界面，人们很容易花费几个小时反复调整控件属性和布局，试图构建世界上最美的界面。现在将这种工作量倍增以提供多种皮肤，你可能会在一个窗口上花费几天时间，而不是“仅仅”几个小时。

### 皮肤的用途

通常，皮肤大部分是装饰性的，改变应用程序的颜色、按钮形状、表单设计、背景图片等。图 16-5 和 16-6 所示的皮肤看起来非常不同，但仅在表面如此。它们在相同的位置使用了相同的控件。

其他皮肤通常是装饰性的，用于增加程序的“酷炫因素”，而多种皮肤也可以具有合法的业务目的。

例如，在美国，8% 的男性和 0.4% 的女性有不同形式的色盲，因此在区分某些颜色时存在困难。如果你的应用程序提供多种皮肤，用户在识别信息遇到较少困难时可以更改程序使用的颜色或形状。

此外，随着普通用户群体的老龄化，必须制作应用程序来帮助老年用户。更大的字体、菜单、按钮和其他组件可以使用户理解和使用应用程序变得更容易。提供具有不同元素尺寸的多种皮肤也允许使用大屏幕的用户利用他们拥有的空间。

皮肤的另一个通常被忽视的用途是让同一个应用程序为不同的目的使用不同的界面。例如，假设你正在编写一个订单输入系统。不同类型的用户需要在な查看订单的不同部分。

当订单最初创建时，订单录入员需要了解有关客户和订单的所有信息，可能还有支付信息（取决于你与客户的安排）。随后，发货员在包装客户订单时只需要知道订购物品和客户的收货地址，不需要支付信息或之前的订单历史。程序可能会自动向客户发送发票，但如果客户来电提问，账单员可能需要了解客户的支付方式以及过去的订单。

你可以使用不同的皮肤来满足这些不同用户的需求。订单录入员皮肤允许用户定位客户数据并输入新订单信息。发货员皮肤将显示当前订单信息和客户收货地址，同时隐藏支付信息和之前的订单历史。

`OrderTracking` 示例程序为不同类型的用户显示了四种不同的界面。图 16-7 显示了程序针对经理、账单员、订单录入员和发货员的皮肤。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_326_0.png)

图 16-7

以下 XML 代码展示了 `OrderTracking` 程序的工作原理：
