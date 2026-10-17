
# Metal 教程

## 第 6 章：纹理

### 顶点属性与片元函数

| Vertex Attributes (顶点属性) | Vertex Attributes | | Library 0x60000176c00... | |
|---|---|---|---|---|
| Vertex_main | Fragment Function (片元函数) | | | |

- `lowpoly-house-color.png`: 纹理 D 1024 x 1024 RGBAUnorm baseColor 读取 (Read)
- `Fragment Bytes` (片元字节): Buffer (2) 384 bytes lights 读取 (Read)
- `Fragment Function` (片元函数): Buffer (3) 32 bytes fragmentUniforms 读取 (Read)
- `fragment_main`: 片元函数库 0x60000176c00... 读取 (Read)

双击每个顶点资源以查看缓冲区的内容：

- `MDL_OBJ-Indices`: 顶点索引。
- `Buffer 0x000000`: 顶点位置、法线和纹理坐标数据，与你的 `VertexIn` 结构体的属性匹配。
- `Vertex Bytes`: 均匀矩阵（uniform matrices）。
- `Vertex Attributes`: 来自 `VertexIn` 的输入数据，以及来自顶点函数的 `VertexOut` 数据。
- `vertex_main`: 顶点函数。当你有多个顶点函数时，确保你设置了正确的流水线状态是非常有用的。

查看片元资源：

- `lowpoly-house-color.png`: 纹理持有光照和第 0 槽。
- `Fragment Bytes` (片元字节): 你有两个这样的资源：一个持有光照，另一个持有片元均匀变量光照数量。
- `fragment_main`: 片元函数。

![](img/655c9de9cdb851b3baacdbce4a1fae64_167_0.png)

- `CAMetalLayer Drawable`: 颜色附件 0 中的编码结果。在这种情况下，这是视图当前的 drawable。稍后，你将使用多个颜色附件。
- `MTKView Depth`: 深度缓冲区。黑色表示较近，白色表示较远。光栅化器使用深度图。

你可以从此列表中看到 GPU 正以 BGRABNorm 格式持有纹理。

如果你反转上一节的纹理加载选项并注释掉 `.sRGB: false`，你就能看到纹理是 BGRABNorm_sRGB。（在继续之前请确保恢复 `.sRGB: false`。）

如果你一直不确定应用中发生了什么，捕获 GPU 帧将为你提供提示，因为你可以检查每一个编码器命令。在本书中使用它来检查 GPU 上正在发生的情况是一个好主意。第 23 章“调试与分析”将提供关于 GPU 帧捕获工具的更深入介绍。

### 采样器 (Samplers)

现在当你对纹理进行采样时，使用的是默认采样器。通过更改采样器参数，你可以决定应用如何读取纹素元素（texels）。你将为场景添加一个地面平面，以观察如何控制地面纹理的外观。

在 `Renderer.swift` 的 `init(metalView:)` 中，找到你添加房子的地方。之后：

```swift
let ground = Model(name: "plane.obj")
ground.scale = [40, 40, 40]
models.append(ground)
```

这添加了一个平面并将其放大得非常大。

地面纹理将拉伸以适应。构建并运行：

![](img/655c9de9cdb851b3baacdbce4a1fae64_169_0.png)

地面纹理将拉伸以适应。你可以从此列表中看到 GPU 正以 BGRABNorm 格式持有纹理。

如果你反转上一节的纹理加载选项并注释掉 `.sRGB: false`，你就能看到纹理是 BGRABNorm_sRGB。（在继续之前请确保恢复 `.sRGB: false`。）

如果你一直不确定应用中发生了什么，捕获 GPU 帧将为你提供提示，因为你可以检查每一个编码器命令。在本书中使用它来检查 GPU 上正在发生的情况是一个好主意。第 23 章“调试与分析”将提供关于 GPU 帧捕获工具的更深入介绍。

现在当你对纹理进行采样时，使用的是默认采样器。通过更改采样器参数，你可以决定应用如何读取纹素元素（texels）。你将为场景添加一个地面平面，以观察如何控制地面纹理的外观。

在 `Renderer.swift` 的 `init(metalView:)` 中，找到你添加房子的地方。之后：

```swift
let ground = Model(name: "plane.obj")
ground.scale = [40, 40, 40]
models.append(ground)
```

这添加了一个平面并将其放大得非常大。

地面纹理将拉伸以适应。构建并运行：

![](img/655c9de9cdb851b3baacdbce4a1fae64_169_0.png)

地面纹理将拉伸以适应。你可以从此列表中看到 GPU 正以 BGRABNorm 格式持有纹理。

在 `draw(in:)` 中，在循环内部，处理模型之前：

```swift
renderEncoder.setFragmentBytes(&fragmentUniforms,
length: MemoryLayout<FragmentUniforms>.stride,
index: Int(BufferIndexFragmentUniforms.rawValue))
```

在 `Shaders.metal` 中，你将 uniform 变量作为参数接收到片元函数：

```swift
float3 baseColor = baseColorTexture.sample(textureSampler,
in.uv * fragmentUniforms.tiling);
```

构建并运行。你的地面和房子现在都正确平铺了！

![](img/655c9de9cdb851b3baacdbce4a1fae64_172_0.png)

地面看起来很棒！房子……不太。shader 也平铺了纹理。为了解决这个问题，你将在模型上创建一个 `tiling` 属性并将其发送到片元函数。

在 `Renderer.swift` 中，在属性：

```swift
var tiling: UInt32 = 1
```

在 `Renderer.swift` 中，在处理模型之前：

```swift
ground.tiling = 16
```

对 `fragmentUniforms` 的赋值目前发生在循环中，所以移动：

```swift
renderEncoder.setFragmentBytes(&fragmentUniforms,
length: MemoryLayout<FragmentUniforms>.stride,
index: Int(BufferIndexFragmentUniforms.rawValue))
```

在 `Shaders.metal` 中，你将 `tiling` 变量作为参数接收到 `fragment_main()`，所以将常量平铺值替换为变量：

在 `Common.h` 的 `struct FragmentUniforms` 中添加此：

```h
uint tiling;
```

### Metal API 采样器状态

在 shader 中创建采样器不是唯一的选择。相反，你将在 Metal API 中创建一个 `MTLSamplerState` 并由模型持有它。然后，你将采样器状态发送到片元函数。

在 `Model.swift` 中，为 `Model` 添加新属性：

```swift
let samplerState: MTLSamplerState?
```

在你初始化了 `samplerState` 后，编译错误将消失。

现在添加以下方法：

```swift
private static func buildSamplerState() -> MTLSamplerState {
let descriptor = MTLSamplerDescriptor()
descriptor.sAddressMode = .repeat
descriptor.tAddressMode = .repeat
let samplerState = 
Renderer.device.makeSamplerState(descriptor: descriptor)
return samplerState
}
```

这创建了采样器状态（sampler state），你将采样器设置为重复模式，就像你在片段器函数中做的那样。

在 `init(name:)` 中，在 `super.init()` 之前调用你的新方法：

```
samplerState = Model.buildSamplerState()
```

编译错误现在应该消失了。

在 `Renderer.swift` 的 `draw(in:)` 中，找到处理模型的循环。在循环内部，在你分配 `tiling` 变量之后，添加以下代码：

```
renderEncoder.setFragmentsSamplerState(model.samplerState, index: 0)
```

你现在正在通过参数表中的索引 0 采样器将采样器状态发送到片段器函数。

在 `Shaders.metal` 中，在 `fragment_main` 的 `texture2d<float> baseColorTexture [[texture(BaseColorTexture)]]` 之后添加一个新参数：

```
sampler textureSampler [[sampler(0)]]
```

现在你已经在函数中接收采样器了，请移除：

```
constexpr sampler textureSampler(filter::linear, address::repeat);
```

编译并运行，输出应该与你在片段器函数内部创建采样器时完全相同。主要的优势是，现在更容易为每个模型设置采样器状态的独立参数。

大幅缩小场景视图，在你缩放时，你会注意到房顶上出现了摩波纹（moiré pattern）。

摩波纹是在对纹理进行欠采样时发生的一种渲染伪影。

![](img/655c9de9cdb851b3baacdbce4a1fae64_173_0.png)

当你旋转场景时，平线处的草地上也有干扰性的噪声，几乎就像在闪烁。你可以通过使用名为 mipmaps（多映射）的调整尺寸纹理进行正确采样来解决这些伪影问题。

### Mipmaps（多映射）

查看房顶纹理的尺寸以及它在屏幕上的显示效果：

![](img/655c9de9cdb851b3baacdbce4a1fae64_174_0.png)

这种模式出现是因为采样的纹素（texels）多于你拥有的像素（pixels）。理想情况是纹素和像素的数量相等，这意味着物体越远，需要的纹理就越小。解决方案是使用 mipmaps，它会让 GPU 以合适的尺寸对纹理进行采样。

> MIP 代表 multum in parvo —— 一个拉丁语短语，意为“小中见大”。

Mipmaps 是每一层级都按 2 的幂次方缩小尺寸的纹理图，一直缩小到 1 像素大小。如果你有一个 64 x 64 像素的纹理，那么一个完整的 mipmap 集合将包含：

- Level 0: 64 x 64, 1: 32 x 32, 2: 16 x 16, 3: 8 x 8, 4: 4 x 4, 5: 2 x 2, 6: 1 x 1。

![](img/655c9de9cdb851b3baacdbce4a1fae64_174_1.png)

在接下来的图中，顶部的棋盘纹理没有 mipmaps；但在底部的图中，每个片段都从相应的 MIP 级进行采样。随着方格变远，噪声少了很多，图像也更清晰。在平线处，你可以看到纯灰色的 mipmaps。

![](img/655c9de9cdb851b3baacdbce4a1fae64_175_0.png)

你可以在第一次加载纹理时轻松且自动地生成这些 mipmaps。

在 `Texturable.swift` 中，更改纹理加载选项：

```
let mipFilterLoaderOptions: [MTKTextureLoaderOption: Any] = [
 .origin: MTKTextureLoader.Origin.bottomLeft,
 .SRGB: false,
 .generateMipmaps: NSNumber(booleanLiteral: true)
]
```

这将创建一直到最小像素的 mipmaps。

还有一件事需要更改：采样器状态。在 `Model.swift` 的 `buildSamplerState()` 中，在创建采样器状态之前添加如下：

```
descriptor.mipFilter = .linear
```

`mipFilter` 的默认值是 `.notMipmapped`；然而，如果你提供了 `.linear` 或 `.nearest`，GPU 将采样正确的 mipmap。

编译并运行。当你缩放和旋转时，建筑和地面上的噪声应该消失了。

使用 GPU 帧捕（Frame Capture）工具，你可以检查 mipmaps。双击纹理，在左下角可以选择 MIP 级别。这是房顶纹理的 MIP 级别 4：

![](img/655c9de9cdb851b3baacdbce4a1fae64_176_0.png)

Mipmap Level 4 ⇩ 400% +

你渲染的房子在背景中看起来有些模糊。这是由于各向异性（anisotropy）。各向异性表面根据你观察的角度发生变化，而 GPU 对倾斜角度投影的纹理进行采样导致了锯齿。

在 `Model.swift` 的 `buildSamplerState()` 中，在创建采样器状态之前添加：

```
descriptor.maxAnisotropy = 8
```

Metal 现在将根据采样器状态进行 8 次采样。

3. 将 Models ► LowPolyHouse ► lowpoly-house.mtl 中的漫反射纹理（diffuse texture）重名为 barn。

> 注意：小心将图像拖到纹理的通用槽（Universal slot）中。如果你将图像拖入资源目录（asset catalog），默认情况下它们是**图像**而不是纹理。

编译并运行你的应用以查看你的新纹理。

![](img/655c9de9cdb851b3baacdbce4a1fae64_180_0.png)

你可以看到纹理已恢复到 sRGB 空间，因为你现在是以原始格式加载它们的。你可以使用 GPU 调试器确认这一点。如果你想在着色器（shader）中避免将 sRGB 转换为线性（linear），可以将纹理设为数据（data）。在 **Textures.xcassets** 中，点击 barn，并在**属性检查器（Attributes inspector）**中将**解释（Interpretation）**更改为 Data：

当应用将 sRGB 纹理加载到非 sRGB 缓冲区时，它会自动从 sRGB 空间转换为线性空间。（转换规则请参阅 Apple 的 Metal Shading Language 文档。）通过访问数据而非颜色，你的着色器可以将颜色数据视为线性的。

你会在上面的图像中注意到，与手动加载 .png 纹理不同，原点是**左上角（Top Left）**。资源目录加载纹理的方式不同。

对地纹理重复操作。

编译并运行，你的颜色现在应该是正确的。

### 适合正确任务的纹理

使用资源目录（asset catalogs）可以让你完全控制纹理的交付方式。目前你只有两个颜色纹理。然而，如果你需要支持具有不同能力的各种设备，可能希望为每种情况准备特定的纹理。

例如，这里是你可以通过检查属性检查器中的不同选项来分配的纹理列表，适用于 Apple watch、1x、2x 和 3x 尺寸，以及 sRGB 和 P3 显示器。

![](img/655c9de9cdb851b3baacdbce4a1fae64_181_0.png)

### 纹理压缩

近年来，人们在压缩纹理方面付出了巨大努力以节省 CPU 和 GPU 内存。你可以使用多种格式，例如 ETC 和 PVRTC。Apple 采用 ASTC 作为最高质量的压缩格式。ASTC 适用于 A8 芯片及更新机型。

在资源目录中使用纹理集允许你的应用自行决定使用哪种是最佳格式。

当你的应用在 macOS 上运行时，查看它消耗了多少内存。点击调试导航器（Debug navigator）并选择 Memory（内存）。这是 30 秒后的使用情况——你的内存消耗将在五分钟内增加并于稳定：

![](img/655c9de9cdb851b3baacdbce4a1fae64_182_0.png)

如果你用 GPU Capture 按钮捕帧，你会发现 GPU 上的纹理格式为 BC7_RGBAunorm。当你使用资源目录时，Apple 会自动为纹理确定最合适的格式。

在 Textures.xcassets 中，选择每个纹理，并在属性检查器中，将像素格式（Pixel Format）从 Automatic 更改为 ASTC 8x8 Compressed - Red Green Blue Alpha。这是一种高压缩格式。编译并运行你的应用，再次检查内存占用。

你会发现内存占用稍微减少。然而，渲染质量也随之下降。对于某些区分，这种质量可能是可以的，但你必须在内存使用和渲染质量之间取得平衡。

![](img/655c9de9cdb851b3baacdbce4a1fae64_182_1.png)

![](img/655c9de9cdb851b3baacdbce4a1fae64_182_2.png)
