
样式表还可以与其他技术结合使用以执行更复杂的自定义。例如，假设我们想在 `QLineEdit` 内部放置一个微小的“擦除”按钮，位于 Qt 文本的右侧。这涉及创建一个 `EraseButton` 类，并将其放置在 `QLineEdit` 之上（例如使用布局），但也要为按钮留出空间，以便输入的文本不会与擦除按钮碰撞。通过子类 `QStyle` 是不方便的，因为我们必须子类 Qt 中可能被应用程序使用的每种样式（`QWindowsStyle`、`QPlastiqueStyle` 等）。使用样式表，以下规则可以解决问题：

```
QLineEdit {
padding: 0px 15px 0px 0px;
}
```

`padding` 属性允许设置内边距。通过样式表，以下规则可以将复选框和单选按钮指示器的大小增加到 20 x 20 像素，并确保指示器与关联文本之间有 8 像素。

当一个属性被多个具有相同选择器的规则设置时，最后定义的规则将会被应用。

对于 `QPushButton` 的样式设置，我们将使用一种完全不同的方法。我们不再使用样式表规则来绘制按钮，而是使用一个现成的图像作为背景。此外，为了让按钮可伸缩，我们使用 CSS 背景图像机制来定义按钮的渐变。

与使用 `background-image` 指定边框图像不同，边框图像被切割成一个 3 x 3 的网格，如图 19.9 所示。在填充控件的背景时，图中的四个角单元格 A、C、G 和 I 将保持原样，而其他五个单元格则会被拉伸或平铺，以填充可用空间。

# 图 19.9 边框图像切割

![](img/5a524abdf0b0d58fa99d30abb4463611_737_0.png)

边框图像使用 `border-image` 属性指定，这要求我们指定图像文件名以及定义九个单元格的四个“切割位置”。这些切割位置定义为距离顶部、右侧、底部和左边缘的像素距离。距离顶、右、底、左边缘分别为 4、8、12 和 16 像素的 `border.png` 边框图像将指定如下：

```
border-image: url(border.png) 4 8 12 16;
```

使用边框图像时，我们必须显式设置 `border-width` 属性。通常，`border-width` 应该对应切割的位置；否则，角单元格将被拉伸或缩小以适应 `border-width`。对于 `border.png`，我们将如下指定边框宽度：

```
border-width: 4px 8px 12px 16px;
```

现在我们已经知道了边框图像机制的工作原理，让我们来看看它是如何用于 Candy `QPushButton` 的。以下是定义按钮行为的规则：

```
QPushButton {
  color: white;
  font: bold 10pt;
  border-image: url(:/images/button.png) 16;
  border-width: 16px;
  padding: -16px 0px;
  min-height: 32px;
  min-width: 60px;
}
```

在 Candy 样式表中，`QPushButton` 图像的四个切割位置位于 34 x 34 像素边框图像边缘的 16 像素处，如图 19.10 (a) 所示。由于四个切割是均匀的，我们只需要为切割位置写“16”，为边框宽度写“16px”。

在图 19.10 (b) 所示的 `QPushButton` 示例中，对应 D、E 和 F 的边框图像单元格被丢弃了，因为调整大小后的按钮没有高度需要它们，而 B 和 H 单元格被水平拉伸以占据额外的宽度。

# 图 19.10 用于 QPushButton 的边框图像

![](img/5a524abdf0b0d58fa99d30abb4463611_738_0.png)

边框图像的标准用法是为控件提供一个边框，让控件位于边框内部。但我们颠覆了边框图像机制，并将其用于创建控件自身的背景。结果是，单元格 E 被丢弃，内边距矩形的高度为 0。为了给按钮文本留出空间，我们指定了 -16 像素的垂直内边距。图 19.11 Illust了这种情况。如果我们使用边框图像机制来定义实际边框，我们可能不希望文本与其碰撞——但由于我们使用它来创建一个可伸缩的背景，我们希望文本位于其上方而不是其内部。

# 图 19.11 QPushButton 的结构

![](img/5a524abdf0b0d58fa99d30abb4463611_739_0.png)

通过 `min-width` 和 `min-height`，我们设置了按钮内容的最小尺寸。所选的值确保了有足够的空间放置边框图像角，并且让“确定”按钮比需要的宽一点，以便在“取消”按钮旁边看起来更好。

之前的 `QPushButton` 规则适用于所有按钮。现在，我们将定义几条仅在按钮处于某些状态时才应用的额外规则。

```
QPushButton:hover {
  border-image: url(:/images/button-hover.png) 16;
}
```

当鼠标指针悬停在 `QPushButton` 上时，`:hover` 状态评估为真，指定的规则将覆盖任何具有低特定性选择器的规则。在这里，我们使用这种技术指定一个稍微亮一点图像作为边框效果。之前指定的 `QPushButton` 属性继续生效；只有 `border-image` 属性发生了变化。

```
QPushButton:pressed {
  color: lightgray;
  border-image: url(:/images/button-pressed.png) 16;
  padding-top: -15px;
  padding-bottom: -17px;
}
```

当用户按下按钮时，我们将前景颜色更改为浅灰色，使用更深颜色的边框图像，并通过微调内边距将按钮文本向下移动一个像素。

我们最终的样式规则将自定义 `QComboBox` 的外观。为了展示我们能够实现的控制和精确性，我们区分了只读和可编辑的组合框。对于只读组合框，我们提供了自定义的下拉箭头，使其比标准箭头稍大一点。图 19.12 显示了此。

# 图 19.12 下拉箭头

![](img/5a524abdf0b0d58fa99d30abb4463611_740_0.png)

对于只读组合框，我们指定了 15 像素的右内边距，以确保组合框中显示的文本与下拉箭头重叠。图 19.13 显示了这些维度是如何相互作用的。

# 图 19.13 只读 QComboBox 的结构

![](img/5a524abdf0b0d58fa99d30abb4463611_742_0.png)

使用 `button.png` 作为边界图像。然而，这一次，我们指定了 16 的边界宽度以缩小图像，并指定了内容的固定大小为水平 7 像素和垂直 6 像素。图 19.14 显示了我们做的示意图。

# 图 19.14 可编辑 QComboBox 下拉按钮的边界图像

![](img/5a524abdf0b0d58fa99d30abb4463611_743_0.png)

如果组合框打开，我们为下拉按钮使用另一种颜色更深的图像：

```
QComboBox::drop-down:editable:open {
  border-image: url(:images/button-pressed.png) 16;
}
```

对于可编辑的组合框，我们指定了 29 像素的右边距为下拉按钮留出空间，如图 19.15 所示：

```
QComboBox::editable {
  margin-right: 29px;
}
```

# 图 19.15 可编辑 QComboBox 的结构

![](img/5a524abdf0b0d58fa99d30abb4463611_743_1.png)

我们现在已经完成了 Candy 样式表的创建。该样式表大约有 100 行，并使用了一些自定义图像。结果是一个极具特色的对话框。

使用样式表创建自定义样式可能涉及大量的尝试和错误，特别是那些没有使用过 CSS 的人来说。样式表的主要挑战之一是 CSS 冲突解决和级联并不总是给出直观的结果。更多细节，请参阅在线文档 `http://doc.trolltech.com/4.3/stylesheet.html`。该文档描述了 Qt 对样式表的支持并提供了指向 CSS 规范的链接。

## 子类 QStyle

`QStyle` 类随 Qt 2.0 引入，旨在提供一种封装应用程序外观和感受的方法。`QAnimationStyle`、`QMotifStyle`、`QCDStyle` 等类为 Qt 运行的平台和桌面环境实现了这种外观。Qt 4.3 除了 `QStyle` 抽象基类和基类 `QCommonStyle` 外，还提供了八种样式。图 19.16 显示了它们之间的关系。

**图 19.16 Qt 内置样式的继承树**

![](img/5a524abdf0b0d58fa99d30abb4463611_745_0.png)

对于 Qt 开发人员来说，`QStyle` 架构使得通过子类 `QStyle` 或现有样式之一来开发自定义的外观和感受成为可能。我们可以对现有样式进行微调（例如 `QAnimationStyle`），也可以从零开始开发整个自定义样式。

`QStyle` API 提供了绘制图形元素的函数（如 `drawPrimitive()`、`drawControl()`、`drawComplexControl()` 等）以及查询样式的函数（`pixelMetrics()`、`styleHint()`、`hitTest()` 等）。`QStyle` 成员函数通常接收 `QStyleOption` 对象，该对象包含了关于绘制部件的通用信息（如其调色板）和特定部件的信息（例如按钮的文本）。这些函数还接收一个可选的 `QWidget` 指针，用于处理 `QStyleOption` 未提供所有必要信息的情况。

假设我们想要创建一个 `MyPushButton` 类，它看起来像标准的 Qt 按钮，但又不继承自 `QPushButton`。（这个例子相当复杂，但它将帮助我们理清部件与样式之间的关系。）在 `MyPushButton` 事件处理程序中，我们将设置一个 `QStyleOption`（实际上是 `QStyleOptionButton`）并如下所示调用 `QStyle::drawControl()`：

```
void MyPushButton::paintEvent(QPaintEvent * /* event */)
{
    QPainter painter(this);

    QStyleOptionButton option;
    option.initFrom(this);
    if (isFlat())
        option.features |= QStyleOptionButton::Flat;
    option.text = text();

    style()->drawControl(QStyle::CE_PushButton, &option, &painter, this);
}
```

`QStyleOption::initFrom` 函数初始化表示部件的基础成员变量，如 `rect`、`state`（启用、聚焦等）和 `palette`。`QStyleOptionButton` 特有的成员变量必须以这种方式进行初始化。在 `MyPushButton` 示例中，我们初始化了 `features` 和 `text`，而 `iconSize` 取了它们的默认值。

`QWidget::style` 函数返回用于绘制部件的相应样式。样式通常使用 `QApplication::setStyle()` 为整个应用程序设置，但也可以使用 `QWidget::setStyle()` 为单个部件进行覆盖。

`drawControl` 函数由各种 `QStyle` 子类实现，用于绘制 `QPushButton` 和其他简单部件。典型的实现可能如下：

```
void QMotStyle::drawControl(ControlElement element,
                             const QStyleOption *option,
                             QPainter painter,
                             const QWidget widget) const
{
    switch (element) {
    case CE_CheckBox:
        ...
    case CE_RadioButton:
        ...
    case CE_PushButton:
        if (const QStyleOptionButton *buttonOption =
            qstyleoption_cast<const QStyleOptionButton *>(option))
            // draw push button
        break;
        ...
    }
}
```

`element` 指明要绘制部件的样式代码。如果类型是 `CE_PushButton`，`QStyle` 子类将使用 `QOption` 参数。如果转换成功，则绘制推送按钮。这个版本的缺点是 `QPushButton` 不能用于渲染。因此，内置的 `QStyle` 子类尽可能使用 `QOption` 参数来获取有关部件的信息。在本节的其余部分中，我们将回顾图 19.17 所示 Bronze 样式的代码。Bronze 样式的特点是具有渐变背景的圆按钮、不常规的数字按钮位置、奢华的勾选以及“刷纹”背景。为了实现这一点，它使用了高级的 2D 图形，如抗锯齿、半透明、线性渐变和复合模式。

# 图 19.17 样式中的部件

![](img/5a524abdf0b0d58fa99d30abb4463611_747_0.png)

这里是 `BronzeStyle` 类的定义：

代码视图：

```
class BronzeStyle : public QStyle
{
    Q_OBJECT

public:
    BronzeStyle() {}

    void polish(QPalette &palette);
    void polish(QWidget widget);
    void unpolish(QWidget widget);
    int styleHint(StyleHint which, const QStyleOption option,
                  const QWidget widget = 0,
                  QStyleHintReturn returnData = 0) const;
    int pixelMetric(PixelMetric which, const QStyleOption option,
                    const QWidget widget = 0) const;
    void drawPrimitive(PrimitiveElement which,
                       const QStyleOption option, QPainter painter,
                       const QWidget widget = 0) const;
    void drawComplexControl(ComplexControl which, const QStyleOptionComplex option,
                            QPainter painter,
                            const QWidget widget = 0) const;
    QRect subControl(ComplexControl which, const QStyleOptionComplex option,
                    SubControl sub,
                    const QWidget widget = 0) const;

public slots:
    QIcon standardIconImplementation(StandardPixmap which,
                                     const QStyleOption option,
                                     const QWidget widget = 0) const;

private:
    void drawBronzeFrame(const QStyleOption option,
                          QPainter painter) const;
    void drawBronzeBevel(const QStyleOption option,
                          QPainter painter) const;
    void drawBronzeCheckBoxIndicator(const QStyleOption option,
                                     QPainter painter) const;
    void drawBronzeSpinBoxButton(SubControl which,
                                 const QStyleOptionComplex option,
                                 QPainter *painter) const;
};
```

在创建自定义样式时，我们通常基于现有样式，这样我们
