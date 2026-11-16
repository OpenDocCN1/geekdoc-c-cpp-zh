

## 控件组件

WPF 模板模型的妙处在于，你可以让控件几乎呈现任何你想要的外观，但所有功能都保持完好。如果你使用的是大多数其他 UI 平台，你就得从头重新构建控件，才能实现我们用几行 XAML 就能完成的事情。但这里的关键词是 "almost"。你可能希望滑块（Slider）看起来像仪表盘（顺便说一句，这会很酷），但仍然得有某种方式让用户更改数值。没有地方输入文本的文本框（TextBox）也不会太有用。组合框（ComboBox）……嗯，你明白我的意思。

进度条（ProgressBar）必须有用于指示进度的东西，以及用于指示 100% 的“轨道”东西。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_787_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_787_1.png)

滑块（Slider）必须有一个可移动的“按钮状”东西，以及一个它可以沿其移动的“轨道”东西。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_787_2.png)

组合框（ComboBox）必须有显示所选内容的地方、显示列表的地方，以及一个用于控制是否显示列表的“按钮状”东西。

## 控件协议

在早期版本的 .NET Framework 中，控件正常运行所需的部分是通过将模板中元素的名称设置为功能代码可引用的“魔术名称”来实现的。这奏效了，但可以说是（委婉地说）令人痛苦的。仅仅弄清楚哪些控件需要哪些部分，以及这些部分应该叫什么，可能就需要图书馆科学博士的研究技能。.NET 4.0 通过在控件协议（CONTROL CONTRACT）中正式化这种临时命名约定，让每个人的生活都更轻松了，该协议定义了模板为了正常运行应包含的所有内容。

控件协议是使用特性（attributes）定义的。（自第 5 章介绍过特性以来，我们就没再使用过它们，所以你忘记它们是向代码组件添加元数据的一种方式也可以理解。）必需的控件组件，称为 PARTS，是使用 TemplatePartAttribute 实现的，它有两个必需参数：Name 和 Type。Name 属性的值是你在控件模板中必须使用的 x:Name，Type 属性的值是它需要的控件类型。（这些通常定义在相当高的层级。）

更棒的是，这些协议实际上在 MSDN 上有文档（搜索“Styles and Templates”，包含引号。）这应该会带你进入库中的“控件样式和模板”部分。

但由于 MSDN 的好心人以移动东西而闻名（通常是在我找到它们后的第二天），如果其他方法都失败了，控件模板特性也包含在控件的类库定义中。

## 动动脑筋

使用上述任一技术，找出进度条（ProgressBar）控件的各个部分，然后编写一段定义控件默认可视化树的 XAML 代码片段。（不用担心 VisualStateManager 的相关内容。我们将在下一节讨论。）

为了完成这个练习，假设所有部分都是 Border 类的实例，并包含在 Grid 中。你不需要把这弄得太复杂；只需弄清楚需要哪些部分，以及它们应该如何命名。

## 你做得怎么样？

这是我的版本。

```xml
<ControlTemplate TargetType="ProgressBar">
<Grid>
<Border x:Name="PART_Track" />
<Border x:Name="PART_Indicator" />
<Border x:Name="PART_GlowRect" />
</Grid>
</ControlTemplate>
```

## 记一下

我一直把控件模板中指定的部分称为“必需组件”，但实际上它们不一定都是必需的。进度条（ProgressBar）就是一个很好的例子。PART_GlowRect 纯粹是装饰性的，如果你省略它，控件仍然可以正常工作。即使是功能性的部分，有时也可以省略。例如，滚动条不需要那些以小增量移动滑块的小箭头。WPF 控件非常智能，会直接忽略模板中未包含的部分。

## 休息一下

许多 WPF 元素都包含模板。本节探讨的控件模板是最常见的一种之一，我们将在下一章介绍数据模板。但所有模板的工作原理基本相同，所以如果你遇到从未见过的模板，不要慌张。

在完成复习并进入本章最后一节（即控件协议中取代触发器的 VisualStateManager）之前，为什么不休息一下呢？

- 你使用哪种 Presenter 来显示控件的 Content 属性？
- 你如何声明一个带有虚线轮廓的椭圆？
- 控件模板通常放在两个位置之一。这些位置是什么，你在什么情况下会使用每个位置？
- Decorator 和 Adorner 有什么区别？
- 为什么习惯在 Border 内部放置一个只有一行一列的 Grid？
- 你使用哪个元素来让控件模板反映元素的公共属性？
- 如果你没有包含控件协议指定的某个部分，会发生什么？

## 可视化状态

在上一章中，我们使用属性触发器和事件触发器来定义控件的可视化行为。在控件模板内部（不幸的是，仅限于控件模板内部），你有另一个更强大的选项：VisualStateManager。与控件部件一样，控件支持的可视化状态由其控件协议定义，使用 TemplateVisualState 特性，该特性同时定义状态和状态组：

```
[TemplateVisualState(Name="Normal", StateGroup="CommonStates")]
```

- VisualStateGroup 内的可视化状态是互斥的。
- 在任何给定时间，一个元素将处于每个 VisualStateGroup 的一个状态中。
- VisualState 元素包含一个 Storyboard。
- VisualTransition 中包含的 Storyboard 将在元素更改状态时激活。
- 一个元素可以包含任意数量的可视化状态组，每个组可以包含任意数量的可视化状态。

## 动动脑筋

Button 元素有三个状态组，总共九个可视化状态，如下所示。编写一个定义每个状态的控件模板骨架。（你知道怎么做，对吧？）现在不用担心 Storyboard。

| 可视化状态组 | 可视化状态 |
|---|---|
| CommonStates | Normal |
| CommonStates | MouseOver |
| CommonStates | Pressed |
| CommonStates | Disabled |
| FocusStates | Focused |
| FocusStates | Unfocused |
| ValidationStates | Valid |
| ValidationStates | InvalidFocused |
| ValidationStates | InvalidUnfocused |

## 记一下

你仍然可以在控件模板中使用触发器，而且你在互联网上找到的许多示例都使用这种较旧的技术。但是，当你自定义定义可视化状态的控件时，你真的应该改用 VisualStateManager，因为控件是为与其集成而构建的，而且与纯触发器解决方案相比，你可能会拥有更多灵活性。当然，如果你想响应控件定义的状态未涵盖的事件或属性更改，你始终可以同时使用两者。

## 你做得怎么样？

你是否想到使用 x:Name 标记扩展来指定组和状态名称，还是不得不偷看？

```xml
<ControlTemplate TargetType="Button">
... Visual Tree ...
<VisualStateManager.VisualStateGroups>
<VisualStateGroup x:Name="CommonStates">
<VisualState x:Name="Normal" />
<VisualState x:Name="MouseOver" />
<VisualState x:Name="Pressed" />
<VisualState x:Name="Disabled" />
</VisualStateGroup>
<VisualStateGroup x:Name="FocusStates">
<VisualState x:Name="Focused" />
<VisualState x:Name="Unfocused" />
</VisualStateGroup>
<VisualStateGroup x:Name="ValidationStates">
<VisualState x:Name="Valid" />
<VisualState x:Name="InvalidUnfocused" />
<VisualState x:Name="InvalidFocused" />
</VisualStateGroup>
</VisualStateManager.VisualStateGroups>
</ControlTemplate>
```

VisualStateGroups 集合不是直接公开的；它是一个附加属性。

每个组和每个状态都由名称标识。

## 记一下

与控件模板中定义的部件不同，控件支持的可视化状态仅在 MSDN 的“控件样式和模板”部分有文档，而不在类库中。至少在我写作时是这样。明天可能就不同了。

