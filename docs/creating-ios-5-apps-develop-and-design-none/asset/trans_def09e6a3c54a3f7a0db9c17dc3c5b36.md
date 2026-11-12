
接下来，实现 setWeightEntries:andUnits: 方法，如下所示：

```
#pragma mark - Setting the weight data
- (void)setWeightEntries:(NSArray*)weightEntries
                  andUnits:(WeightUnit)units {
    self.graphStats =
      [[GraphStats alloc] initWithWeightEntryArray:weightEntries];
    self.units = units;
    [self setNeedsDisplay];
}
```

在这里，我们首先使用 weightEntries 参数实例化一个新的 GraphStats 对象。然后，我们将该对象赋值给 graphStats 属性。我们还设置了 units 属性，并调用了 setNeedsDisplay。

setNeedsDisplay 方法告诉系统视图内容已更改，需要重绘。请注意，setNeedsDisplay 不会触发立即重绘。相反，系统只是记录该请求，然后让 setNeedsDisplay 返回。接下来，在下一个绘制周期中，视图会重绘自身。

## 执行自定义绘制

现在，我们进入本章的核心：绘制用户界面。

当 UIKit 需要绘制一个视图（无论是整体还是部分）时，它会创建一个图形上下文，该上下文的原点与视图的 bounds 一致（例如，{0.0, 0.0} 位于视图的左上角）。它还会应用必要的变换，使上下文与视图匹配（旋转、缩放等）。然后，它调用视图的 drawRect: 方法。

当然，默认的 UIView 的 drawRect: 方法什么也不做，但我们可以重写它来自定义视图的外观。

请注意，这并不是绘制视图的唯一方式。如果你只想更改背景颜色，则无需实现 drawRect:。只需更改视图的 backgroundColor 属性即可，其余工作会自动完成。

另一个极端是，如果你直接在视图的 layer 中绘制内容，或者计划使用 OpenGL ES 进行绘制，则无需重写 drawRect: 方法。这些方式有各自的绘制技术。

## 不透明视图

每个视图都有一个 opaque 属性。该属性充当对绘制系统的提示。如果该属性设置为 YES，绘制系统会假定视图完全不透明，并相应地优化绘制代码。如果设置为 NO，绘制系统会将此视图合成到任何底层视图之上。这样可以实现更炫酷的效果，但速度可能会慢很多。默认情况下，该属性为 YES。除非你的视图确实需要透明或半透明区域，否则应避免更改此属性。

然而，视图不透明意味着我们的自定义绘制代码必须完全填充给定的矩形。我们不能留下任何透明或半透明区域，以免底层视图透出。一种方法是直接设置一个不透明的 backgroundColor，它会隐式填充整个视图的矩形。但是，如果用户（或其他开发者）可以更改背景颜色，尤其是可以选择非不透明背景颜色，那么这种做法可能并不合适。

尽管如此，如果你打算使用 Core Graphics 和 UIKit 中的原生绘制技术，drawRect: 是你最好的朋友。

在我们的视图中，我们将绘制一个简单的图表。y 轴表示体重；x 轴表示时间。我们将动态缩放两个轴，以覆盖 WeightEntries 数组中的全部范围。我们还会在背景中绘制网格，以及标记最大值和最小值的参考线。最后，我们将体重趋势线叠加在这些背景信息之上。

显然，这并不是最优的图表。由于自动缩放，体重的微小变化也可能看起来非常巨大。更好的方法是更智能地选择刻度，使其有效利用整个空间，同时仍能显示完整的趋势线，并尽量减少体重日常自然波动。此外，我们确实应该同时标注两个轴，而不仅仅是体重，并且参考线应在此范围内均匀分布（每 2 磅、5 磅、10 磅，等等）。如果它们与背景网格对齐，那就更好了。

尽管如此，我们这种快速而粗糙的实现相对直接，同时让我们探索了许多有用的绘制技术。所以，请取消 drawRect: 方法的注释。

理论上，第一次调用此方法时，rect 参数应设置为视图的 bounds，让你能够填充整个视图。后续调用可能只要求重绘该视图的一小部分。然而，在实践中，除非你正在更改视图并显式调用 setNeedsDisplay 或 setNeedsDisplayInRect:，否则你可能只会绘制该视图一次。UIKit 会缓存并重用这份原始绘制结果。

UIView 会绘制到其 CALayer 上，然后按需显示 CALayer。因此，我们可以调整视图大小、翻转视图、淡入淡出，甚至将其遮盖后再显示，而无需重新绘制。

如果你正在更新视图，应尽量使更新矩形尽可能小。系统会自动将当前上下文的裁剪路径设置为与更新矩形匹配。这可以防止我们不慎在更新矩形之外进行绘制。即便如此，我们仍应避免进行任何不必要的绘制，尤其是在频繁更新视图时，因为这会成为严重的性能瓶颈。

在复杂视图中，你通常希望使用多个视图或图层来分隔内容——一个包含静态内容，其他包含不同的动态元素。这样，我们可以选择性地只重绘实际发生变化的元素。

就我们的情况而言，整个视图是静态的；它只应在系统首次显示时绘制一次。这意味着我们可以安全地忽略 rect 参数，直接绘制整个视图。如果万一系统恰好只更新了我们视图的一部分，一切也仍会正常运作。是的，我们可能会在裁剪路径之外绘制上浪费一点点计算资源——但这些绘制命令会被忽略，实际上不会影响应用程序的外观。请记住，为实践中永远不会出现的边缘情况优化代码是没有意义的。

另外，请注意我们从未绘制视图的 backgroundColor。系统会在调用我们的 drawRect: 方法之前自动为我们处理。然而，由于我们的自定义绘制代码并没有填充整个视图，我们必须设置一个非不透明的背景颜色，或将视图的 opaque 属性更改为 NO。否则可能会导致不可预测的绘制错误。

### Core Graphics 与 UIKit 绘制对比

我们的自定义绘制代码将结合使用 Core Graphics 绘制函数和 UIKit 绘制方法。这些方法和函数（在很大程度上）完全兼容。实际上，UIKit 方法通常使用 Core Graphics 函数来执行实际绘制。两个框架之间存在许多重复的方法。例如，我们使用 `[self.graphFillColor setFill]` 设置当前上下文的填充颜色。或者，我们也可以调用 Core Graphics 函数 `CGContextSetFillColorWithColor(context, self.graphFillColor.CGColor)` 来替代。

请注意，这里有一个重要区别：UIKit 使用 UIColor 类，而 Core Graphics 使用 CGColorRef。此外，UIKit 方法隐式使用当前图形上下文。大多数 Core Graphics 方法需要显式引用上下文。当然，虽然细节可能不同，但最终结果是相同的。

```
    #pragma mark - drawing
    - (void)drawRect:(CGRect)rect {
        // Calculate bounds with margin.
        CGRect innerBounds =
            CGRectInset(self.bounds, self.margin, self.margin);
        // Fill in the rounded rectangle.
        UIBezierPath* graphBorder =
            [UIBezierPath bezierPathWithRoundedRect:innerBounds
            byRoundingCorners:UIRectCornerAllCorners
            cornerRadii:self.cornerRadius];
        [self.graphFillColor setFill];
        [graphBorder fill];
```

这里我们使用 `CGRectInset()` 方法创建一个以视图 bounds 为中心的更小矩形。我们使用 margin 属性来确定内部 bounds 与视图 bounds 之间的间距。我们将默认 margin 设置为 5.0f，因此所有边缘（左、右、上、下）都应有 5 点的间隙。

接下来，我们使用 `bezierPathWithRoundedRect:byRoundingCorners:cornerRadii:` 便捷方法来创建 `UIBezierPath`。`UIBezierPath` 类允许我们创建一系列直线和曲线段，然后将该路径绘制到当前上下文中。路径可以是开放的，也可以是封闭的。你可以用任意一种方式来构建它们
