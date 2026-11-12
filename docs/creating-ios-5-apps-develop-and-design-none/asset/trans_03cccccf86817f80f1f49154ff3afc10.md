

## 绘制完整趋势线

尽管 drawTrendLine 在许多方面与之前的方法类似，但它增加了几层复杂性。在这里，我们将绘制两条带标签的参考线。一条对应最小重量，一条对应最大重量。我们还需要协调它们的外观，因此即使重量标签的宽度可能不同，参考线的左边缘仍能保持正确对齐。最后，我们需要动态调整图形的大小，使趋势线填满视图的大部分区域。

同样，由于这个方法较长，我们将分小块来查看。

```objective-c
- (void)drawTrendLine {
    // Draw the reference lines.
    UIFont* font = [UIFont boldSystemFontOfSize:self.fontSize];
    CGFloat textPadding = font.lineHeight / 2.0f;
    CGFloat topY = self.margin * 2 + textPadding;
    CGFloat bottomY = self.bounds.size.height - topY;
}
```

我们首先再次请求粗体系统字体。然后，根据字体高度的一半计算 textPadding 变量。接下来，我们使用这个值和 margin 属性来计算参考线的安全上限和下限。毕竟，我们不想截断标签的顶部和底部。

```objective-c
NSString* topLabel =
    [WeightEntry stringForWeightInLbs:self.graphStats.maxWeight
                               inUnit:self.units];
NSString* bottomLabel =
    [WeightEntry stringForWeightInLbs:self.graphStats.minWeight
                                inUnit:self.units];
CGSize topTextSize = [topLabel sizeWithFont:font];
CGSize bottomTextSize = [bottomLabel sizeWithFont:font];
// Get the maximum width.
CGFloat textOffset =
    topTextSize.width > bottomTextSize.width ?
        topTextSize.width : bottomTextSize.width;

[self drawReferenceLineWithLabel:topLabel
                           font:font
                           atY:topY
                           withTextWidthOffset:textOffset];
[self drawReferenceLineWithLabel:bottomLabel
                           font:font
                           atY:bottomY
                           withTextWidthOffset:textOffset];
```

接下来，我们为顶部和底部参考线创建重量标签。如前所述，顶线对应最大重量，底线对应最小重量。然后我们计算这两者的尺寸。

这里我们使用 C 的三元条件运算符来确定最大宽度（参见第 2 章的“运算符”）。该表达式的含义是：如果顶部宽度大于底部宽度，就使用顶部宽度；否则使用底部宽度。

最后，我们调用辅助方法来绘制两条参考线。注意，两条线使用的是同一个 textOffset。

```objective-c
CGFloat startX = self.margin * 4 + textOffset;
CGFloat endX = self.bounds.size.width - (self.margin * 3);
UIBezierPath* trendLine = [UIBezierPath bezierPath];
trendLine.lineWidth = self.trendLineWidth;
trendLine.lineCapStyle = kCGLineCapRound;
trendLine.lineJoinStyle = kCGLineJoinRound;
// Get starting point.
CGRect graphBounds =
    CGRectMake(startX, topY, endX - startX, bottomY - topY);
```

在这里，我们要确保图形的起始位置在标签右侧足够远。因此，我们利用 textOffset 变量和 margin 属性来计算起始和结束的 x 坐标。

一旦获得起始和结束的 x 坐标，我们创建一个空的 UIBezierPath，它将存放我们的趋势线。我们根据 trendLineWidth 属性设置线宽，然后赋予它圆形的端点样式和连接样式。我们之前讨论过端点样式。连接样式定义了两个线段连接处的拐角形状。

作为本代码段的最后一步，我们根据 startX、endX、topY 和 bottomY 的值创建一个矩形。

```objective-c
// Process all the entries.

[self.graphStats processWeightEntryUsingBlock:
    ^(WeightEntry* entry) {
        CGPoint point =
            [self coordinatesForEntry:entry inBounds:graphBounds];
        if (trendLine.empty) {
            // If we don't have any points,
            // move to the starting point.
            [trendLine moveToPoint:point];
        }
        else {
            // Otherwise, draw a line to the next point.
            [trendLine addLineToPoint:point];
        }
    }];
    [self.trendLineColor setStroke];
    [trendLine stroke];
}
```

最后，我们使用 processWeightEntryUsingBlock: 方法处理 GraphStats 对象中的所有 WeightEntry（参见本章开头的“构建 GraphStats”）。

我们首先调用 coordinatesForEntry:inBounds: 辅助方法，计算条目在我们选定的边界内的坐标。然后，如果我们的 Bezier 路径为空，就把光标移动到起始点；否则，我们添加一条从当前光标位置延伸到给定点的新线段。这也会将光标位置更新到新点。

路径完成后，我们设置描边颜色并绘制它。

## 绘制参考线和标签

现在让我们实现参考线辅助方法：

```objective-c
- (void)drawReferenceLineWithLabel:(NSString*)label
                              font:(UIFont*)font
                                 atY:(CGFloat)y
                  withTextWidthOffset:(CGFloat)xOffset {
    // Set x-coordinate.
    CGFloat x = self.margin * 2.0f;
    [self.textColor setFill];
    [label drawAtPoint:CGPointMake(x, y - (font.lineHeight / 2.0f))
             withFont:font];
    x += self.margin + xOffset;
    UIBezierPath* referenceLine = [UIBezierPath bezierPath];
    referenceLine.lineWidth = self.referenceLineWidth;
    [referenceLine moveToPoint:CGPointMake(x, y)];
    [referenceLine addLineToPoint:
        CGPointMake(self.bounds.size.width -
            (self.margin * 2.0f), y)];
    [self.referenceLineColor setStroke];
    [referenceLine stroke];
}
```

我们首先创建一个 x 坐标，它按两倍的 margin 属性内缩——第一次内缩让我们到达圆角矩形的边缘，第二次内缩则在圆角矩形内部留出合适的边距。请注意，我们对所有边距都使用相同的 margin 值：视图边界与圆角矩形之间的距离、圆角矩形左侧与参考标签之间的距离，以及参考标签与参考线之间的距离。我们本可以使用不同的 margin 参数，但这样做能简化代码，并提供干净、统一的外观。

然后，我们将填充颜色设置为 textColor 属性，并使用 UIStringDrawing 的 drawAtPoint:withFont: 方法绘制文本。这会绘制一行文本，其左上角位于给定点。请注意，此方法使用当前上下文的文本绘制模式和颜色；但你不需要设置上下文的字体，drawAtPoint:withFont: 方法会自动为你管理字体。

默认情况下，文本仅使用填充颜色绘制。如果你想改变这一点，可以调用 Core Graphics 的 CGContextSetTextDrawingMode() 方法来添加轮廓（以及其他绘制效果）。

此外，我们希望文本在 y 坐标上垂直居中。请注意，我们通过从 y 坐标中减去字体行高的一半来偏移绘制点。这会将标签上移，使其边界框适当居中。

接下来，我们使用文本宽度偏移和 margin 将 x 坐标向内移动。我们创建一条路径，即从给定的 x、y 坐标延伸到右边距的一条水平线段。我们设置线宽和颜色，然后绘制这条线。

这种方法与我们绘制网格线时使用的方法略有不同。这里我们使用 UIKit 的 UIBezierPath；之前我们使用的是 Core Graphics 的 CGContextStrokeLineSegments() 函数。正如我们之前所说，这两个框架之间有许多重复（或几乎重复）的方法。这通常为我们提供了多种完成同一基本任务的方式。你可以根据具体应用选择最合适的方法。

