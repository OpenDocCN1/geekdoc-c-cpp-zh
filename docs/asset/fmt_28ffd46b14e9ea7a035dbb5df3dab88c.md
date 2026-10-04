
```swift
pipelineDescriptor.vertexDescriptor = MTKMetalVertexDescriptorFromModelIO(mesh.vertexDescriptor)
```

你已经用必要的信息设置了流水线描述符。`MTLRenderPipelineDescriptor` 有许多其他属性，但目前你将使用默认值。

从描述符创建流水线状态：

```swift
let pipelineState =
```

![](img/655c9de9cdb851b3baacdbce4a1fae64_35_0.png)

```swift
try device.makeRenderPipelineState(descriptor: pipelineDescriptor)
```

创建流水线状态需要宝贵的处理时间，因此上述所有操作都应该是一次性的设置。在实际应用中，你可能会创建多个流水线状态来调用不同的着色函数或使用不同的顶点布局。

# 渲染 (Rendering)

从现在开始，代码应该每帧执行一次。MTKView 有一个每帧运行的代理方法，但由于你只是在做一个静态视图的简单渲染器，你不需要每帧不断刷新屏幕。

在执行图形操作时，GPU 的工作是从 3D 场景输出单个纹理。这个纹理类似于物理相机创建的数字图像。纹理将显示在设备的屏幕帧上。

# 渲染通道 (Rendering passes)

如果你正尝试实现一个真实的渲染器，你将想要考虑阴影、光照和反射。这些每一项都需要大量的计算，通常在单独的渲染通道中完成。例如，阴影渲染通道将渲染整个 3D 模型场景，但只保留灰度阴影信息。第二个渲染通道将以全色渲染模型。

# Metal 教程 (Metal by Tutorials)

为了完成向渲染编码器发送命令并最终完成帧，添加以下代码：

```swift
// 1
renderEncoder.endEncoding()
// 2
guard drawable = view.currentDrawable else {
    fatalError()
// 3
commandBuffer.present(drawable)
commandBuffer.commit()
```

遍历代码：

- 1. 你告诉渲染编码器没有更多的绘制调用了。

- 2. 你从 MTKview 获取 drawable。MTKview 由 Core Animation MetalLayer 支撑，该层拥有一个 Metal 可以读写的 drawable 纹理。

- 3. 请求命令缓冲区显示 MTKView 的 drawable 并将其提交给 GPU。

# 子网格 (Submeshes)

模型由子网格组成。当艺术家创建一个汽车时，他们可能会有车身和轮胎。一种材料是光泽漆，另一种材料也是。这个球体只有一个子网格，所以你只需要使用一个。

添加以下代码：

```swift
guard let submesh = mesh.submeshes.first else {
  fatalError()
}
```

现在是激动的部分：绘制！你在 Metal 中通过绘制调用进行绘制。

添加以下代码：

```swift
renderEncoder.drawIndexed(type: .triangle,
indexCount: submesh.indexCount,
indexType: submesh.indexType,
indexBuffer: submesh.indexBuffer,
indexBufferOffset: 0)
```

在这里，你正在指示 GPU 渲染由子网格正确排列顶点的三角形缓冲区。

最后，在播放场的末尾添加此：

```swift
PlaygroundPage.current.liveView = view
```

有了这行代码，你可以在辅助编辑器中看到 Metal 视图。运行播放场，在播放场的实时视图中，你将看到奶油色背景上的一个红色球体。

注意：有时候游场（playgrounds）不会在应该运行的时候编译或运行。如果你确定代码编写得正确，请重启 Xcode 并重新加载游场。在运行前等待一秒钟。

恭喜！你已经编写了你的第一个 Metal 应用，并且还使用了许多在你以后编写的每个 Metal 应用中都会用到的 API 命令。

![](img/655c9de9cdb851b3baacdbce4a1fae64_40_0.png)

## 挑战

在你创建初始球体网格（mesh）的地方，尝试将球体设置为不同的尺寸。如果将尺寸从以下值更改，会发生什么呢：

```
[0.75, 0.75, 0.75]
```

改为：

```
[0.2, 0.75, 0.2]
```

改变球体的颜色。在着色器函数字符串中，你会看到

```
return float4(1, 0, 0, 1);
```

这返回了红=1，绿=0，蓝=0，结果就是红色。尝试更改数字（从零到一）以获得不同的颜色。保持 Ray Wunderlich 的品牌风格：

```
float4(0, 0.4, 0.21, 1)
```

在下一章中，你将在 Blender 中近距离观察 3D 模型。然后在你的 Swift Playground 中继续学习，你将导入并渲染一个火车模型。

## 第 2 章：3D 模型

作者：Caroline Begbie

什么让一个优秀的游戏变得更好？华丽的图形效果！创建像《巫师3 3》、《毁灭战士》和《神秘海域 4》中那种令人惊叹的画质，需要一组程序员和 3D 艺术家紧密合作。你在屏幕上看到的是使用自定义渲染器渲染的 3D 模型，这与你在上一章中编写的类似，但要先进得多。尽管如此，渲染 3D 模型的原理是相同的。

在本章中，你将研究 3D 模型。你将学习如何创建它们、它们由什么组成以及如何用不同的颜色和样式渲染它们。

## 什么是 3D 模型？

3D 模型由顶点（vertices）组成。每个顶点指的是 3D 空间中的一点，由 x, y 和 z 值组成。

![](img/655c9de9cdb851b3baacdbce4a1fae64_42_0.png)

正如你在上一章中看到的，你将这些顶点发送到 GPU 进行渲染。

打开本章的启动游场。该游场包含两个页面：Render and Export 3D Model（渲染并导出 3D 模型）和 Import Train（导入火车）。它还包含火车 .obj 模型。如果你没有看到这些内容，你可能需要使用右上角的图标显示项目导航器（Project navigator）。

![](img/655c9de9cdb851b3baacdbce4a1fae64_42_1.png)

从项目导航器中，选择 Render and Export 3D Model。它包含了第 1 章“Hello, Metal!”的代码。检查游场实时视图（live view）中渲染的球体；目前，球体渲染为一个实心红色形状。如果想以顶点的形式查看球体，请将渲染模式从三角形（triangles）改为点（points）。在游场末尾，将绘制调用（draw call）的类型从 type: .triangle 改为 type: .point：

```
renderEncoder.drawIndexedPrimitives(type: .point,
indexCount:submesh.indexCount,
indexType:submesh.indexType,
indexBuffer:submesh.indexBuffer,
indexBufferOffset: 0)
```

运行游场，你将看到这个结果：

![](img/655c9de9cdb851b3baacdbce4a1fae64_43_0.png)

现在真的能看到球体的 3D 特性了！顶点在水平方向上分布均匀，但由于你是在二维屏幕上查看，球体边缘的点看起来比中间的点靠得更近。

撤销上一次更改并恢复到渲染实心三角形。

以线框模式（wireframe）渲染模型允许你看到每个单独三角形的边缘。若要以线框模式渲染，请在绘制调用之前添加以下行代码：

```
renderEncoder.setTriangleMode(.lines)
```

这告诉 GPU 渲染线条而不是实心三角形。运行游场：

![](img/655c9de9cdb851b3baacdbce4a1fae64_43_1.png)

### Metal 教程：第 2 章：3D 模型

球体看起来是弯的是因为渲染的三角形数量很多——GPU 在这里渲染的是直线。如果你渲染较少的三角形，弯曲的模型看起来会有“块状感”。

在 Blender 或 Maya 等 3D 应用中，你通常操作点、线和面。点是顶点。线（也称为边）是顶点之间的线。面是三角形区域。

顶点通常组织成三角形，因为 GPU 硬件专门用于处理它们。GPU 的核心指令期望看到三角形。在所有可能的形状中，为什么是三角形呢？

- 三角形在二维中可以绘制的点最少。

- 无论你如何移动这三个点，它们都保持在同一个平面上。

- 从任何顶点划分三角形，它都会变成两个三角形。

## 使用 Blender 创建模型

要创建 3D 模型，你需要一个 3D 建模应用。这些应用从免费到昂贵不等。免费应用中最好的是 Blender —— 这本书贯穿使用的。Blender 被许多专业人士使用，如果你更熟悉其他 3D 应用，如 Maya，请随时使用它。

从 https://www.blender.org 下载并安装 Blender。运行 Blender，点击左下角的启动可以看到：

![](img/655c9de9cdb851b3baacdbce4a1fae64_45_0.png)

你的界面可能有所不同。点击设置，让 Blender 看起来像这里所示：

> 注意：如果你想创建自己的模型，最好的起点是 https://www.raywenderlich.com/blender-tutorial-for-beginners。

该教程教你如何制作球体。你可以在游场的末尾查看并渲染它。

![](img/655c9de9cdb851b3baacdbce4a1fae64_46.png)

## 3D 文件格式

有很多标准的 3D 文件格式。在本章中，我们将使用 Wavefront OBJ (.obj) 用于单个模型，USD 用于动态和非动态模型。以下是每个格式的概述：

- .obj：由 Wavefront Technologies 开发，已经存在了一段时间；几乎每个 3D 应用都支持导入导出 .obj 文件。但该格式不支持动画。

- .glTF：由负责 Vulkan 和 OpenGL 的人开发，该格式较新且仍在开发中。由于其灵活性，它拥有强大的社区支持。支持动态模型。

- .blend：这是 Blender 的原生文件格式。

- .dae：这是 COLLADA 标准格式。该格式支持动画。在本书期间，SceneKit 可以导入 .dae，但 Model 不能。

- .fbx：由 Autodesk 拥有的专用格式。这是一个常用的格式，支持动画，但因为是私有的且没有统一的标准正在失去青睐。

- .usd：由 Pixar 引入的可扩展开源格式。USD 可以引用模型和文件，非常适合共享资源。.usd 是一个 USD 归档文件，包含了模型或场景所需的所有内容。Apple 已采用 USD 格式用于他们的 AR 模型。

> 注意：Apple 提供了转换和检查 USD 文件的工具。这些工具可以在 https://developer.apple.com/augmented-reality/quick-look/ 下载。

.obj 文件仅包含单个模型，而 .glTF 和 .usd 文件是整个场景的容器，包含模型、动画、相机和灯光。

## 导出到 Blender

现在你已经设置好了 Blender，是是将模型从你的游场导出到 Blender 了。

仍然在 Render and Export 3D Model 中，在游场顶部创建网格的地方，将：

```
let mdlMesh = MDLMesh(sphereWithExtent: [0.75, 0.75, 0.75],
segments: [100, 100],
inwardNormals: false,
geometryType: .triangles,
allocator: allocator)
```

改为：

```
let mdlMesh = MDLMesh(coneWithExtent: [1,1,1],
segments: [10, 10],
inwardNormals: false,
cap: true,
geometryType: .triangles,
allocator: allocator)
```

这将生成一个原始锥体网格来代替球体。运行播放器，你将看到线框结构的锥体。

![](img/655c9de9cdb851b3baacdbce4a1fae64_48_0.png)

这就是你将使用 Model I/O 导出的模型。

在 Finder 中，进入“文档”（Documents）文件夹，创建一个名为 `Shared Playground Data` 的新目录。Playgrounds 保存的文件将存储在此处，因此请确保你的命名正确。

> 注意：全局常量 `playgroundSharedDataDirectory` 持有此文件夹的名称。

要导出锥体，请在创建网格之后添加此代码：

```swift
// begin export code
// 1
let asset = MDLAsset(mdlMesh)
asset.add(mesh)
// 2
let fileExtension = "obj"
guard MDLAsset.canExportFile(fileExtension) else {
    fatalError("Can't export a \(fileExtension) format")
}
// 3
do {
    let url = playgroundSharedDataDirectory.appendingPathComponent(
        "primitive.\(fileExtension)"
    )
    try asset.export(to:url)
} catch {
    fatalError("Error \(error.localizedDescription)")
}
// end export code
```

观察一下发生了什么：

- 1. Model I/O 中场景的顶层是一个 `MDLAsset`。你可以向该 asset 添加网格、相机和灯光等子对象，并构建出一个完整的层级结构。

- 2. 检查 Model I/O 是否可以导出 `.obj` 类型的文件。

- 3. 将代码导出到存储在 `Shared Playground Data` 中的目录。

运行播放器以导出代码对象。

# .obj 文件格式

在 Finder 中，导航到 “文档” > “Shared Playground Data”。该播放器创建了两个文本文件：`primitive.obj` 和 `primitive.mtl`。

使用纯文本编辑器打开 `primitive.obj`。

以下是 `example.obj` 文件示例。它描述了一个具有四个角顶点的原始体；`.obj` 文件的布局类似，只不过它有很多顶点。

```
# Apple ModelIO OBJ File: plane
mtllib plane.mtl
g submesh
v 0 0.5 -0.5
v 0 -0.5 -0.5
v 0 -0.5 0.5
v 0 0.5 0.5
vn -1 0
vt 1 0
v 0 0
vt 0 1
vt 1 1
usel material_1
f 1/1/1 2/2/1 3/3/1
f 1/1/1 3/3/1 4/4/1
s off
```

以下是详细解析：

- *mtllib*: 这是随附的 `.mtl` 文件的名称。它包含了模型的材质和纹理文件名。

- *g*: 一组顶点的开始。

- *v*: 顶点。对于锥体，你会有 102 个这样的。

- *vn*: 表面法线。这是一个正交指向的向量——即直接指向外部。稍后我们将学习更多关于法线的知识。

- *vt*: uv 坐标。纹理使用 uv 坐标而不是 xy 坐标。

- *usemtl*: 为后续面提供表面信息（如颜色）的材质名称。该材质定义在随附的 `.mtl` 文件中。

- *f*: 定义面。在这个平面示例中有两个面。每个面有三个元素，由顶点/纹理/法线索引组成。例如最后一个列出的面：`4/4/1` 将是第四个顶点元素 / 第四个纹理元素 / 第一个法线元素：`0 0.5 0.5 / 1 1 / -1 0 0`。

- *s*: 平滑度，目前关闭，没有组会形成光滑表面。

# .mtl 文件格式

你导出的第二个文件包含模型的材质。材质描述了 3D 渲染器应该如何为顶点上色。顶点应该是光滑的还是发光的？粉色的吗？反射的？`.mtl` 文件包含了这些属性的值。

使用纯文本编辑器打开 `primitive.mtl`：

```
# ModelI/O MTL File: primitive.mtl
newmtl material_1
Kd 1 1 1
Ka 0 0 0
Ks 0
a 0
subsurface 0
metallic 0
specularTint 0
roughness 0.9
anisotropicRotation 0
sheen 0.05
sheenTint 0
clearCoat 0
clearCoatGloss 0
```

# Metal by Tutorials

## 第 2 章：3D 模型

数据格式，在随后的章节中，你将加载法线和纹理坐标属性。

3. 偏移量（offset）指定了该特定数据在缓冲区中的起始位置。
