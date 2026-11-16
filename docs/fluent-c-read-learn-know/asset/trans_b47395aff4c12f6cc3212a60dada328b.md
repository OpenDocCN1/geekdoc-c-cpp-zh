

## 视觉过渡

除了 VisualState 分镜之外，VisualStateManager 允许你通过将 VisualTransition 元素添加到 VisualStateGroup 的 Transitions 集合中来定义控件在状态之间如何移动。与 VisualState 类似，VisualTransition 只能包含一个 Storyboard，但该类定义了一些其他属性：

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_795_0.png)

From 和 To 属性定义控件正在过渡的视觉状态。

GeneratedDuration 在功能上与 Storyboard 的 Duration 属性相同。它定义过渡所需的时间，与 Storyboard.Transition 类似，默认值为 1 秒，这通常太长了。

GeneratedEasingFunction 采用与 Storyboard 的 EasingFunction 相同的值。

### 动动脑筋

VisualTransition 的属性与 Storyboard 的可比属性的行为类似，与 Storyboard 一样，From 和 To 属性是可选的。你能将属性设置的组合与结果匹配起来吗？

| From | To | Result |
| :--- | :--- | :--- |
| 已指定 | 已指定 | 从任何状态到指定状态 |
| 未指定 | 已指定 | 从指定状态到指定状态 |
| 已指定 | 未指定 | 从任何状态到任何其他状态 |
| 未指定 | 未指定 | 从指定状态到任何其他状态 |

如果多个 VisualTransition 都适用，你期望 WPF 会怎么做？

### 做得怎么样？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_796_0.png)

| | From | To |
|---|---|---|
| 1 | 已指定 | 已指定 |
| 2 | 未指定 | 已指定 |
| 3 | 已指定 | 未指定 |
| 4 | 未指定 | 未指定 |

- 2. 从任何状态到指定状态
- 1. 从指定状态到指定状态
- 4. 从任何状态到任何其他状态
- 3. 从指定状态到任何其他状态

如果多个 VisualTransition 都适用，你期望 WPF 会怎么做？

使用样式、资源或模板项时，WPF 总是使用最后指定的那个。

### 休息一下

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_796_1.png)

VisualStateManager 与样式和模板的一般模式以及 XAML 的一般模式非常契合，这也是我们对该主题探索的结束。在完成本章并转到 WPF 绑定之前，为什么不休息一下呢？

### 独立练习

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_797_0.png)

在上一章末尾，你编写了一个事件触发器来让按钮抖动。使用相同的技术，向示例中添加一个 VisualStateManager，以便当鼠标移到矩形按钮上时它会抖动。再向圆形按钮添加一个，使其先稍微扩大，然后收缩并改变颜色。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_797_1.png)

此按钮应扩大和收缩。

此按钮应抖动。

使用我们的控件模板示例应用程序，将控件模板作为样式移动到资源字典中。

为 TextBox 创建一个你认为能与本章开发的按钮融合的控件模板。请务必检查是否有需要包含的控件部件。

为 Button 控件模板添加可视状态支持。与控件部件一样，你不需要全部包含。由于我们的按钮没有数据绑定，你当然可以省略 ValidationStates 组，并且可能会决定其他一些组不适用。

恭喜！你已经完成了本章。在进入下一章之前，花一分钟思考一下你已经完成了什么...

列出你在本章学到的三件事：

- 1
- 2
- 3

你认为为什么需要知道这些东西才能成为 C# 程序员？

本章中有什么你觉得需要更详细理解的内容吗？如果有，你打算怎么做？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_800_0.png)

## WPF 绑定

在上一章中，我们使用了 TemplateBinding 标记扩展，将控件模板中的值设置为对象公共属性的值。

一般来说，“绑定”只是指属性的值从其他地方获取，而在使用 WPF 时，依赖属性系统会为你完成大部分工作。你告诉 WPF 你想要它做什么，无论是在 XAML 中还是在代码中，它都会处理如何实现。

模板绑定是绑定的一种特殊情况。WPF 通过 Binding 对象和 {Binding} 标记扩展提供了一种通用机制。你可以将依赖属性的值绑定到任何 .NET 对象，并且可以按需要以几乎任何方式操作绑定。

在本章中，我们将探讨 WPF 绑定的基本概念：值的来源、接收值的目标，以及将它们链接在一起的 Binding 和 View 对象。我们还将查看将一组项绑定到项控件，以及可用于格式化和导航一组项的一些技术。

绑定是 WPF 的基础，当你完成本章后，应该理解基础知识。但在 WPF 中，绑定可能是一个非常庞大且复杂的主题，我无法在一章简短的内容中让你成为数据库程序员。如果你对应用程序开发的这个领域感兴趣，你需要学习数据库理论和 ADO.NET（.NET 数据访问平台），以及可能的 Entity Framework（用于将关系数据库映射到对象的工具）。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_802_0.png)

### 将其组装在一起

WPF 绑定的基本结构简单易用且易于理解。只有三个基本组件：绑定源（Binding SOURCE），提供值的 .NET 对象；绑定目标（BINDING TARGET），接收值的依赖属性；以及链接两者的 Binding 类。

绑定源（BINDING SOURCE）可以是任何 .NET 对象。它对绑定一无所知。

Binding 类管理在源和目标之间移动值。一个 Binding 指向特定的源，但可以被多个目标使用。

任何依赖属性都可以是绑定目标。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_802_1.png)

如果绑定源是一组项（如集合或数组），WPF 将创建一个 COLLECTIONVIEW，将绑定指向集合中的特定项，并提供浏览集合和以各种方式组织集合的能力。

如果绑定源提供的值类型错误或格式不正确，你可以向 Binding 添加一个转换器来对其进行转换。

绑定表达式将 BINDING 对象链接到目标。由于它是一个独立对象，你可以将一个 BINDING 与多个目标一起重复使用，这是一件出乎意料地常见的事情。

GetBindingExpression(<property>) 方法将返回对 BindingExpression 的引用。

### 问题...

为了了解 WPF 绑定机制为你做了什么，让我们看一个简单的示例。这是一个简单的窗口，显示顶部窗格中 Border 对象的实际宽度和高度。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_803_0.png)

这只是一个带有背景填充的 TextBox 元素。它的名称设置为 Box。它跨越 Grid 的两列和一行。

这些标签显示 TextBox 元素的 ActualHeight、ActualWidth 和 Text 属性的值。

如果没有 WPF 绑定，为了在窗口大小改变时更改标签中的值，你需要在代码中更新它们。Border 没有 SizeChanged 事件，但 Window 有，我们可以在基本事件处理程序中更新值。

```
private void Window_SizeChanged(object sender, SizeChangedEventArgs e)
{
    WidthLabel.Content = Box.ActualWidth.ToString();
    HeightLabel.Content = Box.ActualHeight.ToString();
}
```

现在，这并不太乏味，但 TextLabel 呢？好吧，TextBox 公开了一个 TextChanged 事件，我们可以捕获它来更新标签。但是有一个问题：应用程序一运行，就会生成一个 null reference 异常，因为 TextChanged 在创建 TextBox 时就会被调用，这发生在标签创建之前。因此，你需要检查窗口是否已加载：

```
private void Box_TextChanged(object sender, TextChangedEventArgs e)
{
    if (this.IsLoaded)
        TextLabel.Content = Box.Text;
}
```

开始变得有点复杂了，不是吗？如果你想，比如说，将标签绑定到 TextBox 的背景颜色呢？对此没有任何事件。（而且 Color 没有合理的文本表示形式。你对此怎么办？）当然，解决方案是让 WPF 为你处理所有这些丑陋的细节。继续阅读...

