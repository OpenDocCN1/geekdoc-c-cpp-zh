

ShowTemplate 程序使用以下代码来显示 Target 控制的模板：

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

ShowTemplate

这段代码的关键在于 `XmlWriter` 类，它的方法可以从像控件或模板这样的 WPF 对象中提取 XAML。

代码开始时初始化一个 `XmlWriterSettings` 对象，以使写入器生成格式化良好的输出。如果你不这样做，代码将以单行 XAML 的形式出现，没有换行符或缩进。

程序随后创建了一个 `StringBuilder` 来存储结果文本。它使用写入器设置来创建一个附加到 `StringBuilder` 的 `XmlWriter`。

代码调用 `XmlWriter` 类的静态 `Save` 方法，将 Target 控件 `Template` 属性的 XAML 表示写入 `StringBuilder`。

程序最后通过在其 TextBox `txtResult` 中显示结果而结束。

在找到控件的默认模板后，你可以修改它以创建你自己的模板，从而更改控件的外观。这让你的模板行为与默认模板完全相同，但在你想要更改的地方除外。

## 总结

属性和样式允许你以浅层的方式更改控件的外观。模板允许你更根本地更改控件，改变组成控件的各个，并改变它对事件和属性值变化的响应方式。通过使用模板，你可以为你的应用程序提供独特的视觉和感受。

下一章将解释与样式和模板紧密相关的两个主题：主题（Themes）和皮肤（Skins）。皮肤允许应用程序更改其整个外观，有时甚至是根本性的改变。它们允许你根据自己的即时需求或心情来更改应用程序。

主题在控件、窗口甚至独立的应用程序之间提供了一种统一的外观。通过提供共同的外观和感受，主题可以让即使是不相关的程序看起来也像属于同一个系统。

# 第16 章

## 主题与皮肤

WPF 允许你构建具有引人注目的、独特外观的应用程序。通过使用阴影、部分透明和透明掩罩等相对简单的技术，你可以创建一个引人注目的界面，为即使是最普通的应用程序增添趣味和兴奋感。

属性允许你更改控件的外观。它们允许你更改视觉特征，如控件的颜色、大小、位置和内容。资源和样式允许你封装这些更改，以便你将它们同时应用于许多控件。

模板允许你通过更改构成控件的部件来改变控件的行为。它们允许你从根本上更改按钮、ListBox、菜单和其他控件的外观和行为，同时允许它们执行其核心功能。

主题和皮肤将所有想法整合在一起，允许你轻松地更改整个应用程序的外观和行为，以适应用户的需求和心情。

# 主题

有些开发者交替使用主题和皮肤，但我做的区分是：皮肤适用于单个应用程序（或应用程序的一部分），而主题则适用于多个应用程序。

更准确地说，主题是一个统一的方案，有助于确定多个应用程序的外观和行为。最常见的主题是由 Windows提供的。Windows 7 提供了以下主题：

- Aero
- Classic
- Luna（包含 Homestead, Metallic 和 Normal 版本）
- Royale

## 使用系统主题

图 16-1 所示的 ShowThemes 示例程序显示了使用 Windows 7 自带主题的控件。差异非常微妙，你需要仔细观察才能看到每个主题中的变化。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_321_0.png)

图 16-1

如果你不使用属性、样式或模板来更改控件的外观或行为，它将使用系统当前主题定义的值。在图 16-1 中，你可以看到“默认”组中的控件与使用 Aero 主题的控件具有相同的外观。这是因为在我运行程序时，系统选择了 Aero。

要更改 Windows 7 中的系统主题，请打开“控制面板”。在“外观和个性化”下点击“更改主题”。在图 16-2 所示的对话框中，点击你想要的主题。

在截取图 16-1 的屏幕后，我按照这些步骤在不关闭 ShowThemes 程序的情况下将系统主题更改为 Windows Classic。程序自动检测到系统主题的变化，并相应地重绘了自己。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_321_1.png)

FIGURE 16-2

图 16-3 显示了结果。如果你仔细看，你会发现“默认”组中的控件与使用 Classic 主题的控件外观一致。

主题 | 285

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_322_0.png)

图 16-3

如果你仔细比较 16-1 和 16-3，你会发现即使是默认主题，程序看起来也略有不同。

## 使用特定主题

通常，你不需要使用属性、样式或模板来更改控件的外观或行为，它会使用系统当前主题的值。

> 更改主题
> 这种技术在测试应用程序在特定主题下的外观时，可能比强制用户使用主题更有用。
> 用户用户可能由于某些原因选择特定主题。例如，视力受损的用户可能会选择高对比度主题来让程序更容易看。
> 如果你更改主题，他们可能无法使用你的应用程序。

要在 Visual Studio 中使用特定主题，请新建 WPF 项目。在引用选项卡上选择你想使用的的主题并点击确定。图 16-4 显示了选择了 Aero、Classic、Luna 和 Royale 主题的引用对话框。

接下来，在资源字典中使用 MergedDictionaries 对象来加载主题。该主题将适用于任何应该修改的控件。

# 286 | 第16 章 主题与皮肤

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_323_0.png)

FIGURE 16-4

例如，下面的代码显示了程序如何使用 Luna Metallic 主题。 16-1 和 16-3 中的每组控件都包含在 StackPanel 中。每个 StackPanel 一个加载其主题的 ResourceDictionary。

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

ShowThemes

注意 ResourceDictionary.Source 属性的特殊语法。PresentationFramework Luna 是包含库的 WPF，而 Source 的其余部分给出了库中的主题。

