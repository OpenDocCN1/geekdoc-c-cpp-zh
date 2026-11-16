

## 使用变换矩阵更新着色器

在本节中，你将创建一个名为 Transform.vert 的新顶点着色器文件。它最初是 Listing 5.3 中 Basic.vert 着色器的副本。提醒一下，你使用 GLSL 而非 C++ 编写此着色器代码。

首先，在 Transform.vert 中使用类型说明符 uniform 声明两个新的全局变量。**统一变量**是一种全局变量，通常在着色器程序的多次调用之间保持不变。这与每次着色器运行时都会改变的 *in* 和 *out* 变量形成对比（例如，每个顶点或像素一次）。要声明统一变量，请使用关键字 uniform，后跟类型，再后跟变量名。

在这种情况下，你需要为两个不同的矩阵定义两个统一变量。可以按如下方式声明这些统一变量：

```
uniform mat4 uWorldTransform;
uniform mat4 uViewProj;
```

这里，*mat4* 类型对应 4x4 矩阵，这是使用齐次坐标的 3D 空间所需的。

然后修改顶点着色器 main 函数中的代码。首先，将 3D 的 *inPosition* 转换为齐次坐标：

```
vec4 pos = vec4(inPosition, 1.0);
```

请记住，此位置处于对象空间。因此，接下来用世界变换矩阵乘以它，将其转换为世界空间，然后再用视图-投影矩阵乘以它，将其转换为裁剪空间：

```
gl_Position = pos * uWorldTransform * uViewProj;
```

这些更改得出了 Transform.vert 的最终版本，如清单 5.11 所示。

### 清单 5.11 Transform.vert 顶点着色器

```
#version 330

// Uniforms for world transform and view-proj
uniform mat4 uWorldTransform;

uniform mat4 uViewProj;

// Vertex attributes

in vec3 inPosition;

void main()
{
    vec4 pos = vec4(inPosition, 1.0);

    gl_Position = pos * uWorldTransform * uViewProj;
}
```

然后修改 Game::LoadShaders 中的代码，使用 Transform.vert 顶点着色器而非 Basic.vert：

```
if (!mSpriteShader->Load("Shaders/Transform.vert", "
{
    return false;
}
```

现在顶点着色器中已有世界变换和视图-投影矩阵的统一变量，你需要一种从 C++ 代码设置这些统一变量的方法。OpenGL 提供了用于在活动着色器程序中设置统一变量的函数。将这些函数的封装函数添加到 Shader 类中很有意义。目前，你可以向 Shader 添加一个名为 SetMatrixUniform 的函数，如清单 5.12 所示。

### 清单 5.12 Shader::SetMatrixUniform

### 实现

```
void Shader::SetMatrixUniform(const char* name, const
{
    // Find the uniform by this name
    GLuint loc = glGetUniformLocation(mShaderProgram,
    // Send the matrix data to the uniform
    glUniformMatrix4fv(
        loc, // Uniform ID
        1, // Number of matrices (only 1 in this
        GL_TRUE, // Set to TRUE if using row vectors
        matrix.GetAsFloatPtr() // Pointer to matrix data
    );
}
```

请注意，SetMatrixUniform 接受一个字符串字面量作为名称，以及一个矩阵。名称对应着色器文件中的变量名。因此，对于 uWorldTransform，参数将是 "uWorldTransform"。第二个参数是要发送到着色器程序的该统一变量的矩阵。

在 SetMatrixUniform 的实现中，你使用 glGetUniformLocation 获取统一变量的位置 ID。从技术上讲，每次更新同一统一变量时都不必查询 ID，因为 ID 在执行期间不会更改。你可以通过缓存特定统一变量的值来改进此代码的性能。

接下来，glUniformMatrix4fv 函数将矩阵分配给统一变量。使用行向量时，此函数的第三个参数必须设置为 GL_TRUE。GetAsFloatPtr 函数只是 Matrix4 中的一个辅助函数，用于返回指向底层矩阵的 float* 指针。

> 注意
> OpenGL 设置统一变量有一种较新的方法，称为**统一缓冲对象**（缩写为 **UBO**）。使用 UBO，你可以将着色器中的多个统一变量分组，并一次性全部发送。对于拥有众多统一变量的着色器程序，这通常比单独设置每个统一变量的值更高效。
> 
> 使用统一缓冲对象，你可以将统一变量拆分为多个组。例如，你可以有一组每帧更新一次的统一变量，以及一组每个对象更新一次的统一变量。视图-投影矩阵每帧不会变化超过一次，而每个角色都会有不同的世界变换矩阵。这样，你可以在帧开始时仅用一个函数调用更新所有每帧统一变量。同样，你可以为每个对象单独更新所有每对象统一变量。要实现此功能，必须更改着色器中声明统一变量的方式，以及在 C++ 代码中镜像该数据的方式。
> 
> 然而，就本书撰写时而言，某些硬件对 UBO 的支持仍然不尽完善。具体来说，某些笔记本电脑的集成显卡芯片不完全支持统一缓冲对象。在其他硬件上，UBO 的运行速度甚至可能比旧方法设置的统一变量更慢。因此，本书不使用统一缓冲对象。然而，缓冲对象的概念在其他图形 API（如 DirectX 11 及更高版本）中很常见。

现在你有了设置顶点着色器矩阵统一变量的方法，需要对其进行设置。由于简单的视图-投影矩阵在整个程序运行期间不会改变，因此只需设置一次。但是，你需要为每个绘制的精灵组件设置一次世界变换矩阵，因为每个精灵组件都使用其所属角色的世界变换矩阵进行绘制。

在 Game::LoadShaders 中，添加以下两行代码，以创建并设置视图-投影矩阵为简单视图投影，假设屏幕宽度为 1024x768：

```
Matrix4 viewProj = Matrix4::CreateSimpleViewProj(1024
mShader.SetMatrixUniform("uViewProj", viewProj);
```

SpriteComponent 的世界变换矩阵稍微复杂一些。角色的世界变换矩阵描述了角色在游戏世界中的位置、缩放和方向。然而，对于精灵，你还希望根据纹理的大小缩放矩形的尺寸。例如，如果角色的缩放为 1.0f，但其精灵对应的纹理图像为 128x128，则需要将单位正方形缩放至 128x128。目前，假设你有加载纹理的方法（如在 SDL 中所做），并且精灵组件通过 mTexWidth 和 mTexHeight 成员变量知道这些纹理的尺寸。

清单 5.13 显示了 SpriteComponent::Draw 的实现（目前）。首先，创建一个缩放矩阵，按纹理的宽度和高度进行缩放。然后，将其与所属角色的世界变换矩阵相乘，以创建精灵所需的世界变换矩阵。接下来，调用 SetMatrixUniform 以在顶点着色器程序中设置 uWorldTransform。最后，像以前一样使用 glDrawElements 绘制三角形。

### 清单 5.13 SpriteComponent::Draw 的当前实现

```
void SpriteComponent::Draw(Shader* shader)
{
    // Scale the quad by the width/height of texture
    Matrix4 scaleMat = Matrix4::CreateScale(
        static_cast<float>(mTexWidth),
        static_cast<float>(mTexHeight),
        1.0f);

    Matrix4 world = scaleMat * mOwner->GetWorldTransform();

    // Set world transform
    shader->SetMatrixUniform("uWorldTransform", world);

    // Draw quad
    glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, r
```

将世界变换和视图-投影矩阵添加到着色器后，你现在可以看到世界中任意位置、缩放和旋转的各个精灵组件，如图 5.7 所示。当然，目前所有矩形都是纯色，因为 `Basic.frag` 仅输出蓝色。这是实现与前几章中 SDL 2D 渲染功能等价的最后需要修复的地方。

![](img/e9afcec1487716b0ef80d7e7c09869c8_386_0.png)

**图 5.7** 使用不同世界变换矩阵绘制精灵组件

## 纹理映射

**纹理映射** 是一种用于渲染的

