
现在在代码后置（code-behind）中使用相应的 `CanExecute` 和 `Exec` 例程。ImageColors 程序对所有命令都使用以下 `CanExecute` 程序，因此当窗口的复选框被选中时，所有命令都处于启用状态：

```
// 如果 CheckBox 被勾选，则返回 True。
private void CanExecuteChecked(Object sender, CanExecuteRoutedEventArgs e)
{
    e.CanExecute = (checkBox.IsEnabled == true);
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_394_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_394_1.png)

Invert 命令的 `Exec` 方法很有意思，但与此讨论无关，因此在此不再显示。从书籍网站开发示例命令以查看其工作原理。

在接下来的 XML 代码中，添加命令绑定（command bindings）以告诉程序使用哪些例程来处理命令的 `CanExecute` 和 `Exec` 属性。以下代码显示 ImageColors 程序如何绑定其 Invert 命令：

```
<Window.CommandBindings>
  <CommandBinding Command="{x:Static local:Window1.CommandInvert}"
                  CanExecute="{Binding ExecuteCommandChecked}"
                  Exec="{Binding ExecuteImageInvert}"/>
  <!-- 省略其他命令的代码 -->
  </CommandBinding>
</Window.CommandBindings>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_394_2.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_394_3.png)

最后，添加 XAML 代码来显示按钮、菜单项以及调用命令的控件。

以下代码显示 ImageColors 程序如何显示其 Invert 菜单项。MenuItem 控件会自动获取命令的 `Text` 属性以显示其标题。它使用命令的输入手势（input gesture）显示快捷键 [Alt+I]。

```
<MenuItem Command="{x:Static local:Window1.CommandImageInvert}" />
```

以下代码显示程序如何显示其 Invert 按钮。与相应的菜单项不同，按钮不会自动从命令对象获取标题，因此 XAML 代码必须使用按钮的标题。

```
<Button Name="btnInvert"
             Command="{x:Static local:Window1.CommandImageInvert}"
             Style="{StaticResource ButtonStyle}"
             Content="{Binding RelativeSource={RelativeSource Self}, Path=Command.Text} />
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_394_4.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_394_5.png)

现在解释代码如何将按钮的 `Content` 绑定到命令对象的 `Text` 属性。由于代码后置为对象的文本添加了下划线，当按下 [Alt] 键时，按钮会自动为加速键下划线，并响应 [Alt]+I 键序列。

这个过程看起来很复杂并涉及许多步骤，但如果逐个执行，步骤其实非常简单。我鼓励你从书籍网站下载 Image-Colors 示例程序并查看代码，看看它们是如何组合的。

# 总结

本章描述了 WPF 命令对象，它们提供了多处好处。它们让程序能够轻松启用和禁用任意数量的按钮、菜单项和其他调用它们的控件；它们允许你挂载输入手势，让用户能够通过键盘序列调用命令；并且它们能够自动在菜单项上显示这些手势。

WPF 提供了约 150 个预定义的命令对象，你可以使用它们来表示应用程序中的逻辑操作。某些命令（如复制、剪切、粘贴）甚至被 TextBox 等控件支持。请参阅附录 X 获取预定义命令对象的列表。

如果预定义命令不能满足你的所有需求，你也可以创建自己的命令。

是否使用命令仍然取决于你。你的应用程序可以捕获事件并采取直接行动，而无需使用命令。这对于简单的操作可能是实用的，但如果你想提供多种方式来调用同一个命令或支持输入手势，那么你应该尝试一下命令。

WPF 命令机制是一种在相当抽象的层面上控制逻辑操作的通用机制。许多应用程序都有“创建新文档”的概念，尽管你看不到动作本身，只能看到结果。

下一章将描述两个更具体的工具：变换（transformations），它们修改了程序绘制图形的方式；以及效果（effects），它们为图形输出添加装饰。

# 变换与效果

正如第 1 章提到的，WPF 使用 DirectX 作为其渲染引擎。DirectX 提供了对系统上任何高性能图形硬件的访问，因此它可以相对快速且容易地产生惊人的效果。

本章介绍了 WPF 作为使用 DirectX 收益的两种有用技术：变换和位图效果。合理使用这些技术可以使应用程序更易用、更具吸引力。

# 变换

变换在绘制对象之前会改变其几何形状。不同类型的变换可以拉伸、旋转、压缩、倾斜和移动对象。

WPF 在内部使用 3x3 矩阵表示变换，并用线性代数对其进行操纵。幸运的是，在 XAML 代码中使用变换时，你并不需要理解它们是如何运作的。

WPF 提供了四种基本的变换，通过以下 XAML 元素表示：

- *RotateTransform*：此变换旋转对象。`Angle` 属性决定对象顺时针旋转的度数。
- *ScaleTransform*：此变换缩放对象。`ScaleX` 和 `ScaleY` 属性分别决定水平和垂直缩放因子。
- *SkewTransform*：此变换通过 `SkewX` 和 `SkewY` 属性指定的角度倾斜对象。
- *TranslateTransform*：此变换移动对象。`X` 和 `Y` 属性决定对象在水平和垂直方向上移动的距离。

# 第20 章变换与效果

通常，旋转、缩放和倾斜相对于对象的起点（通常是左上角）。可以通过设置 `CenterX` 和 `CenterY` 属性更改变换中心。例如，你可以将中心移动到控件中间，以便绕中心而非左上角旋转。

要对对象应用变换，给该对象添加一个 `LayoutTransform` 或 `RenderTransform` 元素，其中包含一种基本变换。当你使用 `LayoutTransform` 时，WPF 在布局控件之前修改内容。当你使用 `RenderTransform` 时，WPF 先布局再修改内容。本章中的“布局与渲染变换”章节将向你展示这两个元素的区别。

例如，以下代码创建了一个 `Label`。`Label.LayoutTransform` 元素包含的 `RotateTransform` 会将 Label 旋转 45 度。

```
<Canvas Left="140" Canvas.Top="50"
Background="LightGreen" Foreground="Red"
Content="Rotate 45 degrees">
  <Label.LayoutTransform>
    <RotateTransform Angle="45"/>
  </Label.LayoutTransform>
</Label>
```

除了四种基本变换外，WPF 还提供了 `MatrixTransform` 类，它将旋转、缩放、倾斜和平移的任意组合表示为矩阵。使用它比使用四种基本变换复杂，且如果没有覆盖的情况，它也不会提供额外的灵活性。更多信息，请参阅 mdn.microsoft.com/system.windows.media.matrixtransform.aspx 中的 MatrixTransform 类在线帮助。

图 20-1 所示的变换示例程序展示了各种变换。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_397_0.png)

图 20-1

以下列表提到了图 20-1 中的一些显著特征：

- 顶部较大的黄色 Label 在水平方向缩放了 5 倍，垂直方向 1 倍。
- 中间较小的白色 Label 在水平方向缩放了 -1 倍。
- 橙色平移 Label 位于蓝色画布内部，因此其平移相对于画布的左上角的。
