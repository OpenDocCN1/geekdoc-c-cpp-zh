

一个产生 Double 值的动画。由于存在多种不同的属性类型，System.Windows.Media.Animation 命名空间中有多个动画类。它们都遵循严格的命名约定；因此，可以分为以下三个部分：

- 基本动画
- 关键帧动画
- 路径动画

让我们详细讨论这些。

## 基本动画

WPF 中的基本动画在两个目标值之间创建过渡。它在起始值和目标值之间进行动画。动画的 From 属性定义了动画的起点。结束值是通过设置动画的 To 属性来定义的。动画的 By 属性指定一个偏移值。你可以使用 From、To 和 By 属性，它们可以一起使用或单独使用来确定动画目标值。From、To 和 By 属性的结果行为列在表 12.33 中：

表 12.33：属性的结果行为
| 属性 | 结果行为 |
|---|---|
| From | 表示动画从 From 属性指定的值进展到正在动画的属性的基础值或前一个动画的输出值 |
| From 和 To | 表示这两个属性一起使动画从 From 属性指定的值进展到 To 属性指定的值 |
| From 和 By | 表示这两个属性一起使动画从 From 属性指定的值进展到 From 属性和 By 属性之和指定的值 |
| To | 表示动画从正在动画的属性的基础值或前一个动画的输出值进展到 To 属性指定的值 |
| By | 表示动画从正在动画的属性的基础值或前一个动画的输出值进展到该值与 By 属性指定的值之和 |

> NOTE
> 如果你在同一个动画中设置 To 和 By 属性，.NET Framework 4.0 会忽略 By 属性执行的任务。

## 关键帧动画

与基本动画相比，关键帧动画是更好的动画选择。在关键帧动画中，你可以对目标属性的值进行动画，并可以指定两个或多个目标值。目标值使用 KeyFrames 集合来描述。要指定动画目标值，你需要创建 KeyFrames 对象并将其添加到动画 KeyFrames 集合中。要使用关键帧动画指定动画，你需要遵循特定的顺序：

- 声明一个动画并指定其持续时间
- 创建适当类型的 KeyFrames 对象，并为每个目标值设置其值和 KeyTime 结构，然后将其添加到 KeyFrames 集合中
- 将动画与属性关联以完成动画过程

针对不同属性类型的不同关键帧动画类列在表 12.34 中：

表 12.34：关键帧动画类
| 属性类型 | 动画类 |
|---|---|
| Boolean | BooleanAnimationUsingKeyFrames |
| Byte | ByteAnimationUsingKeyFrames |
| Color | ColorAnimationUsingKeyFrames |
| Decimal | DecimalAnimationUsingKeyFrames |
| Double | DoubleAnimationUsingKeyFrames |
| Int16 | Int16AnimationUsingKeyFrames |
| Int32 | Int32AnimationUsingKeyFrames |
| Int64 | Int64AnimationUsingKeyFrames |
| Matrix | MatrixAnimationUsingKeyFrames |
| Object | ObjectAnimationUsingKeyFrames |
| Point | PointAnimationUsingKeyFrames |
| Quaternion | QuaternionAnimationUsingKeyFrames |
| Rect | RectAnimationUsingKeyFrames |
| Rotation3D | Rotation3DAnimationUsingKeyFrames |
| Single | SingleAnimationUsingKeyFrames |
| String | StringAnimationUsingKeyFrames |
| Size | SizeAnimationUsingKeyFrames |
| Thickness | ThicknessAnimationUsingKeyFrames |
| Vector3D | Vector3DAnimationUsingKeyFrames |
| Vector | VectorAnimationUsingKeyFrames |

关键帧动画的基本目的是指定 Value 和 KeyTime 属性。Value 属性指定 KeyFrames 集合的目标值；而 KeyTime 属性指定 KeyFrames 集合的 Value 属性被满足的时间。当关键帧动画开始时，它会按 KeyTime 属性定义的顺序迭代其关键帧。如果在时间 0 没有关键帧，动画会在目标属性的当前值和第一个关键帧的 Value 之间创建过渡。

> NOTE
> 如果你将动画持续时间设置为 Automatic 或等于最后一个关键帧的时间，动画就会结束。

你将在本章的 Immediate Solutions 部分了解更多关于关键帧动画及其实际应用。

## 路径动画

路径动画是通过使用几何路径生成输出值来实现的。它用于沿复杂路径移动或旋转对象。基于路径的动画修改一个值以对应于 PathGeometry 对象描述的形状。它主要用于沿路径移动元素。路径动画可用于修改任何具有正确数据类型属性。它在动画与位置相关的属性时最有用。当你创建路径动画时，你不提供起始和结束值，而是提供 PathGeometry 类。构成路径的线条和曲线的集合决定了用于动画属性的值。

> NOTE
> 基于路径的动画始终以连续的速度运行。路径的总长度和你指定的持续时间决定了速度。

## 动画类

你已经了解了 WPF 中的不同类型的动画，例如基本动画、关键帧动画和路径动画。虽然 WPF 目前使用这三种类型的动画，但你可以使用完全不同的方法创建更多修改值的动画类。这些不同类型的动画包含在 System.Windows.Media.Animation 命名空间中。 broadly speaking，有两种动画：

- 那些在起始值和结束值之间按增量变化属性的
- 那些使属性从一个值突然改变到另一个值的

System.Windows.Media.Animation 命名空间中可用的不同类型的动画类列在表 12.35 中：

表 12.35：System.Windows.Media.Animation 命名空间的类

| 类 | 描述 |
|---|---|
| Animatable | 提供动画支持 |
| AnimationClock | 维护 AnimationTimeline 对象的运行状态并处理其输出值 |
| AnimationException | 在动画属性时发生错误时抛出 |
| AnimationTimeline | 定义产生输出值的时间段 |
| BeginStoryboard | 开始 Storyboard 时间线并将其动画分发到其目标对象和属性 |
| BooleanAnimationUsingKeyFrames | 在指定的持续时间内沿一组 KeyFrames 对象对采用布尔值的属性的值进行动画 |
| BooleanKeyFrame | 为 BooleanAnimationUsingKeyFrames 对象定义具有其自身目标值和插值方法的段 |
| BooleanKeyFrameCollection | 表示 BooleanKeyFrame 对象的集合 |
| ByteAnimation | 在指定的持续时间内使用线性插值在两个目标值之间对 Byte 属性的值进行动画 |
| ByteAnimationUsingKeyFrames | 沿一组 KeyFrames 对象对 Byte 属性的值进行动画 |
| ByteKeyFrame | 为 ByteAnimationUsingKeyFrames 对象定义具有其自身目标值和插值方法的动画段 |
| ByteKeyFrameCollection | 表示 ByteKeyFrame 对象的集合 |
| CharAnimationUsingKeyFrames | 在指定的持续时间内沿一组 KeyFrames 对象对 Char 属性的值进行动画 |
| CharKeyFrame | 为 CharAnimationUsingKeyFrames 对象定义具有其自身目标值和插值方法的动画段 |
| CharKeyFrameCollection | 表示 CharKeyFrame 对象的集合 |
| Clock | 为 Timeline 对象维护运行时计时状态 |
| ClockCollection | 表示 Clock 对象的有序集合 |
| ClockController | 交互式控制 Clock |
| ColorAnimation | 在指定的持续时间内使用线性插值在两个目标值之间对 Color 属性的值进行动画 |
| ColorAnimationBase | 对 Color 值进行动画 |
| ColorAnimationUsingKeyFrames | 在指定的持续时间内沿一组 KeyFrames 对象对 Color 属性的值进行动画 |

