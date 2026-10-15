

## 接受其他形式的用户输入

按钮和文本框并非用户与应用交互的唯一方式，WP7 SDK 还提供了其他开箱即用的控件。本节将介绍一些新控件，它们提供了更丰富、更灵活的用户输入接受方式，例如：

- 复选框（Checkbox）——iOS 中没有功能对应的原生 UIKit 复选框控件。
- 单选按钮（RadioButton）——在 iOS 中，UISegmentedControl 通常提供类似功能。
- 密码框（PasswordBox）——在 iOS 中，将 UITextField 控件的 secureTextEntry 属性设置为 YES 即可提供几乎相同的功能。
- 滑块（Slider）——在 iOS 中，UISlider 控件提供此功能，但 iOS 滑块难以自定义，且始终水平显示；而 WP7 滑块可以轻松自定义，并且无需自定义即可垂直显示。
- 超链接按钮（HyperlinkButton）——在 iOS 中实现此功能最简单的方法是创建一个可点击的标签，并为其设置样式使其看起来像超链接（例如蓝色、带下划线的文本）。

打开本章一直在使用的 MainPage.xaml 文件，将清单 8.7 中的代码添加到页面中，位于之前示例中控件的下方。我删除了一些不必要的控件，以便为新 UI 元素腾出空间（如图 8.3 所示）。

### 清单 8.7 添加新的用户输入元素

```
<CheckBox x:Name="checkBoxOne" />
<RadioButton x:Name="ChoiceOne" GroupName="DefaultGroup">
    <TextBlock Text="Radio One" />
</RadioButton>
<RadioButton GroupName="DefaultGroup">
    <TextBlock Text="Radio Two" />
</RadioButton>
<Slider x:Name="SliderOne" Minimum="0" Maximum="100" Value="20" />
<HyperlinkButton x:Name="hyperLinkButtonOne" Click="hyperLinkButtonOne_Click" Content="hyperlink!!" />
<PasswordBox x:Name="PasswordBox" />
```

添加的第一个控件是复选框，它非常简单。复选框允许用户指定布尔值，例如是否启用某个特定偏好，或者关于某些数据的特定陈述是否为真。

接下来添加的是两个单选按钮。它们允许用户在有限的可用选项集中进行选择。当用户选中组内的一个单选按钮时，其他所有按钮的状态都会被清除。若要指示哪些按钮属于同一组，只需为它们的 GroupName 属性分配相同的字符串即可。在上述代码中，我们将两个单选按钮的 GroupName 属性都赋值为 DefaultGroup。

屏幕上可以同时容纳任意多个单选按钮组，只要空间允许（或者你的审美和设计感允许）。

接下来我们添加了一个滑块，它允许用户在任意最小值和最大值之间“滑动”一个值指示器。你可以使用滑块控件提示用户选择音量级别、在策略游戏中为特定对象分配资源，甚至选择用户想要购买某物的数量。尽管滑块很简单，但它是一个强大且通用的控件，可应用于多种场景。

接下来是 HyperlinkButton。顾名思义，该控件向用户显示一些类似于浏览器中可点击超链接的文本。点击该链接时，它可以使用 NavigateUri 属性将用户导航到特定页面（Silverlight 页面，而非网页），也可以在 Click 事件中执行自定义逻辑。

最后是 PasswordBox 控件。该控件的功能与 TextBox 控件完全相同，区别在于用户输入每个字符片刻后，该字符会被替换为圆点。这种模式和风格对于网页浏览器、iPhone 和许多其他移动设备的用户来说应该非常熟悉，用户应该能轻松识别该控件的用途。但是，不要将此控件误认为内置安全机制。该控件所做的只是隐藏密码的显示；你的代码仍然可以访问此文本框的内容，并且没有自动加密。你需要自行编写密码安全代码。本书后面将介绍一些保护 WP7 应用程序的技巧和方法。

![](img/04a00d46bb1059867d95707babd62ee7_104_0.png)

图 8.3 更多的用户输入元素。

## 显示图像

为应用增添趣味的最简单方法之一就是使用图像。在 UI 中精心使用小而精致的图像，甚至在 UI 中间使用大图像，都能为应用增色不少，并且往往是使你的应用超越竞争对手的因素。

在 iOS 中使用图像时，开发者通常使用 UIImageView 类。此类派生自 UIView，其唯一用途就是显示图像。同样，Windows Phone 7 开发者可以使用 Silverlight 的 Image 控件，无论通过编程方式还是通过 XAML 标记，该控件都非常易于使用。

以下代码展示了一个完全通过 XAML 配置的基本图像控件。

```
<Grid x:Name="myGrid" Width="150" Height="150" Background="White">
    <Image x:Name="myImage"
        Source="/images/SuperAwesomeScreen.jpg" Stretch="Fill" />
</Grid>
```

暂时不必担心 Grid 元素，我们稍后会介绍它。在上述代码中，Image 控件被配置为以 Fill 拉伸模式显示名为 SuperAwesomeScreen.jpg 的 JPEG 图像。

图像的拉伸模式可以设置为 None、Fill、Uniform 或 UniformToFill。无拉伸意味着图像将按其文件的原始尺寸显示。Fill 拉伸模式意味着图像将扩展，以填满其所在的任何布局容器。在上述代码中，父级网格是 150×150，因此无论图像原始尺寸如何，都会缩放至该尺寸。使用 Fill 模式时，图像的长宽比不会保持，因此常常会扭曲原始图像。若要即使在缩放后仍保持高度和宽度之间的比例，请使用 Uniform 拉伸模式。此模式会将图像尽量拉伸至新尺寸，同时仍然保持原始长宽比。最后，UniformToFill 拉伸模式类似于 Uniform，但它允许裁剪部分图像，以更好地适配父容器。除了 Stretch 属性之外，你还可以控制图像的其他多个方面，例如 Width、Height 和 Clip，Clip 可用于赋予图像非矩形形状。

在本章一直使用的同一个 MainPage.xaml 文件中，将以下 Image 元素添加到 StackPanel 中第一个 TextBlock 控件的上方。

```
<Image x:Name="sampleImage" />
```

就这样。Stretch 属性的默认模式是 Uniform，这对我们的目的来说已经足够。现在转到 XAML 的代码隐藏文件，将超链接按钮的 Click 事件的实现改为以下内容：

```
private void hyperLinkButtonOne_Click(object sender, RoutedEventArgs e)
{
    sampleImage.Source = new BitmapImage(
        new Uri("success.jpg", UriKind.RelativeOrAbsolute));
}
```

当此代码执行时，它将告诉 Image 控件它有一个新的源。这将导致 Image 控件立即根据新内容重新绘制自身。success.jpg 文件包含在随本章附带的示例代码中，可以在图 8.4 中看到。

尽管这个示例看起来可能很简单，但这只是图像功能应用冰山一角。了解图像的源和其他属性可以在运行时完全更改，这为各种强大的功能铺平了道路，例如从互联网或应用服务器下载和缓存图像，甚至即时创建图像、显示它们，并将它们上传到应用服务器。对于图像，唯一的限制可能就是你的想象力。

![](img/04a00d46bb1059867d95707babd62ee7_106_0.png)

图 8.4 使用 Image 控件。

## 使用基本列表框

到目前为止，我们一直在处理与单个信息相关的控件，例如单张图像、单个文本框或单个按钮。列表框控件使我们能够定义模板，这些模板将用于呈现列表中的项目。该控件内置了滚动浏览项目的能力（包括显示一个

