
// 2

`float2 pos = cam.ray.origin.xz;`

`pos *= 0.1;`

// 3

`pos = floor(fmod(pos, 2.0));`

`float check = mod(pos.x + pos.y, 2.0);`

// 4

`col = check * 0.5 + 0.5;`

}

```

解析代码：

- 1. 如果选中的物体是平面，则构建棋格。
- 2. 获取相机光线沿平面的位置。
- 3. 使用坐标创建棋格图案。
- 4. 根据 `check` 结果应用颜色。

![](img/655c9de9cdb851b3baacdbce4a1fae64_575_0.png)

反射定律规定，入射光射击物体表面的角度 [576]

![](img/655c9de9cdb851b3baacdbce4a1fae64_576_0.png)

运行游场，你会发现天空现在也反射在球体和地板上。

![](img/655c9de9cdb851b3baacdbce4a1fae64_579_0.png)

你可以稍微旋转一下相机，让反射看起来更有趣。在内核函数中添加此参数：

```
constant float &time [[buffer(0)]]
```

并替换此行：

```
float3 camPos = float3(15.0, 7.0, 0.0);
```

替换为：

```
float3 camPos = float3(sin(time) * 15.0,
sin(time) * 5.0 + 7.0,
cos(time) * 15.0);
```

运行游场，你将看到相同的图像，但现在有了精的动画。

# 折射

折射是自然界中常见的的光与物体之间的另一种相互作用。虽然自然界中的大多数物体是不透明的——因此吸收了它们的大部分光——但少数半透明或透明的物体允许光穿过它们。

折射定律比入射光向量和出射光向量角度相等要复杂一点。

![](img/655c9de9cdb851b3baacdbce4a1fae64_580_0.png)

折射遵循斯涅定律，该定律规定角度之比等于折射率倒数之比：

$$\frac{\sin \theta_2}{\sin \theta_1} = \frac{\text{IOR of media 1}}{\text{IOR of media 2}}$$

**折射率**（IOR）是一个定义光在各种介质中传播速度的常数。IOR 定义为真空中光速除以光在该特定介质中的相速度。

> 注意：有已关于各种介质 IOR 值的列表，但我们感兴趣的是空气（IOR = 1）和水（IOR = 1.33）。https://en.wikipedia.org/wiki/List_of_refractive_indices

例如，如果你正尝试寻找穿过水的折射光向量角度，你只需要知道入射光向量角度（你可以从反射光向量获取），然后将其除以水的 IOR（因为空气的 IOR 为 1，不影响计算）：

```
sin(theta2) = sin(theta1) / 1.33
```

是时候继续编码了！

打开 2. 折射游场页面并运行它。代码与上一节相同，你会看到动画。该游场页面的 Resources 文件夹打开 `Shaders.metal`。

你首先需要一种方法知道射线何时在球体内部，因为你只在那种情况下进行折射。在内核计算函数中，循环之前添加此代码：

```
bool inside = false;
```

在这一章的第一部分中，你识别了物体，所以你现在知道射线何时击中球体。你可以根据射线是进入还是离开球体来改变距离的正负号。正如你从之前的章节所知，负距离意味着你位于正在发送射线的物体内部。

找到：

```
float2 dist = distToScene(cam.ray);
```

在其下方添加此行：

```
dist.x *= inside ? -1.0 : 1.0;
```

这调整了 x 值以反映你是否在球体内部。接下来，你需要调整法线。删除此行：

```
float3 normal = getNormal(cam.ray);
```

现在找到此行：

```
if (dist.x < eps) {
```

在该行之后，重新添加法线定义：

```
float3 normal = getNormal(cam.ray) * (inside ? -1.0 : 1.0);
```

你现在有了一个法线，它在球体外部时指向外，在球体内部时指向内部。

# Metal 教程

将以下行移动到内部 if 块中，因为你从现在起只想让平面具有反射性：

```
cam = reflectRay(cam, normal, eps);
```

在内部块之后，添加一个 `else` 块，在其中让球体具有折射性：

```
// 1
if (closestObject == SphereObj) {
inside = !inside;
// 2
float ior = inside ? 1.0 / 1.33 : 1.33;
cam = refractRay(cam, normal, eps, ior);
}
```

通过代码：

- 1. 检查你是否在球体内部。在第一次交点，射线现在进入了球体，所以将 `inside` 设为 true 并进行折射。在第二次交点，射线离开球体，所以将 `inside` 设为 false，不再发生折射。
- 2. 根据射线方向设置折射率（IOR）。水的 IOR 为 1.33。

通过这段代码，你使用一个重新配置的渲染通道描述符（它使用了了自己的着色器函数和顶点描述符）来构建水管道状态。

在 `RendererDraw.swift` 中，添加此新方法来渲染水：

```
func renderWater(renderEncoder: MTLRenderCommandEncoder) {
    renderEncoder.pushDebugGroup("water")
    renderEncoder.setRenderPipelineState(waterPipelineState)
    renderEncoder.setVertexBuffer(water.vertexBuffers[0].buffer,
                                offset: 0, index: 0)
    uniforms.modelMatrix = waterTransform.matrix
    renderEncoder.setVertexBuffer(uniforms,
                               length: MemoryLayout<Uniforms>.stride,
                               index: Int(BufferIndexUniforms.rawValue))
    for submesh in water.submeshes {
        renderEncoder.drawIndexedPrimitives(type: .triangle,
                                          indexCount: submesh.indexCount,
                                          indexType: submesh.indexType,
                                          indexBuffer: submesh.indexBuffer.buffer,
                                          indexBufferOffset: submesh.indexBuffer.offset)
    }
renderEncoder.popDebugGroup()
}
```

这通过设置其渲染流水线状态、顶点缓冲区和统一变量（uniforms）来配置渲染编码器。对于每个子网格（submesh），你像其他章节中那样执行了一个绘制调用。

回到 `Renderer.swift`，在 `draw(in:)` 中，结束渲染编码之前添加此代码：

```
renderWater(renderEncoder: renderEncoder)
```

创建水着色器。在 Shaders 组中，创建一个名为 `Water.metal` 的新 Metal 文件。记得将其同时添加到 macOS 和 iOS 目标（targets）。

将以下代码添加到新创建的文件中：

```
#import "Common.h"

struct VertexIn {
    float4 position [[attribute(0)]];
    float2 uv [[attribute(2)]];
}

struct VertexOut {
    float4 position [[position]];
    float2 uv;
}
```

# Metal 教程

## 第 20 章：高级光照

```
vertex VertexOut
vertex_water(const VertexIn vertex_in [[stage_in]],
              constant Uniforms &uniforms
              [buffer(CreateIndexUniforms)]) {
    VertexOut vertex_out;
    float4x mvp = uniforms.projectionMatrix * uniforms.viewMatrix
                 * uniforms.ModelMatrix;
    vertex_out.position = mvp * vertex_in.position;
    vertex_out.uv = vertex_in.uv;
    return vertex_out;
}

fragment float4
fragment_water(VertexOut vertex_in [[stage_in]]) {
    return float4(0.0, 0.3, 0.5, 1.0);
}
```

这是渲染水面四边形并赋予其蓝色调的最小配置。

编译并运行，你将看到这张带有你新水面的的图像。

![](img/655c9de9cdb851b3baacdbce4a1fae64_588_0.png)

## 2. 反射渲染通道

水面应该反射其周围环境。在第 12 章“环境”中，你曾将天空盒反射到物体上，但这次你还打算在水面上反射房屋和地形。

你将从水面下方向上将场景渲染到一个纹理中。然后你将获取此纹理并将其翻转后渲染到水面上。

![](img/655c9de9cdb851b3baacdbce4a1fae64_589_0.png)

为了实现这一点，你首先需要创建一个新的渲染器。

在 `Renderer.swift` 中，为 `Renderer` 添加此属性：

```
let reflectionPass: RendererPass
```

在 `init(metalView:)` 中，在调用 `.init()` 之前添加以下内容：

```
reflectionPass = RendererPass(name: "reflection",
size: metalView.drawableSize)
```

`RendererPass` 将创建一个带有可绘制纹理（drawable texture）的渲染器描述符。你需要在 `reflectionPass` 在视图缩放时更新这些纹理的大小，因此在 `drawableWillChange(_ size:)` 中添加：

```
reflectionPass.updateTextures(size: size)
```

现在你已经设置好了渲染通道，接下来创建一个编码器，并将整个场景渲染到反射通道中。

在 `draw(in:)` 中，下方添加以下代码：

```
// 1
let reflectEncoder = commandBuffer.makeRenderEncoder(
descriptor: reflectionPass.descriptor)!
reflectEncoder.setDepthState(depthStencilState)
// 2
reflectionCamera.transform = camera.transform
reflectionCamera.transform.position.y = -camera.transform.y
reflectionCamera.transform.rotation.x = -camera.transform.rotation.x
// 3
uniforms.viewMatrix = reflectionCamera.viewMatrix
renderHouse(renderEncoder:reflectEncoder)
renderTerrain(renderEncoder:reflectEncoder)
renderSkybox(renderEncoder:reflectEncoder)
reflectEncoder.endEncoding()
```

逐行分析代码：

- 创建一个新的渲染编码器。这是反射独特之处。
- 设置反射相机的变换。反射相机的 y 轴位置设置为 `-camera.transform.y`，反射相机的 x 轴旋转设置为 `-camera.transform.rotation.x`。
- 设置统一变量的视图矩阵为反射相机的视图矩阵。渲染房屋、地形和天空盒。结束编码。

- 创建一个新的渲染编码器。这是反射的独特部分。
- 你将从水面下方向上，地将场景渲染到一个纹理中。
- 然后你将获取此纹理并将其翻转后渲染到水面上。
- 为了实现这一点，你首先需要创建一个新的渲染器。
- 在 `Renderer.swift` 中，为 `Renderer` 添加此属性：
- 在 `init(metalView:)` 中，在调用 `.init()` 之前添加以下内容：
- `RendererPass` 将创建一个带有可绘制纹理的渲染器描述符。
- 你需要 `reflectionPass` 在视图缩放时更新这些纹理的大小，因此在 `drawableWillChange(_ size:)` 中添加：
- 现在你已经设置好了渲染通道，创建一个编码器，并将整个场景渲染到反射通道中。
- 在 `draw(in:)` 中，下方添加以下代码：
- 创建一个新的渲染编码器。这是反射的独特部分。
- 你将从水面下方向上，地将场景渲染到一个纹理中。
- 然后你将获取此纹理并将其翻转后渲染到水面上。
- 为了实现这一点，你首先需要创建一个新的渲染器。
- 在 `Renderer.swift` 中，为 `Renderer` 添加此属性：
- 在 `init(metalView:)` 中，在调用 `.init()` 之前添加以下内容：
- `RendererPass` 将创建一个带有可绘制纹理的渲染器描述符。
- 你需要 `reflectionPass` 在视图缩放时更新这些纹理的大小，因此在 `drawableWillChange(_ size:)` 中添加：
- 现在你已经设置好了渲染通道，创建一个编码器，并将整个场景渲染到反射通道中。
- 创建一个新的渲染编码器。这是反射的独特部分。
- 你将从水面下方向上，地将场景渲染到一个纹理中。
- 然后你将获取此纹理并将其翻转后渲染到水面上。
- 为了实现这一点，你首先需要创建一个新的渲染器。
- 设置反射相机的变换。
- 渲染的。
- 在 `Renderer.swift` 中，在 `renderWater(renderEncoder:)` 之前添加此代码：

```
renderEncoder.setFragmentTexture(reflectionPass.texture, index: 0)
```

- 渲染的。编码器。这会将反射通道的纹理发送到水着色器。
- 现在，在 `Water.metal` 中，为片元器函数添加一个新的参数：

```
texture2d<float> reflectionTexture [[texture(0)]]
```

将 return 行替换为以下代码：

```
// 1
constexpr sampler s(filter::linear, address::repeat);
// 2
float width = reflectionTexture.width() * 2.0;
float height = reflectionTexture.height() * 2.0;
float x = vertex_in.position.x / width;
float y = vertex_in.position.y / height;
float2 reflectionCoords = float2(x, 1 - y);
// 3
float4 color = reflectionTexture.sample(s, reflectionCoords);
color = mix(color, float4(0.0, 0.3, 0.5, 1.0), 0.3);
return color;
```

逐行分析代码：

- 创建一个新的线性过滤和重复寻址采样器。
- 确定反射坐标将使用反转的 Y 值，因为镜像是水面上方的场景镜像。注意你乘以 2.0，因为纹理只有一半大小。
- 从反射纹理中采样颜色，并与水面之前的蓝色调进行混合。

- 编译并运行，你将看到水面上反射了房屋、地形和天空盒。

## 2. 反射渲染通道

水面应该反射其周围环境。在第 12 章“环境”中，你曾将天空盒反射到物体上，但这次你还打算在水面上反射房屋和地形。

你将从水面下方向上将场景渲染到一个纹理中。然后你将获取此纹理并将其翻转后渲染到水面上。

![](img/655c9de9cdb851b3baacdbce4a1fae64_589_0.png)

为了实现这一点，你首先需要创建一个新的渲染器。

在 `Renderer.swift` 中，为 `Renderer` 添加此属性：
