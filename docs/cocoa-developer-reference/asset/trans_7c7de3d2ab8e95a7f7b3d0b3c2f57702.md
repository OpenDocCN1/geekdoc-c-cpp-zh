
## 变换路径

除非你是数学专家，否则仿射变换中使用的矩阵计算并不简单。幸运的是，即使不理解仿射变换的工作原理，也很容易使用它们。要变换路径，请创建一个变换对象：

```
NSAffineTransform *aTransform = [NSAffineTransform transform];
```

这个略显不寻常的语法会创建一个默认的空变换，将其应用于对象时不会产生任何效果。然后，你可以使用缩放方法来创建调整路径大小的变换，使用旋转方法来旋转路径，并使用平移方法来移动路径。

例如：

```
[aTransform rotateByDegrees: 45];
```

创建一个将对象旋转 45 度的变换。类似地，

```
[aTransform translateXBy: xFloat yBy: yFloat];
```

创建一个移动对象的变换；以及

```
[aTransform scaleXBy: xFloat yBy: yFloat];
```

创建一个缩放对象的变换。

变换是累积的，因此你可以先缩放、再旋转，然后平移。顺序很重要：缩放和旋转围绕左下角原点进行。跟踪相对原点可能很有挑战性。通常，你会将对象平移到原点以进行缩放和旋转，然后再将它们平移回原始位置，或视图中其他某个点。复杂路径可能没有明确定义的中心。

要将变换应用于路径，请使用

```
NSBezierPath *newPath = 
    [aTransform transformBezierPath: anOldPath];
```

当你描边或填充 newPath 时，它会以平移后的位置出现，并经过缩放和旋转。

## 加载图像

要加载图像，请创建一个 NSImage 对象，并用文件中的图像数据初始化它。你可以指定任意文件路径，也可以将图像包含在应用程序包中，并直接从包中加载。图像编辑使用前一种方法，而定义自动加载并显示的图像则使用后一种方法。例如，要将图像包含在包中，请右键单击 Resources 组，然后选择 Add > Existing Files。导航到该文件，选中它，并将其复制到项目中，同时选择 Relative to Enclosing Group 引用类型，如图 16.12 所示。

**图 16.12**

将文件与项目一起打包。不要忘记选择 Relative to Enclosing Group Reference Type；否则，你的捆绑文件将无法正确捆绑。

![](img/2b293e29fc15b0797f113b85dd429b6e_446_0.png)

你可以在每次绘制图像时加载它，但这通常效率很低。更高效的做法是在 awakeFromNib 中加载一次，并在需要时引用它。例如：

```objective-c
NSImage *sourceImage;
- (void) awakeFromNib {
    NSString *sourceImagePath =
        [[NSBundle mainBundle] pathForResource:@"bi" ofType:@"jpg"];

    NSURL *sourceImageURL =
        [NSURL fileURLWithPath: sourceImagePath];
    sourceImage =
        [[NSImage alloc] initWithContentsOfURL: sourceImageURL]
            retain];
}
```

这会根据访问应用程序包的路径，为指定名称的文件创建一个 URL。`initWithContentsOfURL:` 方法将图像数据加载到 NSImage 实例中。

![](img/2b293e29fc15b0797f113b85dd429b6e_447_0.png)

> **注意**
>
> 你可以通过常规文件系统文件路径访问磁盘上其他位置的图像文件。应用程序包中的文件必须通过 URL 访问。这不太一致，但规则就是如此。

## 绘制图像

你可以在视图中的任意位置绘制图像对象。严格来说，图像并不是被绘制出来，而是被*合成*，即将图像数据与视图中现有的像素值组合起来。

如果你使用过图像编辑软件，那么你已经熟悉合成。它有时被称为*图层混合*。Cocoa 支持多种合成选项。你可以按原样合成图像，可以在合成后提取最大和最小像素值，也可以对图像执行 XOR 以创建极其花哨的迷幻效果。不透明度——透明度——可通过一个单独的参数控制，也称为 alpha。

要绘制图像，请对它调用 `drawInRect:` 方法。完整的方法签名指定一个目标矩形、一个源矩形、一个 *operation* 参数（取 Cocoa 预定义合成模式之一）以及一个介于 0 和 1 之间的 *fraction* 参数（定义不透明度/alpha）。

![](img/2b293e29fc15b0797f113b85dd429b6e_447_1.png)

> **提示**
>
> 为源矩形指定 `NSZeroRect` 是快速指定整个图像的一种方式。例如：

```objc
[sourceImage drawInRect:newRect fromRect:NSZeroRect
    operation:NSCompositeSourceOver fraction:0.5];
```

合成模式常量在 NSImage Class Reference 中定义。

图 16.13 展示了将图像与底层渐变组合并以 50% 不透明度绘制的结果。

![](img/2b293e29fc15b0797f113b85dd429b6e_447_2.png)

> **提示**
>
> 当调整图像大小时，它会自动进行插值——也就是说，原始像素信息会被扩展或缩小，以适应新的图像尺寸。你可以通过包含以下内容来设置插值质量：

```objc
[[NSGraphicsContext currentContext]
 setImageInterpolation:NSImageInterpolationHigh];
```

在 `drawRect:` 开头。

**图 16.13**

加载并合成图像。选择 `newRect` 矩形作为目标会在窗口调整大小时自动调整图像大小。将不透明度设置为 50% 可以让部分底层渐变透出。

![](img/2b293e29fc15b0797f113b85dd429b6e_448_0.png)

### 组合 Quartz、Core Graphics 和 Cocoa 图形

Cocoa 图形系统是底层基于 C 的框架 Quartz 2D 的封装。Cocoa 中使用的函数和数据结构在 Quartz 中有对应项，但前缀是 CG 而不是 NS。在操作上，这两个框架明显相似。Quartz 使用路径、颜色、点、渐变和矩形的方式几乎相同，区别在于 Quartz 功能通过函数调用而不是方法访问。Quartz 为图形提供更底层的支持，还使图像可以离屏绘制并作为纹理重复。它也可能明显快于 Cocoa 绘图代码，不过这在很大程度上取决于具体应用。

**图 16.14**

一个简单的应用程序，它在两点之间创建随机的多条贝塞尔路径，并使用一系列吸引人的颜色

![](img/2b293e29fc15b0797f113b85dd429b6e_450_0.png)

> **注意**
>
> 窗口背景已在应用程序委托中设置为黑色。

## 使用 CoreImage 滤镜

CoreImage 滤镜是一组预编写的图像滤镜插件，你可以将它们应用于任何视图的内容或背景。这些滤镜在文档中的 Core Image Filter Reference 里按名称列出，其中还包含预览图像。如果你有 Adobe Photoshop 的使用经验，许多效果会看起来很熟悉，但完整滤镜列表还包括一些尚未在行业标准图像编辑器中提供的新颖效果。

使用滤镜有三种方式：

- 你可以在 Interface Builder 中点击视图的 Inspector 窗口里的 Effects 标签页，将它们添加到任何视图。
- 你可以在 `drawRect:` 的子类实现中通过代码触发它们。
- 你可以编写 Objective-C 代码来组合现有滤镜或定义全新的效果。

创建和组合滤镜属于高级主题，超出了本书的范围。这里不会介绍它们。第一种方式非常容易使用，你可以用很小的精力为任何 UI 添加特殊效果。第二种方式更具挑战性，但可以通过相对简单的样板代码实现。

> **注意**
>
> CoreImage 效果对处理器要求较高，并且尚未在 iPhone 或 iPad 上提供。

### 在 Interface Builder 中添加 CoreImage 效果

作为基于视图的 CoreImage 效果的演示，你将扩展 MultiBezier 项目以包含这些效果。添加效果是一个简单的过程。

在 Doc 窗口中选择 BezierView。如果 Inspector 窗口不可见，请选择 Tools ▸ Inspector 将其打开。选择从左数第二个 Effects 标签页。找到 Content Filters 面板，如图 16.15 所示。

**图 16.15**

找到 Content Filters 面板，它会对视图内容应用一个或多个滤镜

![](img/2b293e29fc15b0797f113b85dd429b6e_451_0.png)

