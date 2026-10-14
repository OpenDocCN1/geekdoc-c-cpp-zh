

CPU 到 GPU 的数据传输是一个主要的瓶颈。

| Pipeline Functions | 1996 | 1997 | 1999 |
|---|---|---|---|
| Application specific tasks (Moving objects, setting up camera, object level culling) | CPU | CPU | CPU |
| Transformation | CPU | CPU | GPU |
| Lighting | CPU | CPU | GPU |
| Clipping | CPU | GPU | GPU |
| Rasterization | GPU | GPU | GPU |

GPU 的演进得益于 SGI（Silicon Graphics Inc.）于 1989 年发布的图形行业最广泛使用的应用程序编程接口（API）SGI-GL 的发布，该接口后来以 OpenGL 的名义流行起来。1993 年，SGI 发布了其首批面向工作站的显卡，而首批 3D 消费级图形硬件则由 Matrox、nVidia、3DFX 和 ATI 等公司提供。然而，在当时的硬件中，GPU 与 CPU 之间的区别并不那么清晰。虽然图形管线的后期阶段已在 GPU 硬件中实现，但 CPU 仍然起着重要作用，尤其是在涉及变换的管线第一部分。

Figure 15.1. Evolution of early graphics pipeline leading to a fixed function pipeline in 1999.

像 Quake 和 Doom 这样的游戏推动了显卡在游戏行业中的快速采用。

第一个接近当前形式的图形处理器单元由 3DFX 于 1996 年推出，名为 Voodoo 卡。CPU 仍然执行顶点变换和光照，而 Voodoo 提供着色、纹理映射、z 缓冲和光栅化。仍然无法在每个像素上评估光照模型，因此 Phong 着色或凹凸映射的效果在交互速率下仍然不可实现。1999 年，通过 nVidia 的 Geforce 256 和 ATI 的 Radeon 7500（Figure 15.1）的引入，首个现代 GPU 硬件成为现实，其中顶点变换和光照计算也被移至 GPU。四条并行管线有助于更快地渲染，并具有多纹理和凹凸映射的新功能。CPU 与 GPU 之间更快的通信通道允许获得更高的性能。然而，该硬件仍然遵循固定功能管线，因为一旦数据发送到 GPU 管线，就无法修改。固定功能是通过 OpenGL 和 DirectX 等 API 定义的功能集实现的。因此，如果在图形 API 中添加了新功能，固定功能硬件就无法利用它们。Figure 15.2 显示了这种固定管线的不同阶段。顶点控制从 CPU 接收三角形数据。VS/T & L（Vertex Shader/Texture and Lighting）阶段变换顶点并为每个顶点分配属性（例如颜色、纹理坐标、切线）。光照计算也可以在 VS/T & L 阶段进行，以为顶点分配颜色。下一个阶段对被裁剪的顶点进行裁剪和属性插值。随后进行光栅化，以标记被裁剪三角形覆盖的像素。着色器实现对三角形触及的每个像素的属性（例如纹理坐标、颜色、法线）进行插值。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_375_0.png)

# Figure 15.2. A fixed graphics hardware pipeline.

最后，执行光栅操作以混合颜色，实现抗锯齿或半透明效果。执行深度缓冲区测试以解决遮挡。帧缓冲接口管理帧缓冲区的读写。

2001 年，我们见证了首个可编程图形管线的出现，通过 ATI Radeon 8500 和 Microsoft X-box，首次可以在 GPU 的部分进行编程。与以往不同，程序员现在可以发送数据以及顶点程序（通常称为着色器），这些着色器将在数据通过 GPU 时对其进行操作。这些着色器是用类似汇编的特定着色器语言编写的小型内核，在管线的顶点处理阶段提供有限的可编程性。可编程图形管线随后在 2002 年通过 nVidia GeForce FX 和 Radeon 9700 带来了首个完全可编程 GPU。这些显卡允许进行逐像素操作，并具有专门用于编程顶点和像素（片段）着色器的硬件。到 2003 年，完整的浮点支持和先进的纹理处理开始出现在显卡中，使得第一波用于非图形计算的 GPU 应用成为可能。

到 2006 年，图形硬件开始利用图形管线提供的大量数据独立性。目标是将灵活性推向着色器程序。早期的高级着色器语言开始出现，以提供更易用的编程接口。GeForce 6 是首个将数据独立性简化为具有固定阶段之间的多个并行多核阶段的管线的 GPU。第一个并行阶段是顶点着色器，它读取顶点位置并计算其在帧缓冲器上的位置。多个线程独立处理不同的顶点。片段着色器处理对每个像素贡献的浮点 RGBA 颜色。同样，多个线程也独立处理不同的像素。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_376_0.png)

Figure 15.3. This shows the programmable GPU via the abstraction of the GeForce 6 card (a) and GeForce 8 card (b).

在这两个并行阶段之间是裁剪和光栅化的固定阶段。同样，混合和深度缓冲区处理也可以在称为光栅操作处理器（ROP）的单元中并行执行。在并行的片段着色器和 ROP 处理器之间，有一个固定的操作，将来自不同线程的片段组合在一起。因此，这种交替的并行和固定阶段将 GPU 转变为大规模并行和可编程处理器。Figure 15.3 显示了 nVidia GeForce 6 中此类管线的抽象。请注意，在此情况下，顶点着色器有 6 个线程，像素着色器有 4 个线程，ROP 操作有 16 个线程。此外，帧缓冲内存的分区允许在不降低帧率的情况下实现更高分辨率的图形。因此，从那时起，GPU 已被视为一种强大的可编程浮点计算和存储单元，可以用于需要计算密集型应用，而这些应用与图形无关。

在这一阶段，图形硬件仍然具有用于顶点、像素和 ROP 操作的专用着色器。GeForce 8 通过统一着色器并将其转变为完全可编程的统一处理器，即流线型处理器或 SP（Figure 15.3）改变了这一点。通过这一变化，图形管线模型成为纯粹的软件抽象。为了利用 GPU 能力，开发了新的编程语言。CUDA 是 nVidia 为 nVidia 显卡提供的此类语言。同样，ATI Stream 用于 ATI 显卡，DirectX 10 用于任一显卡。

## 15.2 Development of Graphics APIs and Libraries

计算机图形学变得非常流行，尤其是在视频游戏和仿真社区。因此，有多个专门的 API 来简化不同图形管线阶段和应用需求的编程。这些 API 提供了一种以抽象方式访问硬件的方法，同时利用特定显卡的特殊硬件功能。然而，由于即使在几年前的固定管线也很流行，许多 API，尤其是那些在固定图形管线时代发展起来的 API，已经演进以适应可编程管线。

OpenGL 是最古老的跨语言跨平台 3D 图形渲染接口，提供与 GPU 交互的方式。GLUT 是 OpenGL 实用工具包，用于编写与用于渲染场景的窗口系统无关的 OpenGL 程序。它为 OpenGL 实现了一个简单的窗口 API，使学习 OpenGL 变得更加容易。GLUT 还在多个操作系统和 PC 上提供可移植的 API。OpenGL 被定义为一组函数，可由客户端程序调用。这些函数在表面上类似于 C，但与语言无关。OpenGL 的流行主要归功于其官方文档的质量，这些文档以封面颜色命名（红、橙、绿和蓝书分别是《OpenGL 编程指南》的第一至第四版）。通常，GLU、GLEE 或 GLEW 等伴随库与 OpenGL 绑定，以支持当代硬件可能不支持的有用功能，如 mipmapping 或细分。OpenGL 着色语言（GLSL）是一种基于 C 语法的<|message|> 高级着色语言，最初设计用于让 OpenGL 使用汇编级或硬件特定语言访问可编程 GPU。OpenGL ES 是 OpenGL API 的扩展，用于嵌入式设备的编程。WebGL 是用于渲染 3D 图形的 Javascript API。Direct3D 是微软提供的类似 API，承诺在 Windows 操作系统上提供更好的性能，而 Metal 是为 Apple 的 iOS8 首次推出的 API。

Vulkan 是一个更新的跨平台 API。它最初被称为“下一代 openGL 计划”。它建立在 AMD 的 Mantle API 之上。除了像 OpenGL 一样优化 GPU 上的性能外，Vulkan 还优化了 CPU 的使用，并将 CPU 需要的任何内容分发到多个核心。它适用于高端显卡和移动设备。与 OpenGL 不同，它提供计算内核和图形着色器的统一管理，消除了同时使用着色器 API 和图形 API 的需求。

现代 GPU 提供了巨大的潜力，可以使用 GPU 解决大量可并行化的通用问题。然而，这意味着程序员必须很好地了解图形 API 和 GPU 硬件，以便将通用问题映射到顶点、纹理和着色器程序上。为缓解这一问题，nVidia 开发了 CUDA，一种编程语言，提供

