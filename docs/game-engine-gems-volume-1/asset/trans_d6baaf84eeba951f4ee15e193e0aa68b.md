

### 15.5 实现说明

Although the computations described above can execute pretty quickly, there is no need to compute them every frame. The resulting light values should be cached until the time of day or location changes, and may even be precomputed for the range of zenith angles for a given location at load time.

虽然上述计算执行速度相当快，但无需每帧都计算。生成的光照值应缓存，直到一天中的时间或位置发生变化，甚至可以在加载时针对给定位置的天顶角范围预先计算。

With physically-based light sources, it becomes important that the materials on your scene's objects are also accurate. If the materials on your objects are set to 100% brightness for diffuse or ambient light, they will look too bright when using these techniques. Real-world materials do not reflect 100% of the incoming light, unless they are perfect mirrors. Work with your art staff to ensure your materials are reasonable.

使用基于物理的光源时，场景中物体的材质也必须准确。如果将物体材质的漫反射或环境光亮度设置为 100%，使用这些技术时它们会显得过亮。现实世界中的材质不会反射 100% 的入射光，除非它们是完美的镜子。请与美术人员合作，确保材质合理。

These algorithms all assume a clear sky at the camera's location; for cloudy conditions, you'll need to attenuate the results. Since the amount of attenuation depends on the thickness of the clouds, how much is really up to you. For really thick clouds, you may want to reduce the amount of direct light and increase the ambient, since the clouds will scatter the sunlight further.

这些算法都假设摄像机位置天空晴朗；对于多云天气，你需要衰减结果。由于衰减量取决于云层厚度，具体衰减多少由你决定。对于非常厚的云层，你可能需要减少直接光量并增加环境光，因为云层会进一步散射阳光。

Strictly speaking, scattered sunlight and moonlight is not really ambient light—it is more accurately modeled as directional light radiating perpendicular to the surface of the sky dome. Without some sort of global illumination scheme, however, your objects will likely appear too dark if the scattered light does not reflect between objects on the ground, and treating it as an ambient term will yield better results. There is certainly nothing to stop you from doing something more sophisticated with the resulting direct and scattered light that these techniques produce.

严格来说，散射阳光和月光并非真正的环境光——它更准确地建模为垂直于天空穹顶表面辐射的方向光。然而，如果没有某种全局光照方案，且散射光不在地面物体之间反射，你的物体可能会显得过暗；将其视为环境光项会产生更好的结果。当然，没有什么能阻止你对这些技术产生的直接光和散射光做更复杂的处理。

### References

- [1] R. E. Bird 和 C. Riordan. "无云大气中水平和倾斜平面上直接和漫射辐照度的简单太阳光谱模型". 技术报告 No. SERI/TR-215-2436, 太阳能研究所, 1984.
- [2] Peter Duffett-Smith. 《使用计算器进行实用天文学》. 剑桥大学出版社, 1988.
- [3] Frédo Durand 和 Julie Dorsey. "交互式色调映射". 渲染技术 Eurographics 工作坊论文集 2000, 第 219–230 页.
- [4] Henrik Wann Jensen, Frédo Durand, Julie Dorsey, Michael M. Stark, Peter Shirley, 和 Simon Premože. "基于物理的夜空模型". 第 28 届计算机图形学与交互技术年会论文集, 2001, 第 399–408 页.
- [5] 英国和美国水文年鉴办公室. 《天文年鉴和美国天文及水文年鉴说明补充》. 女王陛下文具局, 1961.

## Chapter 16: Rendering Physically-Based Skyboxes

Frank Kane

Sundog Software, LLC

### Overview

Simple, GPU-friendly algorithms exist for rendering realistic skyboxes in real time for any given time and location. This gem reviews the Preetham et al. model [3] for accurately distributing luminance throughout a sky, with some extensions to ensure natural-looking results. When paired with the gem "Physically Based Outdoor Scene Lighting", outdoor scenes with lighting that perfectly matches the sky become possible. Algorithms for procedurally generating realistic skyboxes are surprisingly simple, and enable continuous time of day effects in your engine.

存在简单且 GPU 友好的算法，可用于在任何给定时间和地点实时渲染逼真的天空盒。本文回顾了 Preetham 等人 [3] 模型，用于在天空中准确分布亮度，并加入了一些扩展以确保效果自然。当与“户外场景基于物理的照明”文章配合使用时，就能实现与天空完美匹配的照明的室外场景。程序生成逼真天空盒的算法出人意料地简单，并能在引擎中实现连续的一天中的时间效果。

### 16.1 Generating and Drawing the Skybox

First, some skybox basics: a skybox is just that—a cube that is always rendered around the camera's location such that it moves and rotates with the camera, which is colored to look like a sky. You may properly position it by simply zeroing out the translation components of your view matrix before drawing it.

首先，了解一些天空盒基础：天空盒就是一个立方体，它始终围绕摄像机位置渲染，随摄像机一起移动和旋转，并着色以呈现天空效果。你可以在绘制之前，仅通过将视图矩阵的平移分量置零来正确定位它。

Intuition would tell us to render the skybox as the first thing in your frame, as it's infinitely distant and everything else will be drawn in front of it. You could just disable depth buffer reads and writes, and draw the skybox instead of clearing the depth buffer, and go about rendering your scene. This simple approach, however, is not the most optimal, since you'll end up spending time filling your color buffer with a bunch of sky that will end up being overdrawn by your scene. In reality, you won't save anything on modern hardware by not clearing the depth buffer along with your color buffer at the beginning of the frame—in fact, it may hurt performance. A better approach is to keep clearing your color and depth buffer together, then draw your skybox as the last thing in your frame, with depth buffer reads enabled to prevent drawing parts of the sky that are not visible. If you use an infinite projection matrix while rendering the skybox, drawing the skybox last instead of first will render correctly and can gain you some performance.

直觉告诉我们应该将天空盒作为帧中的第一个渲染对象，因为它在无限远处，其他所有内容都会绘制在它前面。你可以禁用深度缓冲区读写，绘制天空盒而不是清除深度缓冲区，然后渲染场景。然而，这种简单的方法并非最优，因为你会花时间将颜色缓冲区填满大量天空，而这些天空最终会被场景覆盖。实际上，在现代硬件上，在帧开始时不连同颜色缓冲区一起清除深度缓冲区并不能节省任何开销——事实上，这可能会损害性能。更好的方法是保持一起清除颜色缓冲区和深度缓冲区，然后将天空盒作为帧中的最后一个绘制对象，启用深度缓冲区读取以防止绘制不可见的天空部分。如果在渲染天空盒时使用无限投影矩阵，将天空盒放在最后而不是第一个绘制可以正确渲染，并能带来一些性能提升。

For procedurally generated skyboxes, we'll use a vertex program to render the sky just using vertex colors (disable texturing and enable smooth shading). This implies that the geometry of the skybox warrants some effort; you need to have enough vertices in the skybox to achieve convincing results, but too many may impact performance. In the images shown in Figure 16.1, each face of the skybox cube consists of a 40×40 grid. You may choose to have a higher vertex density near the horizon, as this is where sky colors change more quickly; you may also choose to have higher vertex density vertically rather than horizontally, as the sky color changes less rapidly as you look around the horizon than as you look up toward the sky's zenith.

对于程序生成的天空盒，我们将使用顶点程序仅使用顶点颜色来渲染天空（禁用纹理并启用平滑着色）。这意味着天空盒的几何体需要投入一些精力；你需要在天空盒中有足够的顶点才能获得令人信服的效果，但顶点过多可能会影响性能。在图 16.1 所示的图像中，天空盒立方体的每个面都由 40×40 网格组成。你可以选择在地平线附近使用更高的顶点密度，因为天空颜色变化更快；你也可以选择垂直方向而非水平方向使用更高的顶点密度，因为环顾地平线时天空颜色变化不如向上看向天顶时那么快。

![](img/7ba1225bb0e5a87be0fd35866408ffa7_370_0.png)

Figure 16.1: (See also Color Plates.) Physically-based skybox generated for (left) late morning and (right) twilight. (Images courtesy of Sundog Software, LLC.)

图 16.1：（另请参阅彩色插页。）为（左）上午晚些时候和（右）黄昏生成的基于物理的天空盒。（图片由 Sundog Software, LLC 提供。）

If you're certain that the bottom of your skybox will never be visible, you may omit this face—but as an engine developer, you shouldn't make this assumption. Your users might end up rendering the Earth from space using your skybox for a star-field and wonder why nothing is drawn underneath it. You may also want to allow your users to shift the skybox down by some amount instead of drawing it perfectly centered with the camera position; if the terrain in the scene doesn't actually extend all the way to the horizon, this is a simple way to cover up that fact.

如果你确定天空盒底部永远不会可见，可以省略该面——但作为引擎开发者，你不应该做此假设。你的用户可能会使用你的天空盒作为星空来从太空渲染地球，并奇怪为什么下面没有绘制任何东西。你可能还希望允许用户将天空盒向下移动一定量，而不是将其与摄像机位置完美居中绘制；如果场景中的地形并未实际延伸至地平线，这是一种简单的掩盖事实的方法。

The techniques in this gem will work just as well with a sky dome. However, a box is simpler, allows us to easily cull faces of the box that are not visible, and since we're using vertex colors instead of texture mapping, the corners of the box are not at all perceptible.

本文的技术同样适用于天空穹顶。然而，立方体更简单，允许我们轻松剔除不可见的面，并且由于我们使用顶点颜色而不是纹理映射，立方体的角落完全不可察觉。

Using a conventional projection matrix, the size of the skybox must be chosen with care; you need to ensure that it falls within the near and far clipping planes of your view frustum. This becomes especially problematic with engines that dynamically adjust the near and far clip planes based on the scene's bounding volumes to maximize depth buffer resolution. An elegant way around this problem is to render the skybox using an infinite projection matrix and with w-coordinates of zero, assuring the far clip plane is irrelevant and the skybox is drawn at maximum depth. Care must be taken with this technique to avoid round-off error artifacts [1].

使用常规投影矩阵时，必须谨慎选择天空盒的大小；你需要确保它位于视锥体的近裁剪平面和远裁剪平面之间。对于根据场景包围体动态调整近裁剪平面和远裁剪平面以最大化深度缓冲区分辨率的引擎，这尤其成问题。绕过此问题的优雅方法是使用无限投影矩阵和 w 坐标为零来渲染天空盒，确保远裁剪平面无关紧要，且天空盒在最大深度处绘制。使用此技术时需小心，以避免舍入误差产物 [1]。

### 16.2 Computing the Skybox Vertex Colors

Back in 1993, Perez et al. developed a simple model for distributing luminance across the sky, by fitting equations to experimental data [2]. In 1999, Preetham et al. extended this method to work in full color in a paper presented at Siggraph. The only input required is the position of the sun (or moon) in the sky, and the _turbidity_ of the atmosphere. Turbidity is a measure of the particulate matter in the atmosphere; a reasonable value for realistic-looking scenes is around 2.2. Higher values imply more polluted skies, and will result in more dramatic sunsets.

早在 1993 年，Perez 等人通过将方程拟合到实验数据，开发了一个用于在天空中分布亮度的简单模型 [2]。1999 年，Preetham 等人在 Siggraph 上发表的论文中将此方法扩展为全彩色工作。所需的唯一输入是天空中太阳（或月亮）的位置，以及大气的 _浑浊度_。浑浊度是大气中颗粒物的度量；对于逼真场景，合理的值约为 2.2。较高的值意味着天空更污染，并会导致更壮观的日落。

The position of the sun or moon is specified in polar coordinates. \(\theta_S\) is the angle from the up axis to the light source, and \(\phi_S\) is the angle from the South axis (positive is toward East.) The `Ephemeris` class introduced in "Physically-Based Outdoor Scene Lighting" is useful for computing the position of the sun and moon for a given time and location.

太阳或月亮的位置以极坐标指定。\(\theta_S\) 是从上轴到光源的角度，\(\phi_S\) 是从南轴的角度（正向为东）。在“户外场景基于物理的照明”中介绍的 `Ephemeris` 类可用于计算给定时间和地点的太阳和月亮位置。

The Perez model for distributing luminance across the sky is given by

天空中分布亮度的 Perez 模型由以下公式给出

```
\( F(\theta, \gamma) = (1 + Ae^{B/cos\theta})(1 + C^{\gamma} + Ecos^2 \gamma) \)。
```

We refer to this equation as the "Perez function". Here, \(\theta\) is the angle of the skybox vertex from the up axis, and \(\gamma\) is the angle between the vertex and the sun or moon—your vertex program will compute these angles given the position of each skybox vertex. We'll discuss the constants _A_ through _E_ shortly.

我们将此方程称为“Perez 函数”。这里，\(\theta\) 是天空盒顶点相对于上轴的角度，\(\gamma\) 是顶点与太阳或月亮之间的角度——你的顶点程序将根据每个天空盒顶点的位置计算这些角度。我们将稍后讨论常数 _A_ 到 _E_。

To arrive at an actual luminance value \(Y_P\) for a given vertex, you need to compute the above function once for the vertex's position, and again for the position of the sun or moon (this only needs to be computed when the time of day changes, then cached):

要为给定顶点得到实际亮度值 \(Y_P\)，你需要对顶点位置计算一次上述函数，再对太阳或月亮的位置计算一次（这只需在一天中的时间变化时计算，然后缓存）：

