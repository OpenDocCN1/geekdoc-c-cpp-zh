
从 OpenGL 相机视角看，按顺时针方向推进的顶点是*背面朝向*的，不会被渲染。这种将“正面朝向”定义为逆时针方向的做法有时称为*环绕顺序*，可以通过函数调用 glFrontFace(GL_CCW) 显式设置为逆时针（默认值），或通过 glFrontFace(GL_CW) 设置为顺时针。同样，渲染的是正面朝向还是背面朝向的三角形，也可以显式设置。实际上，为此我们指定的是哪些三角形*不*被渲染——也就是哪些三角形被“剔除”。我们可以通过调用 glCullFace(GL_BACK) 指定剔除背面朝向的三角形（尽管这没有必要，因为这是默认值）。或者，我们可以分别将参数 GL_BACK 替换为 GL_FRONT 或 GL_FRONT_AND_BACK，来指定剔除正面朝向的三角形，甚至剔除所有三角形。

正如我们将在第 6 章看到的，3D 模型通常设计为外表面由具有相同环绕顺序的三角形构成——最常见的是逆时针——因此如果启用了剔除，默认情况下会渲染模型外表面中面向相机的部分。由于 OpenGL 默认假定环绕顺序为逆时针，如果模型设计为以*顺时针*环绕顺序显示，那么在启用背面剔除时，程序员需要调用 glFrontFace(GL_CW) 来处理这种情况。

请注意，在 GL_TRIANGLE_STRIP 的情况下，每个三角形的环绕顺序会交替变化。OpenGL 在构建每个后续三角形时通过“翻转”顶点序列来补偿这一点，如下所示：0-1-2，然后是 2-1-3、2-3-4、4-3-5、4-5-6，依此类推。

背面剔除通过确保 OpenGL 不花时间光栅化和渲染那些永远不会被看到的表面来提高性能。我们在本章中见过的大多数示例都非常小，因此几乎没有启用面剔除的动力（一个例外是图 4.9 所示的示例，其中有 100,000 个实例化动画立方体，这可能会在某些系统上造成性能挑战）。在实践中，大多数 3D 模型通常是“封闭的”，因此习惯上会例行启用背面剔除。例如，我们可以通过如下修改 display() 函数，为程序 4.3 添加背面剔除：

```cpp
void display(GLFWwindow* window, double currentTime) {
    …
    glEnable(GL_CULL_FACE);
    // draw the cube
    …
    glEnable(GL_DEPTH_TEST);
    glDepthFunc(GL_LEQUAL);
    glFrontFace(GL_CW);              // the cube vertices have clockwise winding order
    glDrawArrays(GL_TRIANGLES, 0, 36);

    // draw the pyramid
    ...
    glEnable(GL_DEPTH_TEST);
    glDepthFunc(GL_LEQUAL);
    glFrontFace(GL_CCW);            // the pyramid vertices have counter-clockwise winding order
    glDrawArrays(GL_TRIANGLES, 0, 18);
}
```

在使用背面剔除时，正确设置环绕顺序很重要。错误的设置，例如本应为 GL_CCW 却设置为 GL_CW，可能导致渲染对象的内部而不是外部，进而产生类似于透视矩阵不正确时的畸变。

效率并不是进行面剔除的唯一原因。在后续章节中，我们将看到其他用途，例如当我们想要看到 3D 模型的内部时，或在使用透明度时。

### 补充说明

OpenGL/GLSL 中还有大量其他功能和结构可用于管理和利用数据，而我们在本章中只是触及了表面。例如，我们还没有描述*uniform 块*，这是一种组织 uniform 变量的机制，类似于 C 语言中的*结构体*。uniform 块甚至可以设置为从缓冲区接收数据。另一种强大的机制是*着色器存储块*，它本质上是一个着色器可以写入的缓冲区。

关于管理数据的众多选项，一个极好的参考资料是*OpenGL SuperBible* [SW15]，尤其是题为“数据”的一章（第 7 版中的第 5 章）。它还描述了我们所涵盖的各种命令的许多细节和选项。本章的前两个示例程序，程序 4.1 和程序 4.2，受到*SuperBible*中类似示例的启发。

还有其他类型的数据需要学习如何管理，以及如何沿着 OpenGL 管线向下传递。其中之一是*纹理*，它包含彩色图像数据（例如照片中的图像数据），可用于“绘制”场景中的对象。我们将在第 5 章研究纹理图像。另一个我们将进一步研究的重要缓冲区是*深度缓冲区*（或 Z 缓冲区）。当我们在第 8 章研究阴影时，它将变得很重要。关于在 OpenGL 中管理图形数据，我们还有很多东西要学！

### 练习

- **4.1** *（项目）* 修改程序 4.1，将立方体替换为你自己设计的其他简单 3D 形状。请务必在 `glDrawArrays()` 命令中正确指定顶点数量。

- **4.2** *（项目）* 在程序 4.1 中，“视图”矩阵在 display() 函数中简单地定义为相机位置的负值：

  ```cpp
  vMat = glm::translate(glm::mat4(1.0f), glm::vec3(-cameraX, -cameraY, -cameraZ));
  ```

  用图 3.13 所示计算的实现替换这段代码。这将允许你通过指定相机位置和三个朝向轴来定位相机。你会发现有必要存储第 3.7 节描述的向量 U、V、N。然后，尝试不同的相机视点，并观察渲染立方体的最终外观。

- **4.3** *（项目）* 修改程序 4.4，加入第二个“行星”，即你在练习 4.1 中自定义的 3D 形状。确保你的新“行星”与现有行星处于不同的轨道上，以免它们相撞。

- **4.4** *（项目）* 修改程序 4.4，使“视图”矩阵使用“look-at”函数构造（如第 3.9 节所述）。然后尝试将“look-at”参数设置为不同位置，例如看向太阳（在这种情况下场景应显示正常）、看向行星或看向月球。

- **4.5** *（研究）* 提出 `glCullFace(GL_FRONT_AND_BACK)` 的一种实际用途。

### 参考文献

- [BL20] Blender，Blender 基金会，访问于 2020 年 7 月，https://www.blender.org/
- [HT12] J. Hastings-Trew，JHT's Planetary Pixel Emporium，访问于 2020 年 7 月，http://planetpixelemporium.com/
- [MA16] Maya，AutoDesk 公司，访问于 2020 年 7 月，http://www.autodesk.com/products/maya/overview
- [NA16] NASA 3D 资源，访问于 2020 年 7 月，http://nasa3d.arc.nasa.gov/
- [OL16] Legacy OpenGL，访问于 2020 年 7 月，https://www.opengl.org/wiki/Legacy_OpenGL
- [SW15] G. Sellers、R. Wright Jr. 和 N. Haemel，*OpenGL SuperBible: Comprehensive Tutorial and Reference*，第 7 版（Addison-Wesley，2015）。

## 第 5 章：纹理映射

- 5.1 *加载纹理图像文件* … 104
- 5.2 *纹理坐标* … 106
- 5.3 *创建纹理对象* … 108
- 5.4 *构造纹理坐标* … 109
- 5.5 *将纹理坐标加载到缓冲区* … 110
- 5.6 *在着色器中使用纹理：采样器变量和纹理单元* … 111
- 5.7 *纹理映射：示例程序* … 112
- 5.8 *Mipmapping* … 114
- 5.9 *各向异性过滤* … 119
- 5.10 *环绕与平铺* … 120
- 5.11 *透视畸变* … 122
- 5.12 *纹理——更多 OpenGL 细节* … 124
- *补充说明* … 125

纹理映射是将图像覆盖到光栅化模型表面上的技术。它是为渲染场景增加真实感的最基本、最重要的方法之一。

纹理映射如此重要，以至于有专门的硬件支持，可实现非常高的性能，从而实现实时照片级真实感。*纹理单元*是专为纹理处理设计的硬件组件，现代显卡通常包含多个纹理单元。
