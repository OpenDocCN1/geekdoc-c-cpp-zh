

你是否要为绘制的每个像素执行光照计算？

因为你可能想要使用许多技术来显示场景，所以并没有真正的万能方法。为了允许更多自定义，包括OpenGL在内的图形API支持**着色器程序**——在图形硬件上执行以完成特定任务的小程序。重要的是，着色器是*独立程序*，拥有各自独立的`main`函数。

> 注记
>
> 着色器程序不使用C++编程语言。本书为着色器程序使用GLSL编程语言。虽然GLSL表面上看起来像C，但有许多GLSL特有的语义。本书不会一次性介绍所有GLSL细节，而是在需要时介绍相关概念。

因为着色器是独立程序，你将它们写在独立文件中。然后在你的C++代码中，你需要告诉OpenGL何时编译和加载这些着色器程序，并指定你希望OpenGL使用这些着色器程序做什么。

虽然你可以在游戏中使用多种不同类型的着色器，但本书专注于两个最重要的着色器：顶点着色器和片元（或像素）着色器。

## 顶点着色器

一个**顶点着色器**程序为绘制的每个三角形的每个顶点运行一次。顶点着色器将顶点属性数据作为输入。然后顶点着色器可以根据需要修改这些顶点属性。虽然你可能不清楚为何要修改顶点属性，但随着本章的深入，这会变得更加明显。

鉴于三角形有三个顶点，你可以将顶点着色器视为每个三角形运行三次。但是，如果你使用顶点缓冲和索引缓冲，那么你会较少调用顶点着色器，因为一些三角形共享顶点。这是使用顶点和索引缓冲而非仅使用顶点缓冲的额外优势。请注意，如果你每帧多次绘制同一模型，那么每次绘制时的顶点着色器调用彼此独立。

## 片元着色器

在三角形的顶点经过顶点着色器后，OpenGL必须确定颜色缓冲中的哪些像素对应于该三角形。将三角形转换为像素的过程称为光栅化。有许多不同的光栅化算法，但当今的图形硬件会为我们执行光栅化。

片元着色器（或像素着色器）的工作是确定每个像素的颜色，因此片元着色器程序至少为每个像素执行一次。这种颜色可能会考虑表面的属性，例如纹理、颜色和材质。如果场景中有光照，片元着色器也可能执行光照计算。由于潜在计算非常多，平均3D游戏在片元着色器中的代码比在顶点着色器中多得多。

## 编写基本着色器

虽然你可以从C++代码中的硬编码字符串加载着色器程序，但将它们放在独立文件中要好得多。本书为顶点着色器文件使用.vert扩展名，为片元着色器文件使用.frag扩展名。

由于这些源文件使用不同的编程语言，它们位于章节的Shaders子目录中。例如，Chapter05/Shaders包含本章着色器的源文件。

### Basic.vert文件

Basic.vert包含顶点着色器代码。请记住，这不是C++代码。

每个GLSL着色器文件首先必须指定所使用的GLSL编程语言版本。以下行表示与OpenGL 3.3对应的GLSL版本：

```
#version 330
```

接下来，因为这是顶点着色器，你必须为每个顶点指定顶点属性。这些属性应与先前创建的顶点数组对象的属性匹配，并且是顶点着色器的输入。但是，在GLSL中，`main`函数不接收任何参数。相反，着色器输入看起来像全局变量，并用特殊的`in`关键字标记。

目前，你只有一个输入变量——3D位置。以下行声明此输入变量：

```
in vec3 inPosition;
```

`inPosition`变量的类型是`vec3`，对应于三个浮点值的向量。这将包含与顶点位置对应的x、y和z分量。你可以通过点语法访问`vec3`的每个分量；例如，`inPosition.x`访问向量的x分量。

与C/C++程序一样，着色器程序将`main`函数作为其入口点：

- 单击此处查看代码图像

```
void main()
{
    // TODO: Shader code goes here
}
```

请注意，此处的`main`函数返回`void`。GLSL也使用全局变量来定义着色器的输出。在此情况下，你将使用名为gl_Position的内置变量来存储着色器的顶点位置输出。

目前，顶点着色器直接将顶点位置从inPosition复制到gl_Position。但是，gl_Position期望四个分量：常规（x、y、z）坐标加上一个称为w分量的第四个分量。我们将在本章后面介绍w代表什么。目前，假设w始终为1.0。要将inPosition从vec3转换为vec4，你可以使用以下语法：

- 单击此处查看代码图像

```
gl_Position = vec4(inPosition, 1.0);
```

### 清单5.3 Basic.vert代码

- 单击此处查看代码图像

```
// Request GLSL 3.3

#version 330

// Any vertex attributes go here

// For now, just a position.
in vec3 inPosition;

void main()
{
    // Directly pass along inPosition to gl_Position
    gl_Position = vec4(inPosition, 1.0);
}
```

### Basic.frag文件

片元着色器的工作是为当前像素计算输出颜色。对于Basic.frag，你将为所有像素硬编码一个蓝色输出颜色。

与顶点着色器一样，片元着色器始终以#version行开头。接下来，你声明一个全局变量来存储输出颜色，使用out变量说明符：

```
out vec4 outColor;
```

outColor变量是一个vec4，对应于RGBA颜色缓冲的四个分量。

接下来，你声明片元着色器程序的入口点。在此函数内，你将outColor设置为像素所需的颜色。蓝色的RGBA值为(0.0, 0.0, 1.0, 1.0)，这意味着你使用以下赋值：

单击此处查看代码图像

```
outColor = vec4(0.0, 0.0, 1.0, 1.0);
```

### 清单5.4 Basic.frag代码

单击此处查看代码图像

```
// Request GLSL 3.3

#version 330

// This is output color to the color buffer
out vec4 outColor;

void main()
{
    // Set to blue
    outColor = vec4(0.0, 0.0, 1.0, 1.0);
}
```

## 加载着色器

一旦你编写好独立的着色器文件，就必须在游戏的C++代码中加载这些着色器，以让OpenGL了解它们。从高层次来看，你需要遵循以下步骤：

- 1. 加载并编译顶点着色器。
- 2. 加载并编译片元着色器。
- 3. 将两个着色器链接到一个“着色器程序”中。

加载着色器有许多步骤，因此最好声明一个独立的Shader类，如清单5.5所示。

### 清单5.5 初始着色器声明

单击此处查看代码图像

```
class Shader
{
public:
    Shader();
    ~Shader();

    // Load the vertex/fragment shaders with the given
    bool Load(const std::string& vertName,
              const std::string& fragName);

    // Set this as the active shader program
    void SetActive();

private:

// Tries to compile the specified shader
bool CompileShader(const std::string& fileName,
                   GLenum shaderType, GLuint& out

// Tests whether shader compiled successfully
bool IsCompiled(GLuint shader);

// Tests whether vertex/fragment programs link
bool IsValidProgram();

// Store the shader object IDs
GLuint mVertexShader;
GLuint mFragShader;
GLuint mShaderProgram;
};
```

请注意，此处的成员变量对应着色器对象ID。它们具有与顶点和索引缓冲类似的对象ID。（GLuint只是OpenGL对unsigned int的版本。）

你在private部分声明CompileShader、IsCompiled和IsValidProgram，因为它们是Load使用的辅助函数。这减少了代码

