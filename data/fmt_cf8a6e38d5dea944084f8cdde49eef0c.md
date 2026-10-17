
```swift
ball.position.y <= ball.size.y / 2 // collision with
ball.position.y = ball.size.y / 2
ballVelocity = ballVelocity * -1 * bounciness
```

编译并运行，你的小球将与网格碰撞，正好在小球的边缘。

## 关键帧 (Keyframes)

如果你想制作小球来回跳动的动画，你需要输入其随时间变化的位置。对于这种输入，你需要设置一个位置数组并为指定的时间提取正确的位置。

在`BallAnimations.swift`中，在`Utility`组中已经有一个名为`ballPositionXArray`的数组。该数组由 60 个从 -1 到 1 然后再回到 -1 的值组成。通过计算当前帧，你可以从数组中获取正确的位置。

在`Renderer.swift`中，将`update(deltaTime:)`修改为：

```swift
func update(deltaTime: Float) {
    let currentTime += deltaTime
    let ball = models[0]
    ball.position.y = ball.size.y

    let fps: Float = 60
    let currentFrame =
    Int(currentTime * fps) % (ballPositionXArray.count)
    ball.position.x = ballPositionXArray[currentFrame]
}
```

在这里，基于 60 fps（每秒帧数）计算当前帧，并从数组中提取正确的值。

![](img/655c9de9cdb851b3baacdbce4a1fae64_220_0.png)

编译并运行。观察小球在 60 帧内以机械的往复运动移动。这与正弦动画的结果几乎相同，但现在它是由一个你可以控制和复用的值数组驱动的。

## 插值 (Interpolation)

为每一帧输入一个值是一项大量的工作。如果你只是让物体从 A 点直线移动到 B 点，你可以对值进行插值。插值是在给定一个值范围和该范围内的当前位置时计算出一个值。在制作动画时，当前位置是当前时间占动画持续时间的百分比。

要计算时间百分比，使用此公式：

```swift
time = (currentTime - min) / (max - min)
```

这会产生一个 0 到 1 之间的时间值。

例如，如果你有一个起始值 5，结束值 10，持续时间为 2 秒，在经过 1 秒后，插值值为 7.5。

```swift
time = (1.0 - 0) / (2.0 - 0)
value = (10 - 5) * time + 5
```

这是线性插值。然而，还有其他插值不同公式的方法。

![](img/655c9de9cdb851b3baacdbce4a1fae64_221_0.png)

![](img/655c9de9cdb851b3baacdbce4a1fae64_221_1.png)

在上面的图中，线性插值在左侧。x 轴是时间，y 轴是值。你在适当的时间采样该值。之前的的小球示例是机械的，可以使用右侧的淡入淡出（ease in and out）插值进行改进。

使用淡入淡出后，小球在开始时缓慢加速，然后在动画结束时减速。

你不需要为每一帧创建一个值来制作小球动画，只需要持有关键位置。这些将是姿态的极端值。在小球示例中，极端姿态位置是 -1 和 1。你还将持有与该关键值时间匹配的关键时间。例如，如果你的动画长度为 2 秒。

首先，创建一个结构体来持有时间和值：

```swift
struct Keyframe {
    var time: Float
    var value: float3
}
```

然后，创建一个`Animation`类来管理关键帧：

```swift
class Animation {
    var translations: [Keyframe] = []
    var repeatAnimation: Bool = false

    func getTranslation(at time: Float) -> float3? {
        guard !translations.isEmpty else { return nil }
        
        var currentTime = time
        if repeatAnimation {
            currentTime = fmod(time, translations.last!.time)
        }
        
        for i in 0..<translations.count - 1 {
            let start = translations[i]
            let next = translations[i+1]
            if currentTime >= start.time && currentTime <= next.time {
                let t = (currentTime - start.time) / (next.time - start.time)
                return mix(start.value, next.value, t)
            }
        }
        return translations.last?.value
    }
}
```

现在，在`BallAnimations.swift`中填充关键帧：

```swift
func generateTranslations() -> [Keyframe] {
    var animation = Animation()
    animation.translations.append(Keyframe(time: 0, value: float3(-1, 0, 0)))
    animation.translations.append(Keyframe(time: 1, value: float3(1, 0, 0)))
    animation.translations.append(Keyframe(time: 2, value: float3(-1, 0, 0)))
    return animation.translations
}
```

(注：原文后续部分存在大量 OCR 识别错误和重复，译文已根据逻辑进行了整合与去重。)

## 欧拉角旋转

现在你已经让球在空中移动了，你可能也想让它旋转。为了表示对象的旋转，你有一个包含 x、y 和 z 轴旋转角的`float3`。这些角度被称为用数学家莱昂哈德·欧拉（Leonhard Euler）命名的欧拉角。欧拉是欧拉旋转定理的创立者，该定理指出任何旋转都可以用三个旋转角来描述。对于单个旋转这是可以的，但在这三个值之间进行插值并不如你想象的有效。

为了创建一个旋转矩阵，你一直在`Metal.swift`的数学库中调用此函数：

```swift
init(rotation angle: float3) {
  let rotationX = float4x(rotationX: angle.x)
  let rotationY = float4x(rotationY: angle.y)
  let rotationZ = float4x(rotationZ: angle.z)
  let self = rotationX * rotationY * rotationZ
}
```

在这里，最终的旋转矩阵是由三个按特定顺序相乘的旋转矩阵组成的。这个顺序并不是固定的，它是六种可能顺序之一。根据乘法顺序的不同，你会得到不同的旋转。

> 注意：有时（例如在飞行模拟器中），这些旋转被称为偏航（Yaw）、俯仰（Pitch）和滚滚（Roll）。取决于你的参考系，如果你使用 y 轴垂直向上（记住这并不是通用的），那么偏航是绕 y 轴旋转，俯仰是绕 x 轴旋转，滚滚是绕 z 轴旋转。

对于单个渲染引擎内的静态对象，这是可以。主要问题出现在动画以及这些角度的插值上。

当你进行旋转插值时，如果两个轴对齐，你就会遇到名称可怕的“万向锁”（gimbal lock）。

![](img/655c9de9cdb851b3baacdbce4a1fae64_225_0.png)

这意味着你丢失了一个旋转轴。因为内轴旋转是建立在外轴旋转之上的，两个旋转发生了重叠。这导致了异常的插值。

## 四元数

在不强制顺序的情况下，如果不涉及第四维度，相乘 x、y 和 z 旋转是不可能的。1843年，威廉·罗文·汉密尔顿爵士（Sir William Rowan Hamilton）正是这样做的！他在都柏林的一座桥上的石头上刻了他的四元数乘法基本公式：

```swift
i^2 = j^2 = k^2 = ijk = -1
```

该公式使用四维向量和复数来描述旋转。数学原理很复杂，幸运的是，你不需要理解四元数的工作原理就可以使用它们。四元数的主要优点是：

- 当使用球面线性插值（或 slerp）时，它们可以正确插值。

- 它们永远不会丢失控制轴。

- 除非你明确要求长路径，否则它们总是采取两个旋转之间的最短路径。

> 注意：如果你对研究四元数的内部感兴趣，`references.markdown` 包含了进一步阅读的内容。

你不需要编写任何复杂的插值代码，因为`simd`提供了四元数类和方法可以使用`simd_slerp()`为你处理一切。四元数按照此处描述的那样沿最短路径进行球面插值：

![](img/655c9de9cdb851b3baacdbce4a1fae64_226_0.png)

# 第8章：角色动画

在`simd`内部，四元数是包含四个元素的向量，但 Apple 建议将它们视为抽象的数学对象，而不是深入内部存储。这让你免于学习四元数的最后一个元素是实部、前三个元素是虚部的麻烦。

你将旋转从欧拉角切换到四元数。利用`simd`四元数与旋转矩阵之间的转换，这种切换是轻而易见的。在`Node.swift`中，添加此属性：

```swift
var quaternion = simd_quatf()
```

在你定义矩阵的地方，将`rotateMatrix`的定义改为：

```swift
let rotateMatrix = float4x4(quaternion)
```

现在你的 Nodes 将支持四元数而不是欧拉角。你应该改变旋转以更新四元数。将旋转更改为：

```swift
var rotation: float3 = [0, 0, 0] {
  didSet {
    let rotateMatrix = float4x4(rotation)
    quaternion = simd_quatf(rotationMatrix)
  }
}
```

当你设置模型的旋转时，这保持了四元数值的值。

要使用四元数旋转进行动画，你将重复对平移的操作。在`Animation.swift`中，添加此结构体（顶层）来保存关键帧：

```swift
struct KeyQuaternion {
  var time: Float = 0
  var value = simd_quatf()
}
```

为`Animation`添加一个新属性：

```swift
var rotations: [KeyQuaternion] = []
```

复制`getTranslation(at:)`，并将所有的平移和浮点数替换为旋转和四元数：

```swift
func getRotation(at time: Float) -> simd_quatf {
  guard let lastKeyframe = rotations.last else {
    return nil
}
var currentTime = time
if first = rotations.first, first.time >= currentTime {
    return first.value
}
if currentTime >= lastKey.time, !repeatAnimation {
    return lastKey.value
}
currentTime = fmod(currentTime, lastKey.time)
let keyFramePairs = rotations.indices.dropFirst().map {
    (previous: rotations[$0 - 1], next: rotations[$0])
}
guard let (previousKey, nextKey) = keyFramePairs.first else { return nil }
if currentTime < nextKey.time {
    let interpolant = (currentTime - previousKey.time) / (nextKey.time - previousKey.time)
    return simd_slerp(previousKey.value, nextKey.value, interpolant)
}
return lastKey.value
}
```

注意这里你将插值函数改为使用`simd_slerp`而不是`simd_mix`。这没有使用球面线性插值。

在`BallAnimations.swift`中，取消`generateBallRotations()`方法的注释。它包含旋转关键帧数组。旋转从 0 开始，在 3.5 秒内绕 z 轴旋转 90 度。

对于球的最终旋转，在`Renderer.swift`中，将`update(deltaTime:)`改为：

```swift
func update(deltaTime: Float) {
    currentTime += deltaTime
    let ball = models[0]
    
    var animation = Animation()
    animation.translations = generateBallRotations()
    animation.rotations = generateBallRotations()
    ball.position = animation.getTranslation(at: currentTime)
        ?? float3(repeating: 0)
    ball.position.y += ball.size / 2
    ball.quaternion = animation.getRotation(at: currentTime)
        ?? simd_quatf()
}
```

构建并运行，你的球会带有旋转移动。

![](img/655c9de9cdb851b3baacdbce4a1fae64_229_0.png)

如果你在做更复杂的动画，你可能想在 3D 应用中完成。海滩球实际上在其 USD 文件中包含了一些动画。

# USD 和 USDZ 文件

要克服的一个大问题是从 3D 应用导入动画。USD 是由 Pixar 设计的格式，可以包含带有纹理、动画和光照的海量场景。有多种扩展名：

- **usd**: 通用场景描述 (USD) 文件由资产或链接组成，允许多个艺术家在同一个场景中工作。该文件可以包含网格、着色信息、模型、相机和光照。

- **usdz**: 单个归档文件，包含了渲染模型所需的所有文件（而不只是链接）。

- **usda**: 该文件是文本格式的 USD 文件。本章中的模型使用的是 usda 格式，以便你用 TextEdit 打开并检查内容。

- **usdc**: 该文件是二进制格式的 USD 文件。

Apple 已采用 USDZ（USD 的归档衍生）作为其首选的增强现实 3D 格式。然而，目前还没有多少 3D 应用支持导出 USD。Maya 和 Houdini 支持，Blender 不支持。

Apple 提供了一套 USD Python 工具，包括一个名为`usdconvert`的应用程序，它可以从支持的格式转换为 USD。目前支持的格式包括 .obj, .fbx, .abc 和 .gTF。

> 注意：你可以在 AR Quick Look Gallery 页面的底部下载工具：https://developer.apple.com/augmented-reality/quick-look/ 这是一个 USDZ 工具，用于转换、生成、验证和检查 .usds 文件。

gTF 是由 Khos Group 开发的，并开源了该格式，任何人都可以在自己的引擎中使用。http://sketchfab.com 是 3D 模型的主要供应商和展示平台；你所有可下载的模型都以 gTF 格式提供，其中许多可以使用 Apple 的 usdconvert 转换为 USD。

# 制作网格动画

`beachball.usda` 文件包含了平移和旋转动画，且 Model I/O 可以提取这些动画。初始化这些信息有几种方法，你将在本章中使用其中两种。Model I/O 组件并不允许你直接访问旋转和和平移值，但它为你提供了一个方法，可以返回特定时间的变换矩阵。对于网格变换动画，你将在模型加载过程中提取动画中每一帧的动画数据。

稍后，当你定义骨骼动画时，你将能够访问关节的旋转和平移值，因此你只需要在有关键帧的地方加载数据，并由你的插值方法对每一帧进行插值。

> 注意：在编写自己的引擎时，你可以选择为每一帧加载这些动画数据以匹配变换动画。你应该考虑游戏的需求以及你的模型包含的内容。通常，将加载代码提取到单独的 App 中更高效，该 App 将材质、纹理和动画数据加载并保存为匹配你游戏引擎的高效格式。这种资产流水线的良好示例是 Apple 的视频和示例代码《From Art to Engine with Model I/O》https://developer.apple.com/videos/play/wwdc2017/610/

你将以固定的 fps（通常为 60 fps）运行游戏，并为动画的每一帧保留一个变换矩阵。

# Metal 教程第 8 章：角色动画
