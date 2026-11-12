
Core Animation 图层可能也需要显式支持。每当你创建一个新的 CALayer（一个尚未与视图关联的图层）时，它默认的 scale 值为 1.0。如果你随后将这个图层绘制到 Retina 显示屏上，它会自动放大以匹配屏幕。你可以通过手动更改图层的缩放因子，然后提供适合分辨率的内容来避免这种情况。

最后，OpenGL ES 默认也使用 1.0 的缩放比例。所有内容仍然会绘制在 Retina 显示屏上，但会被放大，并且可能显得块状（尤其是与正确缩放的绘图相比时）。为了获得全分辨率渲染，我们必须增加渲染缓冲区的大小。然而，这可能会对性能产生严重影响。因此，我们必须手动进行这些更改。更改视图的 contentScaleFactor 会自动修改底层的 CAEAGLLayer，使渲染缓冲区的大小按缩放因子增加。

在你打算支持的所有设备上测试绘图代码同样很重要。绘制一条 0.5 点宽的线在 iPhone 3GS 上可能看起来没问题，但在 iPhone 4 上可能显得太细。类似地，更高分辨率的资源会占用更多内存，并且加载和处理可能需要更长时间。不过，使用逻辑坐标系大大简化了创建跨多种分辨率工作的自定义绘图代码的过程。

## 绘制单条目趋势线

现在我们需要实现辅助方法。让我们从只包含单个条目时绘制一个点开始。当我们没有任何条目时，这也同样有效，因为 GraphStats 会返回 0.0 的持续时间和 0.0f 的权重。

```objc
- (void)drawSingleEntryTrendLine {
    NSAssert2(self.graphStats.minWeight ==
    self.graphStats.maxWeight,
              @"If there's only one entry the minimum weight "
              @"(%1.2f) should equal the maximum (%1.2f)",
              self.graphStats.minWeight, self.graphStats.maxWeight);
```

我们首先进行一个快速的健全性检查。只有在 GraphStats 对象包含零个或一个 WeightEntry 时，我们才应该调用 drawSingleEntryTrendLine 方法。在这两种情况下，最小和最大权重都应该具有相同的值。

我们可以使用 NSAssert（及其变体）来验证这个假设。NSAssert 接受两个参数：第一个是表达式，第二个是 NSString。默认情况下，该宏会计算表达式的值。如果结果为 false，NSAssert 会抛出 NSInternalInconsistencyException，并在错误消息中使用该字符串。

NSAssert 在调试、测试和强化代码时很有帮助。但是，我们可能不希望将这些检查包含在最终的发布版本中。幸运的是，我们可以轻松地禁用这些检查。只需定义一个 NS_BLOCK_ASSERTIONS 预处理器宏，编译器就不会包含 NSAssert。

默认情况下，Xcode 4.0 在进行发布版本构建时会自动禁用 NSAssert。这意味着我们在开发和测试时可以根据需要使用任意数量的 NSAssert。我们不必担心它们会对最终产品产生不利影响。

在代码中大量使用断言可以大大帮助提高应用程序的可靠性。如果一个方法只应该接受正数，请使用断言来验证这一事实。与其让应用程序在未定义的状态下蹒跚前行，不如用合理的错误信息使其崩溃。

当然，关于使用 Cocoa 的 NSAssert 宏还是 C 的 assert() 函数更好，存在一些争论。虽然它们基本上做的事情相同，但有两个主要区别。assert() 方法不接受错误字符串作为参数。使用带有明确定义错误消息的 NSAssert 可以让调试代码变得容易得多。另一方面，assert() 保证会终止你的应用程序——而 NSAssert 可能不会。

NSAssert 通常会抛出一个异常，但你可以通过创建自定义的 NSAssertionHandler 子类来改变这种行为。然而，在实践中，这几乎从未做过。更常见的情况是，当第三方库意外捕获然后静默丢弃你的 NSInternalInconsistencyException 时，问题可能会出现，从而掩盖了错误。这意味着你的断言可能失败了，但你从未真正看到它。

就我个人而言，我更喜欢 NSAssert 提供的更丰富的消息。毕竟，你总是可以设置断点来捕获异常，所以它们实际上无法躲过你的眼睛——至少在开发过程中是这样。而且，如果这真的成为一个问题，你总可以实现一个自定义的 NSAssertionHandler 来解决这个问题。

另一个互联网争论的重要来源是关于从发布代码中剥离断言的争论。除非它们确实损害了你的性能，否则无论是将其移除还是保留，都有充分的理由。我必须承认，我通常采取最省事的方式。以前版本的 Xcode 不会自动剥离 NSAssert；Xcode 4 会。大多数情况下，我并没有足够的动力去真正修改这种行为。

### 使用 NSAssert

> NSAssert 有许多变体，可以接受格式字符串，类似于 NSLog()。这里，我们只需在宏名称的末尾附加一个数字，表示传入我们字符串的参数数量。例如，在 drawSingleEntryTrendLine 方法中，我们使用 NSAssert2，然后传入两个参数。
>
> 然而，只要断言处于启用状态，你就可以使用带有格式字符串和可变参数列表的标准 NSAssert 宏。不幸的是，一旦你禁用断言，可变参数会导致编译错误（至少在 Xcode 4.0 中是这样）。因此，使用编号变体更容易也更安全。

```objc
// Find the center of the screen.
CGFloat x = self.bounds.size.width / 2.0f;
CGFloat y = self.bounds.size.height / 2.0f;
CGFloat weight = self.graphStats.minWeight;
```

通过健全性检查后，我们生成一些有用的值。我们计算图表视图中心的 x 和 y 坐标。然后获取权重值。由于我们只有一个值，我们可以直接使用 GraphStats 的最小权重——无需访问单独的 WeightEntry 对象。

```objc
NSString* label =
    [WeightEntry stringForWeightInLbs:weight inUnit:self.units];
UIFont* font = [UIFont boldSystemFontOfSize:self.fontSize];
CGSize textSize = [label sizeWithFont:font];
[self drawReferenceLineWithLabel:label
                           font:font
                            atY:y
              withTextWidthOffset:textSize.width];
```

现在我们要进入正题了。我们首先根据权重创建一个标签字符串。与往常一样，这将包含格式正确的数字和单位标签。然后，我们根据当前的 fontSize 属性请求粗体系统字体。我们可以使用该字体来计算绘制字符串所需的边界框。只需调用 NSString 的 UIStringDrawing 扩展中的 sizeWithFont: 方法即可。

手头有了字符串、字体、y 坐标和文本宽度，我们就可以调用 drawReferenceLineWithLabel:font:atY:withTextWidthOffset: 辅助函数。我们稍后会看一下这个函数，但基本上它会在沿左边距的指定 y 坐标处绘制我们的文本标签。这之后是一个小空格（基于文本宽度偏移和我们的 margin 属性），然后绘制一条延伸到右边距的细水平线。

```objc
    UIBezierPath* trendLine = [UIBezierPath bezierPath];

    trendLine.lineWidth = self.trendLineWidth;

    trendLine.lineCapStyle = kCGLineCapRound;

    [trendLine moveToPoint:CGPointMake(x, y)];

    [trendLine addLineToPoint:CGPointMake(x + 1, y)];

    [self.trendLineColor setStroke];

    [trendLine stroke];
    }
```

最后，我们绘制趋势线——或者实际上是我们趋势点。虽然我们可以使用 UIBezierPath 来创建一个真正的圆，但我们希望趋势点尽可能与多条目趋势线相匹配。最简单的方法就是绘制一条非常短的线。

在这里，我们创建我们的贝塞尔路径。我们根据 trendLineWidth 属性设置线宽。默认情况下，这是 4 点宽。然后我们将线帽样式设置为圆帽。这定义了线端点的形状。然后我们将光标移动到视图的中心，并创建一条 1 点长的线。

最后，我们根据 trendLineColor 属性设置线条颜色，并绘制线条。通过绘制一条带有圆端帽的很短很宽的线，我们创建了一个漂亮的小圆点，它将与我们将在下一个辅助方法中绘制的实际线条完美匹配。

