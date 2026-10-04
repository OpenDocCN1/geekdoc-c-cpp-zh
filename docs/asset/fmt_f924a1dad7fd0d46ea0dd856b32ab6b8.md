
```swift
var rotation = float3(Float(-20).degreesToRadians(), 0, 0)
```

编译并运行，看到高度图位移了顶点。注意顶点是高高的，黑色的是低的：![](img/65c9de9cd851b3acdbce4a1fae64333.png)

这还没有很多细节，但很快就会改变。在`Renderer.swift`中，将`maxTessellation`常量改为：

```swift
static let maxTessellation: Int = {
#if os(macOS)
    return 64
#else
    return 16
#endif
}()
```

这是每个操作系统的最大值。由于 iOS 上的最大细分如此之低，你可能想增加在 iOS 上渲染的补片数量。将`patches`和`terrain`改为：

```swift
let patches = (horizontal: 6, vertical: 6)
var terrain = Terrain(size: [8, 8], height: 1,
    maxTessellation:
    UInt32(Renderer.maxTessellation))
```

你现在要在十六个区域上创建了三十六个补片。编译并运行查看你的补片高度映射成了一座壮丽的山。不要忘记点击线框模式查看你山脉的渲染效果。![](img/65c9de9cd851b3acdbce4a1fae64334.png)

## 按高度着色

在上一节中，你在顶点函数中采样了高度图，颜色在发送到片段着色器时会进行插值。为了获得最大的颜色细节，你需要每个片段采样一次纹理，而不是每个顶点。

为了实现这一功能，你需要设置三个纹理：雪、悬崖和草地。你把这些纹理发送到片段函数（fragment function）并在那里进行高度测试。

在`Renderer.swift`的`Renderer`中，添加三个新的纹理属性：

```swift
let cliffTexture: MTLTexture
let snowTexture: MTLTexture
let grassTexture: MTLTexture
```

在`init(metalView:)`中，创建高度图的闭包添加以下内容：

```swift
cliffTexture =
  try Renderer.loadTexture(imageName: "cliff-color")
snowTexture = try Renderer.loadTexture(imageName: "snow-color")
grassTexture =
  try Renderer.loadTexture(imageName: "grass-color")
```

这些是资源目录中的纹理。

要将纹理发送到片段函数`draw(in:)`，在`encoder draw`调用之前添加以下内容：

```swift
renderEncoder.setFragmentTexture(cliffTexture, index: 1)
renderEncoder.setFragmentTexture(snowTexture, index: 2)
renderEncoder.setFragmentTexture(grassTexture, index: 3)
```

在`Shaders.metal`中，为`VertexOut`添加两个新属性：

```swift
float height;
float2 uv;
```

在`vertex_main`的末尾，返回之前，设置这两个属性的值：

```swift
out.uv = xy;
out.height = height;
```

你将高度值从顶点函数发送到片段函数，以便将片段分配给高度计数器。

将纹理添加到`fragment_main`参数中：

```swift
texture2d<float> cliffTexture [[texture(1)]],
texture2d<float> snowTexture [[texture(2)]],
texture2d<float> grassTexture [[texture(3)]]
```

用以下内容替换片段函数：

```swift
constexpr sampler sample(filter::linear, address::repeat);
float tiling = 16.0;
float4 color;
if (in.height < -0.5) {
    color = grassTexture.sample(sample, in.uv * tiling);
} else if (in.height < 0.3) {
    color = cliffTexture.sample(sample, in.uv * tiling);
} else {
    color = snowTexture.sample(sample, in.uv * tiling);
}
return color;
```

你创建了一个可平铺纹理采样器，并根据高度读取相应的纹理。高度在 -1 到 1 之间，类似于`vertex_main`。然后你通过 16 告诉纹理——这是一个根据视觉效果的任意值。

编译并运行。点击线框渲染器查看你的带纹理的山脉。

你在低海拔处有草，在高海拔有雪峰。

![](img/655c9de9cdb851b3baacdbce4a1fae64_336_0.png)

当你缩放和旋转时，注意山脉似乎在波动。这是细分细节水平（tessellation level of detail）过度敏感。降低这种敏感的方法是更改渲染通道的细分分区模式（tessellation partition mode）。

在`Renderer.swift`的`buildRenderPipelineState()`中，将`descriptor.tessellationPartitionMode`的赋值更改为：

```swift
descriptor.tessellationPartitionMode = .pow2
```

编译并运行。当细分器将边缘因子向上舍入到 2 的幂时，现在补片（patches）之间的细分差异更大，但细分变化不会发生那么频繁，波动消失了。

![](img/655c9de9cdb851b3baacdbce4a1fae64_337_0.png)

## 按坡度着色

你之前的渲染中的雪线是不符合现实的。通过检查山的坡度，你可以在平坦区域显示雪地纹理，在坡度陡峭的地方显示悬崖纹理。

计算坡度的一种简单方法是在高度图上运行 **Sobel 滤波器**。Sobel 滤波器是一种查看相邻像素之间梯度的算法。

## Metal Performance Shaders

Metal Performance Shaders 框架包含了许多用于图像处理、矩阵乘法、机器学习和光线追踪的高度优化着色器。你将在第 21 章“Metal Performance Shaders”中阅读更多内容。

你在这里使用的着色器是`MPSImageSobel`，它接收源图像并输出过滤后的灰度图像。

> 注意：在本章节中，你将使用 Sobel 过滤后的图像，并根据坡度将这三个纹理应用到你的山脉。

在`Renderer.swift`的顶部，导入 Metal Performance Shaders 框架：

```swift
import MetalPerformanceShaders
```

## Metal by Tutorials

创建一个处理高度图的方法：

```swift
static func heightToSlope(source: MTLTexture) -> MTLTexture {
}
```

接下来，你需要修改高度图并返回一个新的纹理。要创建新纹理，你首先需要创建一个纹理描述符，可以在其中分配大小、像素格式以及用于纹理的 GPU。

在`heightToSlope(source:)`中添加以下内容：

```swift
let descriptor =
MTLTexture2DDescriptor(
pixelFormat: source.pixelFormat,
width: source.width,
height: source.height,
mipmapped: false,
```

（注：OCR 中的`npixelFormat`已修正为`pixelFormat`）。

# 第 12 章：环境

作者：Caroline Begbie

在本章中，你将为环境的渲染完成最后的收尾工作。

你将在场景外添加一个立方体，用于显示天空纹理。然后，这个天空纹理将照亮场景内的模型，使它们看起来像是属于该场景的。

请查看以下两个渲染效果的对比。

![](img/655c9de9cdb851b3baacdbce4a1fae64_342_0.png)

此对比展示了你如何使用相同的着色器代码，但通过更改天空图像来创建不同的光照环境。

## 开始

打开本章的启动项目。在大多数情况下，该项目与你在第 9 章“场景图”中创建的引擎相似。不过，有几处明显的变化：

- 你可以为`Model`初始化器添加一个片段器字符串名称，以便你为不同的道具测试不同的渲染样式。

- 赛车资产和`Textures`资源目录包含了金属属性（metallic）和环境遮蔽（ambient occlusion）贴图。

构建并运行项目，你将看到使用第 7 章“贴图与材质”中所描述的物理着色渲染的汽车。第 8 章“角色动画”和第 9 章“场景图”使用了相同的着色方法，并在片段着色器中偷偷使用了一个缩放因子来减弱阴影。

![](img/655c9de9cdb851b3baacdbce4a1fae64_343_0.png)

除了光照昏暗之外，渲染还存在一些明显的问题：

- 所有金属（例如金属轮毂）看起来都不发亮。纯金属会反射周围环境，但目前没有环境可以反射。

- 当你使用键盘绕汽车移动时，注意光线没有直接照射汽车的地方是黑色的。这是因为应用程序没有提供任何环境光。在章的后续部分，你将使用天空光作为全局环境光。

> 注意：如果你使用的是 macOS，请使用键盘键 WASD 移动，使用 QE 或左/右箭头键进行旋转。

## 天空盒

目前，天空是单一颜色，看起来极不真实。通过在场景周围添加一个 360° 的图像，你可以轻松地将动作置于沙漠或雪山的背景中。

为了实现这一点，你将创建一个环绕整个场景的天空盒立方体。

这个天空盒类与普通模型相同，但不是从外部查看它，而是相机位于立方体中心向外看。你将使用**立方体纹理**对立方体进行纹理处理，这提供了一种创建完整环境的廉价方法。

你可能认为立方体会在角处发生畸变，但你将会发现，立方体的每个片段将在实际上无限远的距离渲染，不会发生任何畸变。立方体贴映射比球面映射更容易创建，并且经过了硬件优化。

为天空盒类创建一个新的 Swift 文件`Skybox.swift`。记得将该文件同时添加到 iOS 和 macOS 目标中。该类持有立方体的几何结构，还包含了必要的流水线和天空纹理。

将默认代码替换为：

```swift
import MetalKit
class Skybox {
    let mesh: MTKMesh?
    var texture: MTLTexture
    let pipelineState: MTLRenderPipelineState
    let depthStencilState: MTLDepthStencilState?

    init(textureName: String?) {
    }
}
```

你创建了天空盒类以及一些属性：

- mesh: 一个你将使用 Model I/O 原型创建的立方体。

- texture: 在初始化器中给出名称的立方体纹理。

- pipelineState: 天空盒需要简单的顶点和片段函数，因此它需要它自己的流水线。

- depthStencilState: 天空盒的每个像素将放置在归一化裁剪空间的最边缘。渲染器当前的深度模板状态仅在添加时有效。
