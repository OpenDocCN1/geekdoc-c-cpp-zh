
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`。

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

---

```
case .f:
renderer.fogEnabled = !renderer.fogEnabled
```

最后，在`Shaders.metal`中，在所有三个片段着色器的定义中添加以下内容：

```
constant bool fogEnabled [[buffer(1)]]
```

然后，在`Shaders.metal`中，任何片段函数之前创建一个新函数：

```
float4 fog(float4 position, float4 color) {
// 1
float distance = position.z / position.w;
// 2
float density = 0.2;
float fog = 1.0 - clamp(exp(-density * distance), 0.0, 1.0);
// 3
float4 fogColor = float4(1.0);
color = mix(color, fogColor, fog);
return color;
}
```

通过这段代码，你：

- 1. 计算片段位置的深度。
- 2. 定义了一个下一步雾化将使用的分布函数。它是雾密度与上一步计算出的深度之间经过限制（在 0 到 1 之间）的乘的倒数。
- 3. 使用上一步定义的分布函数将当前颜色与雾色（你刻意将其设置为白色）混合。

现在，在所有三个片段着色器的`return color`之前，添加以下代码：

```
if (fogEnabled) {
  color = fog(vertex_in.position, color);
}
```

这段代码调用了`fog`函数。再次运行 playground，并用 F 键切换雾化：

![](img/655c9de9cdb851b3baacdbce4a1fae64_309_0.png)

如你所见，整个场景现在都在雾中。你离树越近，雾就越稀。地面也是如此。

当你向前移动时，你会看到更多细节。离树近一点，你会更清楚地看到树：

![](img/655c9de9cdb851b3baacdbce4a1fae64_310_0.png)

> 注意：注意奶油色的天空不受雾化的影响。这是因为奶油色是来自`MTKView`而不是渲染出来的。稍后你将创建一个带纹理的天空。

## 挑战 (Challenge)

我希望你玩各种片段处理技术玩得很开心。我知道我很开心！

如果你准备好接受几个挑战：

- 1. 将雾化密度设置为较低值，然后设置为较高值，看看看起来有什么不同。
- 2. 为两个窗口使用不同的纹理颜色，观察不同颜色是如何混合的。
- 3. 修改一个或两个颜色的 alpha 值，观察这种变化如何影响混合后的颜色。

# 接下来去哪里？

在这一章中，你只研究了固定函数混合和抗锯齿。通过使用`[[color]]`属性（该属性作为标识颜色附件，作为片段函数的参数），可以实现**可编程混合**（programmable blending）。

同样，通过可编程的采样位置也可以实现**可编程抗锯齿**（programmable antialiasing），这允许你为不同的渲染通过设置自定义采样位置，而固定函数抗锯齿的相同采样位置适用于所有渲染通过。如需进一步阅读，可以查阅苹果文档上的`Programmable Sample Positions`页面：https://developer.apple.com/documentation/metal/using_programmable_sample_positions。

# 第 11 章：曲面化 (Tessellation) 与地形 (Terrains)

到目前为止，你一直在使用法线贴。在本章中，你将使用灰度贴图创建详细的地形。

通过曲面化，你可以：

- 向 GPU 发送更少的数据。因为内存中不存储曲面化的顶点，它更高效。
- 通过曲线补丁（patches）让多边形物体看起来不平滑。
- 在不使用法线贴的情况下偏移顶点。
- 根据距离决定细节水平。物体离相机越近，包含的顶点越多。

## 曲面化 (Tessellation)

你不再向 GPU 顶点，而是发送补丁。这些补丁由控制点组成——三角形需要三个，矩形需要四个。曲面化器可以将每个矩形转换为特定数量的三角形：在最近的 iMac 上可以是 4096 个三角形，在 iPhone 上可以是 256 个。

> 注意：曲面化适用于 2012 年之后的所有 Mac 以及 iOS 10（包括 iPhone 6 及更新机型）。然而，它不支持 iOS 模拟器。

## 初始化项目 (Starter Project)

在创建曲面化地形之前，你将对单个四点补丁进行曲面化。打开并运行本章的初始化项目。该项目的代码是渲染六个顶点以创建矩形的最小代码。

![](img/655c9de9cdb851b3baacdbce4a1fae64_314_0.png)

你的任务是将这个矩形转换为由许多顶点组成的曲面化补丁。与其向 GPU 发送六个顶点，不如发送补丁四个角的位置。你赋予 GPU 边缘因子（edge factors）和内部因子（inside factors），告诉曲面化器创建多少顶点。为了看到曲面化器添加的顶点，我们将以线条模式渲染。

为了转换矩形，你需要在 GPU 端执行以下操作：

| 设置补丁数据和缓冲区 |
| 设置边缘和内部因子 |
| 设置计算管道状态 |
| 绘制补丁 |

观察曲面化器创建了多少顶点。

![](img/655c9de9cdb851b3baacdbce4a1fae64_313_0.png)

![](img/655c9de9cdb851b3baacdbce4a1fae64_313_1.png)

## 细分片 (Tessellation patches)

一个片由特定数量的控制点组成，通常有：

- 双线性 (bilinear)：四个控制点，每个角一个
- 二次二次 (biquadratic)：九个控制点
- 三次立方 (bicubic)：十六个控制点

![](img/655c9de9cdb851b3baacdbce4a1fae64_315_0.png)

控制点构成了一个由样条组成的围格。样条是由控制点组成的参数曲线。

有各种算法来插值这些控制点，但在这里，A、B 和 C 是控制点。当点 P 从 A 移动到 B 时，点 Q 从 B 移动到 C。P 和 Q 的中间点描述了蓝色的曲线。

![](img/655c9de9cdb851b3baacdbce4a1fae64_315_1.png)

为了创建弯曲片表面，顶点函数插值顶点以遵循此参数曲线。

## 细分因子 (Tessellation factors)

对于每个片，你需要指定内部边缘因子和外部边缘因子。下图中的四点片显示了每个边的不同边缘因子——指定为 [2, 4, 8, 16]——以及两个不同的内部因子——分别指定为 [8, 16]，对应水平和垂直。

![](img/655c9de9cdb851b3baacdbce4a1fae64_316_0.png)

边缘因子指定了边缘将拆分成多少段。边缘因子为 2 的表示沿边缘有两个段。对于内部因子，查看水平和垂直中心线。在例例中，水平中心有八段，垂直中心有十六段。

虽然只有四个点（用红色显示）发送到了 GPU，但硬件细分器创建了得多的顶点。然而，在平面上创建更多顶点并不会让渲染器变得有趣。

稍后，你会发现如何在顶点函数中移动这些顶点以创建一个凹凸的转弯。但首先，你将发现如何细分单个片。

在`Renderer.swift`中，在`Renderer`中添加以下内容：

```
let patches = (horizontal: 1, vertical: 1)
var patchCount: Int {
  return patches.horizontal * patches.vertical
}
```

# Metal 教程

# 第 11 章：细分与地形 (Tessellation & Terrains)

这为你将要创建的片数量创建了一个常量，在这种情况下，`patchCount`是一个返回片总数的便利属性。

现在添加：

```
var edgeFactors: [Float] = [4]
var insideFactors: [Float] = [4]
```

在这里，你正在将边缘因子和内部因子设置为`Float`数组属性。这些变量表示沿每条边有四段，中间有四段。

你可以通过将它们添加到数组中为不同的边指定不同的因子。对于每个片，GPU 会处理这些边缘因子并为每个缓冲区放置要细分的数量。

创建一个懒性加载属性来提供一个正确长度的缓冲区：

```
lazy var tessellationFactorsBuffer: MTLBuffer = {
// 1
let count = patchCount * (4 + 2)
// 2
let size = count * MemoryLayout<Float>.size / 2
return Renderer.device.makeBuffer(length: size, options: .storageModePrivate)
}
```

- 1. 这是片的数量乘以四个边缘因子和两个内部因子。
- 2. 这计算了缓冲区的大小。在细分内核中，你将用一个由半精度浮点数组成的特殊类型填充缓冲区。该类型目前没有 Swift 中的等效类型。

现在是设置片数据了。

## 设置片数据

与其创建一个六个顶点的数组，不如创建一个带有四个控制点的四点片。

目前`Data.swift`持有一个包含顶点的`vertexBuffer`；你将用一个包含控制点的缓冲区替换它。

在`Renderer`中，添加此属性：

```
var controlPointsBuffer: MTLBuffer?
```

在`init(metal)`的末尾，用控制点填充缓冲区：

```
let controlPoints = createControlPoints(patches: patches,
    size: (2, 2))
controlPointsBuffer =
    Renderer.makeBuffer(bytes: controlPoints,
    length: MemoryLayout<float3>.stride)
```

`Data.swift`中的`createControlPoints(patches:size:)`该函数接受片的数量和大小。它返回一个控制点数组。你正在创建一个在 [-1, 0, 0] 有一个角，在 [1, 0, -1] 有对角角的片。这是一个平面，将片旋转 90 度。

## 设置渲染流水线

你可以通过更改流水线状态来配置细分器。到目前为止一直在处理顶点，现在你将修改 vertex descriptor 以处理片。

在`buildPipelineState()`中设置`vertexDescriptor`时，添加此内容：

```
vertexDescriptor.layouts[0].stepFunction = .perPatch
```

使用旧的`.perVertex`。现在你已转向处理片，需要为每个控制点获取新属性。

## 内核函数 (Kernel functions)

你习惯为渲染设置流水线状态，但 compute 允许你在不同线程上执行不同的任务。

![](img/655c9de9cdb851b3baacdbce4a1fae64_318_0.png)

此部分创建的内核函数非常简单。在第 11 章中，将深入研究。顶点和片段着色器在所有顶点上运行相同的任务，因此对每个线程没有细粒度的控制。你需要设置一个指向细分内核函数的计算流水线状态。

向`Renderer`添加此新方法：

```
static func buildComputePipelineState()
  -> MTLComputePipelineState {
  guard let kernelFunction = 
    Renderer.makeFunction(name: "tessellation_main")
  else {
    fatalError("Tessellation shader function not found")
  }
  return try! Renderer.device.makeComputePipelineState(
    function: kernelFunction)
}
```

这创建了一个期望 kernel 类型而不是 vertex 或 fragment 类型的计算流水线状态。通过内核函数，你可以在渲染之前处理缓冲区。

向`Renderer`添加新属性：

```
var tessellationPipelineState: MTLComputePipelineState
```

在`init(view:)`中，`super.init()`之前添加此内容：

```
tessellationPipelineState = Renderer.buildComputePipelineState()
```

在这里为计算流水线实例化流水线状态。

## 计算通过 (Compute pass)

你设置了一个计算流水线状态和一个包含片数据的`MTLBuffer`。你还创建了一个空缓冲区，细分内核将用边缘和内部因子填充。接下来你需要创建一个计算编码器。此编码器与渲染编码器类似，你向编码器添加命令然后将其发送到 GPU。

打开`Shaders.metal`。目前此文件包含简单的顶点和片段函数。你将在这里添加细分内核。

```
kernel void
    tessellation_main(constant float* edge_factors [[buffer(0)]],
        constant float* inside_factors [[buffer(1)]],
        device MTLQuadFactorsHalf*
            factors [[buffer(2)]],
        uint pid [[thread_position_in_grid]]) {
```

`kernel`指定着色器类型。该函数在所有线程（即片）上操作，并接收你发送的三要素：边缘因子、内部因子以及你在这个函数中填充的细分缓冲区。

第四个参数是片 ID 及其在网格中的线程位置。细分缓冲区由每个片的边缘和内部因子组成；你使用片索引进入此数组。

在内核函数内部，添加以下内容：

```
factors[pid].edgeTessellationFactor[0] = edge_factors[0];
factors[pid].edgeTessellationFactor[1] = edge_factors[0];
factors[pid].edgeTessellationFactor[2] = edge_factors[0];
factors[pid].edgeTessellationFactor[3] = edge_factors[0];
```

```
factors[pid].insideTessellationFactor[0] = inside_factors[0];
factors[pid].insideTessellationFactor[1] = inside_factors[0];
```

这用你发送的因子填充细分缓冲区。你发送的边缘和内部因子数组各发送了一个值，因此你将此值放入所有因子。

填充缓冲区对于内核来说是件易事。然而，随着你获得更多的片以及细分这些片的复杂性，你将理解为什么将数据发送到 GPU 进行并行处理是一个很有用的步骤。

完成通过后，渲染通过将接管。

## 渲染通过 (Render pass)

回到`Renderer.swift`，在渲染之前，你需要告诉渲染编码器关于你在计算通过期间更新的细分缓冲区。

在`draw(in:)`中，找到 // draw 命令。紧随之后添加此内容：

```
renderEncoder.setTessellationFactorBuffer(
tessellationFactorsBuffer,
```

offset: 0, instanceStride: 0)

后细分顶点函数（post-tessellation vertex function）会读取你在内核函数中设置的缓冲区。

你不需要从顶点缓冲区绘制三角形，而是需要从控制点缓冲区绘制补丁控制点。

```
renderEncoder.setVertexBuffer(vertexBuffer, offset: 0, index: 0)
```

使用：

```
renderEncoder.setVertexBuffer(controlPointsBuffer, offset: 0, index: 0) command 并此内容：
```

替换`drawPrimitives`调用：

```
renderEncoder.drawPatches(numberOfPatchControlPoints: 4, patchStart: 0, patchCount: patchCount, patchIndexBuffer: nil, patchIndexOffset: 0, instanceCount: 1, baseInstance: 0)
```

该渲染命令告诉 GPU 它将绘制一个具有四个控制点的补丁（patch）。

## 后细分顶点函数

再次打开`Shaders.metal`。在细分器完成创建顶点的工作后，会调用顶点函数，它将对这些新顶点中的每一个进行操作。在顶点函数中，你将告诉每个顶点在渲染的四边形（quad）中的位置应该是什么。

将`VertexIn`重命名为`ControlPoint`。`position`的定义保持。

由于你使用了顶点描述符来描述输入的控制点数据，你可以使用`[[stage_in]]`属性。

顶点函数将检查当前管道状态的顶点描述符，发现数据在缓冲区 0 中，并使用顶点描述符布局来读取数据。

将顶点函数`vertex_main`替换为：
