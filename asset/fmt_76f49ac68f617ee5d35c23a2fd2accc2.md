
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

- 2. **定义路径上的各个点后，使用 `NSBezierPath` 类的 `bezierPath` 类方法创建 `NSBezierPath`。**

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

- 4. **使用 `closePath` 函数闭合路径：**

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

除了形状和路径外，Cocoa 在图形中显示文本方面也相当擅长。在开始绘制文本之前，你需要将该文本加载到一个 `NSString` 变量中。例如，要为停车标志添加 ***STOP*** 字样，请遵循以下步骤：

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

![](img/ea40cad434a338535474e82c1a6ace20_259_0.png)

图 12-10：到目前为止，这看起来并不太像一个停车标志。

显然，你需要定义字体的外观。为了实现这一点，请在 `drawAtPoint` 函数的 `withAttributes` 参数中传递非 nil 的值。`withAttributes` 参数接受一个 `NSDictionary`，因此你需要声明并创建一个这样的对象。

`NSMutableDictionary` 是用于存储项目集合的容器；在这种情况下，它是文本属性集合的容器。`NSMutableDictionary` 是 `NSDictionary` 的子类，因此它可以替代 `NSDictionary` 使用。可变对象是指在你创建它之后某时仍可以更改的对象。不可变对象是指在你创建它之后无法更改的对象。可变对象（例如 `NSMutableDictionary`）的名称中包含 mutable（可变）。不可变对象（例如 `NSDictionary`）则不包含。

按照以下步骤定义你的字体：

- 1. 创建一个 `NSMutableDictionary`：

在此情况下，由于你使用的是预定义的一组属性，因此可以使用不可变字典。

```objective-c
NSMutableDictionary *theAttributes;
//create the NSDictionary object
theAttributes = [[NSMutableDictionary alloc] init];
```

- 2. 添加代表某些文本属性的对象到 `NSMutableDictionary` 中。

例如，要将字体设置为 62 号的 Helvetica（赫尔维提卡字体），请使用类似以下的代码：

```objc
[theAttributes setObject:
    [NSFont fontWithName: @"Helvetica" size: 62]
          forKey: NSFontAttributeName];
```

- 3. 设置文本的颜色。

此代码向 `NSDictionary` 添加了白色文本颜色属性：

```objc
[theAttributes setObject:
    [NSColor whiteColor] forKey:
        NSForegroundColorAttributeName];
```

- 4. 当你完成向 `NSDictionary` 对象添加文本属性后，将该字典对象传递给 `drawAtPoint` 函数的 `withAttributes` 参数：

```objc
[theString drawAtPoint:theTextPos withAttributes:
    theAttributes];
```

- 5. 释放 `NSDictionary`：

```objc
[theAttributes release];
```

在停车标志上绘制字符串的组合代码如下所示。注意，`theTextPos` 的第一个参数值为 267 而不是 275，这是为了适应较大的 Helvetica 字体。

```objc
//**********************************
//      DRAW STOP SIGN TEXT
//**********************************

//Define a string
NSString *theString;
theString = @"STOP";

//Position the text
NSPoint theTextPos;
theTextPos = NSMakePoint(267, rect.size.height-150);

//Create the NSDictionary object
NSMutableDictionary *theAttributes;
theAttributes = [[NSMutableDictionary alloc] init];

//Add attributes to the NSDictionary
[theAttributes setObject:
    [NSFont fontWithName: @"Helvetica" size: 62]
          forKey: NSFontAttributeName];

[theAttributes setObject:  
    [NSColor whiteColor] forKey:
    NSForegroundColorAttributeName];

//Draw the text
[theString drawAtPoint:theTextPos withAttributes:
    theAttributes];

//Dispose of the NSDictionary
[theAttributes release];
```

你可以在图 12-11 中查看结果。

![](img/ea40cad434a338535474e82c1a6ace20_261_0.png)

## 显示图像

最终，你会厌倦自己创建图形，而希望改为显示图像文件。在 Cocoa 应用程序中显示图像文件最简单的方法是直接将文件添加到项目中。例如，如果你从访达（Finder）中将 `face.jpg` 图像拖放到 Xcode 中，你的项目可能如图 12-12 所示。

![](img/ea40cad434a338535474e82c1a6ace20_262_0.png)

图 12-12：将图像从访达拖入你的项目以方便访问。

要在视图中绘制此图像，你只需要添加几行代码：

- 1. **创建一个 `NSPoint` 来保存你希望显示图像的坐标。**

此代码为视图的左下角创建了一个 `NSPoint`：

```objectivec
NSPoint theImagePos;
theImagePos = NSMakePoint(0, 0);
```

- 2. **创建一个 `NSImage` 对象并将图像加载到其中。**

```objectivec
NSImage* theImage;
theImage = [NSImage imageNamed:@"face.jpg"];
```

- 3. **通过调用 `dissolveToPoint` 函数在视图中显示图像。**

```objectivec
[theImage dissolveToPoint: theImagePos
    fraction:(1.0)];
```

图 12-13 展示了 `dissolveToPoint` 函数的实际效果。

`dissolveToPoint` 函数的 `fraction` 参数代表图像的透明度。你使用的 `fraction` 值越小，图像就越透明。值 1.0 表示不透明；值 0.0 表示完全透明。图 12-14 展示了不同透明度设置的效果。

![](img/ea40cad434a338535474e82c1a6ace20_263_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_263_1.png)

要查看透明度是如何工作的，请将以下代码添加到你的 `drawRect` 函数末尾：

```objective-c
NSPoint theImagePos;
theImagePos = NSMakePoint(0, 0);

NSImage* theImage;
theImage = [NSImage imageNamed:@"face.jpg"];

int i;
for (i=3; i<7; i++)
{
    [theImage dissolveToPoint: theImagePos
        fraction:(i*0.1)];
    theImagePos.x = theImagePos.x + 130;
}

theImagePos = NSMakePoint(0, 130);
for (i = 7; i<=10; i++)
{
    [theImage dissolveToPoint: theImagePos
        fraction:(i*0.1)];
    theImagePos.x = theImagePos.x + 130;
}
```

> **在这个示例中，你使用了字面量值 130 来定位屏幕上的元素。这仅仅是为了演示目的，使代码更易于阅读，但在实际环境中不要这样做。相反，应根据视图的高度和宽度来确定数值。**

![](img/ea40cad434a338535474e82c1a6ace20_264_0.png)

# 第 13 章

## 管理你的文件

### 本章内容
