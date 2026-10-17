
接下来，在`init(metalView)`之前添加这段代码：

```
lazy var window: MTKMesh = {
do {
    let primitive = self.loadModel(name: "plane")
    let model = try MTKMesh(mesh: primitive, device: device)
    windowTexture = loadTexture(imageName: "windowColor")
    return model
} catch {
    fatalError()
}()
var windowTransform = Transform()
```

这段代码与地形和树的代码相同，不过回顾一下：你使用`mesh`和`windowColor`纹理定义了一个新的窗户模型，然后为该模型创建一个新的变换。在`init(metalView)`的末尾添加这段代码：

```
windowTransform.scale = [2, 2, 2]
windowTransform.position = [0, 3, 4]
windowTransform.rotation = [-Float.pi / 2, 0, 0]
```

这段代码同样与地形树的变换相似：首先，设置大小为 2；然后将窗户位置移动离眼睛更近（树在 6 的位置）；最后，在 x 轴上旋转窗户 90 度。

![](img/655c9de9cdb851b3baacdbce4a1fae64_298_0.png) 圆周是 $2\pi$，这意味着 90° 是 $\pi / 2$。

在`buildPipelineState()`内部的末尾添加这几行：

```
let windowFragmentFunction =
library.makeFunction(name: "fragment_window")
descriptor.fragmentFunction = windowFragmentFunction
descriptor.vertexFunction = lightVertexFunction
try
.makePipelineState(descriptor)
```

在这里，你使用该描述符构建管道状态。稍后我们会编写`fragment_window()`着色器。

在`draw()`的末尾，在`renderEncoder.endEncoding()`之前添加这段代码：

```
// render window
renderEncoder.setPipelineState(windowPipelineState)
modelViewProjectionMatrix = camera.projectionMatrix *
camera.viewMatrix * windowTransform.matrix
renderEncoder.setVertexBuffer(modelViewProjectionMatrix,
    length: MemoryLayout<floatx4>.stride,
    index: 1)
renderEncoder.setVertexBuffer(window.vertexBuffers[0].buffer,
    offset: 0, index: 0)
renderEncoder.setFragmentTexture(windowTexture, index: 0)
draw(renderEncoder: renderEncoder, model: window)
```

这段代码绘制窗户，你现在应该熟悉它了。

在`Shaders.metal`中，添加新函数：

```
fragment float4
    fragment_window(VertexOut vertex_in [[stage_in]],
    texture2d<float> texture [[texture(0)]]) {
    constexpr sampler s(filter:linear);
    float4 color = texture.sample(s, vertex_in.uv);
    return color;
}
```

这个函数与之前的相似：你创建一个默认采样器，采样纹理获取像素颜色，最后返回新颜色。

再次运行 Playground。

![](img/655c9de9cdb851b3baacdbce4a1fae64_300_0.png) 这是一个暗淡、不透明的窗户！

你将通过混合来修复它。处理混合有两种方式：可编程方式和固定函数方式。在本章中，你将学习固定函数混合。

在`Renderer.swift`中，在`buildPipelineState()`的末尾，在以下之前：

```
windowPipelineState =
try device.makeRenderPipelineState(descriptor: descriptor)
```

添加这段代码：

```
// 1
guard let attachment = descriptor.colorAttachments[0] else
{ return }
// 2
attachment.isBlendingEnabled = true
// 3
attachment.rgbBlendOperation = .add
// 4
attachment.sourceRGBGBlendFactor = .sourceAlpha
// 5
attachment.destinationRGBGBlendFactor = .oneMinusSourceAlpha
```

# 第 10 章：片元后处理

通过这段代码，你：

- 1. 从渲染流水线描述符中获取第一个颜色附件（color attachment）。颜色附件是一个颜色渲染目标，它指定了与渲染流水线相关的颜色配置和颜色操作。渲染目标持有渲染输出的可绘制纹理。

- 2. 在附件上启用混合（blending）。

- 3. 指定用于颜色的混合操作类型（blend type operation）。混合操作决定了源片元（source fragment）如何与颜色附件中的目标值结合，以确定要写入的像素值。

- 4. 指定源颜色使用的混合因子（blend factor）。混合因子决定了颜色对混合颜色的贡献程度。如果没有指定，该值为默认 1 (.one)。

- 5. 指定目标颜色使用的混合因子。如果没有指定，该值默认为 0 (.zero)。

> 注意：除了`sourceAlpha`和`oneMinusSourceAlpha`之外，还有几个混合因子可用。要查看完整的选项列表，请参阅 Apple 关于混合因子的官方页面：https://developer.apple.com/documentation/metal/mtlblendfactor。

你已经准备好观察混合效果了。不过，像之前一样，你要为混合设置一个切换键。

在`Renderer.swift`中，在`Renderer`顶部添加此属性：

```
var blendingEnabled = false
```

在`draw(in:)`中，添加此渲染窗口的绘制调用：

```
renderEncoder.setFragmentBytes(&blendingEnabled, length: MemoryLayout<Bool>.size, index: 0)
```

在`MetalView.swift`中，为`keyDown(with:)`中的`KeyCode`枚举添加 B 键的新 case：

```
case b = 0xB
```

然后，在 switch 语句中检查此 case，并切换`blendingEnabled`的状态，就像你之前处理透明度的那样：

```
case .b:
    renderer.blendingEnabled = !renderer.blendingEnabled
```

在`Shaders.metal`中，将`fragment_window`的定义更改为：

```
fragment float4
fragment_window(VertexOut) vertex_in [[stage_in]],
constant bool &blendingEnabled [[buffer(0)]],
texture2d<float> texture [[texture(0)]]
```

现在，在`fragment_window`的`return color`之前添加这段代码：

```
if (blendingEnabled) {
    color.a = 0.5;
}
```

如果启用了混合，你将将当前像素的 alpha 分量设置为 0.5（半透明）。再次运行 playground。点击渲染后的图像以确保按键被捕获。然后，按几次 B 键来观察混合的开启和关闭：

![](img/655c9de9cdb851b3baacdbce4a1fae64_302_0.png)

增加第二个窗口来增加更多趣味怎么样？

你将复用窗口的网格（mesh）和纹理，因此在`Renderer.swift`中，在`init(metalView)`之前添加这段代码：

```
var window2Transform = Transform()
```

在`init(metalView)`结束处，通过添加以下代码设置第二个窗口的大小、位置和旋转：

```
window2Transform.scale = [3, 2, 2]
window2Transform.position = [0, 3, 5]
window2Transform.rotation = [-Float.pi / 2, 0, 0]
```

在`draw(in:)`中，在保持流水线状态的同时，在`renderEncoder.end(in)`之前添加这段代码，向 GPU 发送关于第二个窗口的信息：

```
modelViewProjectionMatrix = camera.projectionMatrix *
camera.viewMatrix * window2Transform.matrix
renderEncoder.setVertexBytes(modelViewProjectionMatrix,
length: MemoryLayout.float4x4.stride,
index: 1)
draw(renderEncoder: renderEncoder, model: window)
```

这段代码与你用于第一个窗口的代码几乎相同，区别在于第二个窗口的变换矩阵是不同的。

再次运行 playground 并开启混合。

![](img/655c9de9cdb851b3baacdbce4a1fae64_303_0.png)

哇！发生了什么？看起来就像是透过一个单一窗口而不是两个窗口。你完全确定窗口没有重叠，因为其中一个位于 Z = 4，另一个位于 Z = 5。那么发生了什么呢？

> 注意：启用混合时，你应该始终注意按照从后到前的顺序渲染对象。然而，你目前是在渲染第二个窗口之前渲染了第一个窗口，但第一个窗口在第二个窗口的前面。

在这种情况下，树的流水线状态没有启用混合，因此重要的是按顺序渲染这两个窗口。你有两个选择：

- 在`draw(in:)`中交换两个窗口的渲染块：

- 或者将第二个窗口移动到第一个窗口前面。

方案一是简单的剪切粘贴。方案二也不太难，在`Renderer.Swift`的`init(metaView)`中，按如下更改第二个窗口的变换：

```
window2Transform.scale = [2, 2, 2]
window2Transform.position = [0, 2, 2]
```

再次运行 playground 并开启混合。

![](img/655c9de9cdb851b3baacdbce4a1fae64_304_0.png)

在这种情况下，树的流水线状态没有启用混合，因此重要的是按顺序渲染这两个窗口。你有两个选择：

- 在`draw(in:)`中交换两个窗口的渲染块：

- 或者将第二个窗口移动到第一个窗口前面。

方案一是简单的剪切粘贴。方案二也不太难，在`Renderer.Swift`的`init(metaView)`中，按如下更改第二个窗口的变换：

```
window2Transform.scale = [2, 2, 2]
window2Transform.position = [0, 2, 2]
```

## 抗锯齿

渲染的模型通常会有锯齿。这被称为锯齿（aliasing）。为了解决这个问题，我们使用多采样抗锯齿（MSAA）。MSAA 通过对每个像素进行多次采样并取平均来确定最终颜色。

在 Metal 中实现 MSAA，你需要：

1. 增加渲染描述符中的采样数。

2. 配置流水线状态使用相同的采样数。

3. 使用解析纹理（resolve texture）将多采样纹理转换为采样纹理。

首先，让我们更新渲染通道描述符。在`Renderer.swift`中，找到创建`renderPassDescriptor`的代码并更新`sampleCount`：

```
let renderPassDescriptor = MTLRenderPassDescriptor()
renderPassDescriptor.colorAttachments[0].sampleCount = 4
```

接下来，我们需要更新流水线状态。在`Renderer.swift`中，找到创建`pipelineDescriptor`的代码并更新`sampleCount`：

```
let pipelineDescriptor = MTLRenderPipelineDescriptor()
pipelineDescriptor.sampleCount = 4
```

等等，我们需要确保流水线状态的采样数与渲染通道描述符相同。如果不相同，应用程序将崩溃。

最后，我们需要使用解析纹理。在`Renderer.swift`中，找到创建颜色理的代码并更新它以包含解析纹理：

```
let colorTexture = device.makeTexture(pixelFormat: .rgba8Unorm,
                                  width: width,
                                  height: height,
                                  mipmappedLevel: 1,
                                  options: [])

let resolveTexture = device.makeTexture(pixelFormat: .rgba8Unorm,
                                        width: width,
                                        height: height,
                                        mipmappedLevel: 1,
                                        options: [])

renderPassDescriptor.colorAttachments[0].resolveTexture = resolveTexture
```

现在，更新绘制调用以使用解析纹理：

```swift
let encoder = commandBuffer.makeRenderCommandEncoder(descriptor: renderPassDescriptor)
// ... draw calls ...
encoder.end()
```

有了这些更改，锯齿边缘应该会平滑很多。再次运行 playground 查看差异。

在`switch`语句中添加该检查，相应切换`antialiasingEnabled`的状态。

```
case :a:
  renderer.antialiasingEnabled = !renderer.antialiasingEnabled
```

再次运行 playground 并直接缩放到树。现在点击渲染后的图像，这样按键就会被捕获在树中。按几次 A 键，观察抗锯齿的开启和关闭。如果你使用的是 Retina 屏幕，这种效果可能很难看到。观察透明度关闭时叶子上的对角线。

![](img/655c9de9cdb851b3baacdbce4a1fae64_307_0.png)

## 雾化 (Fog)

如果你在这一章中还没玩够的话，为什么不给场景添加一些雾，让它变得更有趣呢？

雾化在渲染中非常有用，原因有两个。首先，它作为渲染内容的远端边界符。渲染器可以忽略消失在雾中的物体，因为它们已经不再可见。雾化有助于避免从远处突然出现在场景中的物体产生“闪现效应”（popping-effect），让它们进入场景的过程更加平滑。

和之前一样，你为雾化添加一个切换键。

在`Renderer.swift`中，类顶部添加此属性：

```
var fogEnabled = false
```

如果你希望所有物体都处于雾中，你需要在片段着色器中添加雾化。

在`draw(in:)`中，在第一次绘制调用之前添加以下代码：

```
renderEncoder.setFragmentBytes(&fogEnabled,
length: MemoryLayout<Bool>.size,
index: 1
```

这使用`index: 1`将`fogEnabled`布尔变量发送到 GPU。因为没有资源使用该索引，它将留在游戏表的索引处，供后续所有的绘制调用使用。

在`MetalView.swift`中，在`keyDown(with:)`中添加一个 KeyCode case：

```
case f = 0x3
```

在`switch`语句中，检查 F 键是否按下，以切换`fogEnabled`的状态。
