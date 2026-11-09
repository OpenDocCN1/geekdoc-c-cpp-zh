
单击 + 按钮。会看到图 16.16 所示的面板。选择“模糊”，然后选择“高斯模糊”。单击“好”将滤镜添加到视图中。

**图 16.16** 从列表中选择并添加滤镜。滤镜按功能分组。要查看完整列表，请选择“全部”组。

![](img/2b293e29fc15b0797f113b85dd429b6e_452_0.png)

图 16.17 显示了结果。选中 Bezier View 旁边的复选框以启用效果。在“详细信息”标签页中，可以更改滤镜的设置。将 Radius 改为 4 左右的值。滑块未按精确值校准，但 3 到 5 之间的任何值都可以接受。

> **注意**
>
> 从技术上讲，CoreImage 是 CoreAnimation 系统的一部分，因此窗口顶部的提示要求你**启用 CoreAnimation 渲染**。选中顶部视图旁边的复选框以启用 CoreAnimation。

**图 16.17** 设置滤镜详细信息——控制每个滤镜属性的具体值。高斯模糊滤镜只有一个 Radius 属性。有些滤镜根本没有属性。另一些则有六个或更多属性。

![](img/2b293e29fc15b0797f113b85dd429b6e_453_0.png)

保存 nib 文件。构建并运行应用程序。图 16.18 显示了内容如何经过模糊滤镜处理。现在可以尝试其他滤镜，也可以通过添加多个滤镜来创建组合效果。使用 – 按钮移除滤镜。可以通过拖放更改滤镜效果的顺序。

按照类似步骤为视图背景设置滤镜效果。Aqua 的菜单系统利用此功能模糊菜单后面的内容，营造出漂浮的半透明效果。

## 设置用于处理的滤镜

本书附带的 Twirl Filter 项目演示了如何将滤镜应用到上下文的内容。在此示例中，代码从应用程序包中加载图像，对其进行处理，并将其绘制到视图中。结果与在 IB 中向视图应用滤镜相同。但你可以使用类似技术将滤镜应用到不可见的离屏上下文；例如，实现图像的批处理。

**图 16.18** 滤镜运行后，Bezier 路径的锐利线条被纤细的模糊效果取代。Radius 参数控制模糊量。这是单个滤镜的输出，但你可以几乎无限地组合滤镜，以创建复杂的多重效果。

![](img/2b293e29fc15b0797f113b85dd429b6e_454_0.png)

图 16.19 显示了应用程序的 nib 和 UI。Filter Browser View 和 Filter View 都是 NSView 的子类。Browser View 管理界面。它响应应用程序窗口内的 mouseDown: 事件，并实现两个与两个滤镜参数关联的滑块。此视图用于管理 UI，其 drawRect: 方法不会被使用。

Filter View 从 UI 接收设置，并实现滤镜。通过调用 CIFilter 的 filterWithName: 方法创建滤镜对象：

```
CIFilter *thisFilter =
    [CIFilter filterWithName: @"CITwirlDistortion"];
```

CIFilter 参数通过键值编码访问：

```
[thisFilter setValue: [NSNumber numberWithFloat: 50]
           forKey: @"inputRadius"];
```

**图 16.19** Twirl Filter 应用程序的 nib 和视图结构。它是一个标准内容视图，外加一个额外的滤镜视图和一对滑块。

![](img/2b293e29fc15b0797f113b85dd429b6e_455_0.png)

## 查找滤镜键

每个滤镜都有不同的一组键，列在《Core Image 滤镜参考指南》中。在 Twirl Filter 项目中，这些键硬编码在代码中，并由另一个视图控制。还可以在代码中使用 `inputKeys` 方法读取任何滤镜的键。它会生成一个字符串键名数组：

```
NSArray *keyNames = [thisFilter inputKeys];
```

这个列表不足以创建有用的 UI，因为它不会告诉你每个值的最大或最小范围。要获取该信息，请使用 `attributes` 方法返回一个字典：

```
NSDictionary *filterAttributes = [thisFilter attributes];
```

该字典列出：

- 滤镜所属的类别。类别是滤镜的功能分组；例如，扭曲、视频、静态图像等。类别名称在参考指南中定义。
- 滤镜名称。
- 键名列表。
- 每个键的属性列表，包括可接受的最大值和最小值以及值类型。

## 创建滤镜控制器界面

理论上，你可以使用这些信息创建一个完全通用的滤镜包装器。在实践中，字典格式很复杂，创建通用的自动化 UI 是一项具有挑战性的工程。

有一种更简单的解决方案。对任何滤镜运行 `viewForUIConfiguration:` 方法，都会自动生成完整的控制器视图，其中包含适当的滑块、颜色选择器和其他 UI 功能。你可以指定各种大小的控制器视图，也可以排除特定参数；例如，你可能会选择单独实现图像源选择器。使用 `addSubview:` 或 `replaceSubview:` 将控制器视图嵌入容器视图。

图 16.20 显示了一个简单的原型示例。UI 控件出现在右下角。该 UI 设计更注重功能而非样式，而且你必须使用绑定将 UI 元素链接到滤镜参数。但你可以使用此方法以相对较少的编码工作自动生成滤镜控件。

**图 16.20** 使用 `viewForUIConfiguration:` 创建滤镜界面。自动生成的视图出现在窗口右下角。

![](img/2b293e29fc15b0797f113b85dd429b6e_456_0.png)

## 将滤镜应用到图像

Twirl Filter 示例中的 drawRect: 方法演示了如何设置滤镜的输入值和输出值，以及如何应用滤镜。输入图像通过 inputImage 键设置。

图像对象必须是 CIImage——CoreImage 特有的一种特殊图像类型。在此示例中，图像数据通过 URL 路径从文件加载。

对于更通用的解决方案，将源图像转换为位图或 NSData 对象，并使用 imageWithBitmap: 或 imageWithData: 方法加载 CIImage 对象。

处理来自视图的数据的最简单方法——不将滤镜添加到 IB 中的视图——是从 CGLayer 对象读取数据。

这些转换选项在实践中可能很麻烦。在某些应用程序中，你需要通过各种中间数据类型转换图像。但它们使对其他图形框架生成的图像应用滤镜成为可能。

运行该滤镜的 drawRect: 方法如下：

```objc
- (void)drawRect:(NSRect)viewRect {
    thisContext = [[NSGraphicsContext currentContext] CIContext];
    preFilterImage =
        [CIImage imageWithContentsOfURL:sourceImageURL];
    [thisFilter setValue: preFilterImage forKey: @"inputImage"];
    thisCenter =
        [CIVector vectorWithX: filterCenter.x Y: filterCenter.y];
    [thisFilter setValue:thisCenter forKey:@"inputCenter"];
    [thisFilter setValue:
        [NSNumber numberWithFloat: filterSize]
    forKey:@"inputRadius"];
    [thisFilter setValue:
        [NSNumber numberWithFloat: filterAngle]
    forKey:@"inputAngle"];
    postFilterImage = [thisFilter valueForKey:@"outputImage"];
    CGRect preRect = [preFilterImage extent];
    CGPoint anImageOrigin =
        CGPointMake(viewRect.size.width*.5 - preRect.size.width*.5,
                    viewRect.size.height*.5 - preRect.size.height*.5);
    [thisContext drawImage: postFilterImage
                   atPoint:anImageOrigin
                   fromRect:preRect];
}
```

代码的关键点包括：

- `filterAngle`、`filterCenter` 和 `filterSize` 的值由控制器视图提供。
- 滤镜输出由特殊的 `CIContext` 对象管理。它的工作方式类似 `CGContext` 或 `NSGraphicsContext`，但包含一个特殊的 `drawImage:` 方法，该方法将输出绘制到上下文中，并由此绘制到周围的视图中。
- `CIVector` 数据类型用于定义点。滤镜不能使用 `NSPoint` 或 `CGPoint`。
- 输入和输出图像数据存储在两个 `CIImage` 对象中，分别称为 `preFilterImage` 和 `postFilterImage`。
- 通过触发最后一行中的 `drawImage:` 方法来运行滤镜。在调用此方法之前，不会进行任何过滤。此方法运行滤镜，然后将数据写入上下文中指定的点；而几乎完全不一致的是，该点被指定为 `CGPoint`，而不是 `CIVector`。

该应用程序如图 16.21 所示。在滤镜视图中单击可设置滤镜中心，滑块控制滤镜参数。你可以使用类似代码实现任何其他 CoreImage 滤镜，设置不同的键和值，并根据需要从控制器中添加或移除参数滑块。

**图 16.21** 完成后的 Twirl Filter。创建这个简单的滤镜效果并不是一项完全简单的挑战。

![](img/2b293e29fc15b0797f113b85dd429b6e_458_0.png)

> **警告**
>
> CoreImage 并不稳健。如果因为提供无效值或键而导致滤镜崩溃，整个框架会停止工作，所有滤镜效果也会随之停止。重新启动它的唯一方法是重新启动应用程序。必须仔细调试代码以避免使 CoreImage 崩溃。
