
//填充黄色椭圆
theColor = [NSColor colorWithDeviceRed:(float)1.0
green:(float)1.0 blue:(float)0.0
alpha:(float)1.0];
[theColor set];
[thePath fill];

//创建椭圆路径
theRect = NSMakeRect(100, rect.size.height-80, 60, 60);
thePath = [NSBezierPath bezierPathWithOvalInRect:theRect];

//填充红色椭圆
theColor = [NSColor colorWithDeviceRed:(float)1.0
green:(float)0.0 blue:(float)0.0
alpha:(float)1.0];
[theColor set];
[thePath fill];

图 12-7 展示了结果。

![](img/ea40cad434a338535474e82c1a6ace20_253_0.png)

**图 12-7：** 添加几个圆形椭圆，创建一个简单交通信号灯的图像。

## 绘制路径

你不必填充遇到的所有路径。你也可以*描边*一条路径，其效果是在路径周围绘制轮廓。描边路径与填充路径一样简单：

```OBJECTIVE-C
[thePath stroke];
```

![](img/ea40cad434a338535474e82c1a6ace20_254_0.png)

你还可以结合填充和描边以产生不同的效果。这样做时，请确保在填充函数之后执行描边函数，以便轮廓绘制在已填充路径的上方。例如，假设你想为其中一个交通信号灯绘制一个黑色圆环。你的代码可能如下所示：

```OBJECTIVE-C
//描边黑色椭圆
theColor = [NSColor blackColor];
[theColor set];
[thePath stroke];
```

这段代码在灯周围绘制了一条细轮廓。如果你更喜欢较粗的轮廓，请使用路径的 `setLineWidth:` 函数。默认线宽为 1，因此任何更大的值都会产生更粗的线条：

```OBJECTIVE-C
[thePath setLineWidth: 5];
```

要在每盏灯周围绘制轮廓，请通过添加**加粗**代码来调整你的 `drawRect:` 函数：

```OBJECTIVE-C
- (void)drawRect:(NSRect)rect
{
... 代码省略 ...

//**************************************
//       绘制灯光
//**************************************
//创建椭圆路径
theRect = NSMakeRect(100, rect.size.height-220, 60, 60);
thePath = [NSBezierPath bezierPathWithOvalInRect:theRect];

//填充绿色椭圆
theColor = [NSColor colorWithDeviceRed:(float)0.0
                                green:(float)1.0
                                blue:(float)0.0
                                alpha:(float)1.0];
[theColor set];
[thePath fill];

//描边黑色椭圆
theColor = [NSColor blackColor];
[theColor set];
[thePath setLineWidth: 5];
[thePath stroke];

//创建椭圆路径
theRect = NSMakeRect(100, rect.size.height-150, 60, 60);
thePath = [NSBezierPath bezierPathWithOvalInRect:theRect];
//填充黄色椭圆
theColor = [NSColor colorWithDeviceRed:(float)1.0
                                green:(float)1.0 blue:(float)0.0
                                alpha:(float)1.0];
[theColor set];
[thePath fill];
//描边黑色椭圆
theColor = [NSColor blackColor];
[theColor set];
[thePath setLineWidth: 5];
[thePath stroke];
//创建椭圆路径
theRect = NSMakeRect(100, rect.size.height-80, 60, 60);
thePath = [NSBezierPath bezierPathWithOvalInRect:theRect];
//填充红色椭圆
theColor = [NSColor colorWithDeviceRed:(float)1.0
                                green:(float)0.0 blue:(float)0.0
                                alpha:(float)1.0];
[theColor set];
[thePath fill];
//描边黑色椭圆
theColor = [NSColor blackColor];
[theColor set];
[thePath setLineWidth: 5];
[thePath stroke];
}
@end
```

图 12-8 展示了代码更改后的结果。

### 创建花哨的路径

到目前为止，你一直在处理矩形和椭圆路径。然而，路径不必局限于这两种简单形状。路径可以简单或复杂，完全取决于你的需求。

![](img/ea40cad434a338535474e82c1a6ace20_256_0.png)

假设你想在交通信号灯图形旁边显示一个停车标志。停车标志是八边形。要创建停车标志形状的路径，只需创建八个 `NSPoint` 变量，并用代表停车标志形状的坐标点填充它们。由于追踪复杂路径中的各个点可能会变得繁琐，Cocoa 允许你相对于路径中的最后一个点来定义路径。这样，你可以用实际坐标定义起点，并将路径的其余部分相对于该点进行定义。

![](img/ea40cad434a338535474e82c1a6ace20_256_1.png)

> 如果你以后想将该路径移动到另一个位置，只需要修改一个点——即第一个点。路径的其余部分将跟随第一个点移动，无需进行其他代码更改。

以下代码创建了一个停车标志形状路径的点。此代码使用相对于第一个点的坐标：

```OBJECTIVE-C
/************************************************************************/
//          绘制停车标志
/************************************************************************/

    // 创建八边形（停车标志）的八个点
    NSPoint pt1,pt2,pt3,pt4,pt5,pt6,pt7,pt8;

    //定义这些点
    pt1 = NSMakePoint(300, rect.size.height-220);
    pt2 = NSMakePoint(100, 0);
    pt3 = NSMakePoint(50, 50);
    pt4 = NSMakePoint(0, 100);
    pt5 = NSMakePoint(-50, 50);
    pt6 = NSMakePoint(-100, 0);
    pt7 = NSMakePoint(-50, -50);
    pt8 = NSMakePoint(0, -100);
```

第一个点相对于视图的原点。后面七个点中的每一个，其值都相对于列表中前一个点。

以下是如何使用相对点创建路径的方法：

- 1. **为路径定义相对点位置。**

  请遵循以下准则：

  - *正 x 值*：路径向右移动。
  - *负 x 值*：路径向左移动。
  - *正 y 值*：路径向上移动。
  - *负 y 值*：路径向下移动。

- 2. **定义路径上的各个点后，使用 NSBezierPath 类的 bezierPath 类方法创建 NSBezierPath。**

```OBJECTIVE-C
// 创建停车标志路径
NSBezierPath *stopSign = [NSBezierPath bezierPath];
```

- 3. **将点添加到路径中。**

  对于第一个点，使用 `moveToPoint` 函数。对于后续的点，使用 `relativeLineToPoint` 函数，因为你应该将这些点相对于第一个点进行定位：

```OBJECTIVE-C
[stopSign moveToPoint:pt1];
[stopSign relativeLineToPoint:pt2];
[stopSign relativeLineToPoint:pt3];
[stopSign relativeLineToPoint:pt4];
[stopSign relativeLineToPoint:pt5];
[stopSign relativeLineToPoint:pt6];
[stopSign relativeLineToPoint:pt7];
[stopSign relativeLineToPoint:pt8];
```

- 4. **使用 closePath 函数闭合路径：**

```OBJECTIVE-C
[stopSign closePath];
```

- 5. **路径定义完成后，你可以对其应用常见的颜色、填充和描边命令。**

  例如，要将停车标志填充为红色并用白色描边，请使用如下代码：

```OBJECTIVE-C
// 绘制路径
[[NSColor redColor] set];
[stopSign fill];

// 绘制路径
[[NSColor whiteColor] set];
[stopSign setLineWidth: 5];
[stopSign stroke];
```

本节中的代码组合起来，产生的结果如图 12-9 所示。

![](img/ea40cad434a338535474e82c1a6ace20_258_0.png)

## 绘制文本

除了形状和路径外，Cocoa 在图形中显示文本方面也相当擅长。在开始绘制文本之前，你需要将该文本加载到一个 **NSString** 变量中。例如，要为停车标志添加 ***STOP*** 字样，请遵循以下步骤：

- 1. 创建 `NSString` 变量：

  ```
  NSString *theString;
  theString = @"STOP";
  ```

- 2. 确定要在视图中显示文本的位置，并将该位置存储在一个 `NSPoint` 中：

  ```
  NSPoint theTextPos;
  theTextPos = NSMakePoint(275, rect.size.height-150);
  ```

- 3. 使用 `drawAtPoint` 方法绘制字符串，并传入 `NSPoint`：

  ```
  [theString drawAtPoint:theTextPos withAttributes:nil];
  ```

这行代码在由 `NSPoint` 确定的位置绘制文本。当你运行该示例时，可能会像图 12-10 所示的那样对结果感到失望。***STOP*** 字符串显示为非常小的字体，且字母为黑色，这是默认的文字设置。

