
接下来让我们看看细分求值着色器。它开头有一行代码：

```glsl
layout (quads, equal_spacing, ccw) in;
```

这乍看可能与控制着色器中的 “out” 布局语句有关，但实际上二者无关。相反，这一行是指示细分器生成顶点，使它们排列成一个大矩形（一个“四边形”）。它还指定细分段（内部和外部）等长（稍后我们将看到不等长细分段的用途）。“ccw”参数指定生成细分网格顶点时的绕序（此处为逆时针）。

细分器生成的顶点随后被发送到求值着色器。因此，求值着色器*可能*既从控制着色器（通常作为控制点）接收顶点，又从细分器（细分网格）接收顶点。在程序 12.1 中，仅从细分器接收顶点。

求值着色器对细分器生成的每个顶点执行一次。可使用内置变量 gl_TessCoord 访问顶点位置。细分网格的朝向使其位于 X-Z 平面，因此 gl_TessCoord 的 X 和 Y 分量被应用在网格的 X 和 Z 坐标上。网格坐标（因而 gl_TessCoord 的值）范围为 0.0 到 1.0（稍后在计算纹理坐标时会很方便）。求值着色器随后使用 mvp 矩阵来确定每个顶点的朝向（在之前章节的示例中，这是由顶点着色器完成的）。

最后，片段着色器对每个像素仅输出恒定颜色黄色。当然，我们也可以像前几章看到的那样，用它为场景应用纹理或光照。

## 12.2 贝塞尔曲面的细分

现在让我们扩展程序，使简单的矩形网格变成贝塞尔曲面。细分网格应为我们提供足够多的顶点来采样曲面（如果想要更多顶点，可以提高内部/外部细分级别）。现在我们需要做的是将*控制点*送入管线，然后使用这些控制点执行计算，把细分网格转换为所需的贝塞尔曲面。

## 需要带原子单位的乳白色背景容器图

### 实验目的：

通过本实验了解IR基团频率与分子结构之间的关系，掌握红外光谱图的解析方法。

### 实验原理：

红外光谱是一种分子吸收光谱，当样品受到频率连续变化的红外光照射时，分子吸收其中某些频率的辐射，引起分子振动和转动能级的跃迁，通过记录透过率或吸光度随波数或波长的变化，得到红外光谱图。

### 实验仪器与药品：

- 傅里叶变换红外光谱仪
- 压片机
- 溴化钾（KBr）
- 苯甲酸样品

### 实验步骤：

- 1. 将少量干燥的溴化钾粉末置于玛瑙研钵中研磨均匀。
- 2. 加入少量苯甲酸样品，继续研磨使其与溴化钾充分混合。
- 3. 将混合物装入压片模具中，在压片机上压成透明薄片。
- 4. 将薄片放入红外光谱仪样品室，在4000～400 cm⁻¹范围内扫描。
- 5. 记录红外光谱图，分析主要吸收峰对应的官能团。

将这些顶点重新定位到由控制点指定的曲面上，并用纹理图像绘制所得曲面。它还展示了 Java/JOGL 应用程序的相关部分，具体是在 display() 函数中。在本例中，控制点源自顶点着色器（它们在顶点着色器中硬编码），而不是从 Java/JOGL 应用程序进入 OpenGL 管线。代码清单之后还有更多细节。

### 程序 12.2 贝塞尔曲面的细分

### 顶点着色器

```glsl
#version 430
out vec2 texCoord;
uniform mat4 mvp;
layout (binding = 0) uniform sampler2D tex_color;

void main(void)
{
    // this time the vertex shader defines and sends out control points:
    const vec4 vertices[] = {
        vec4(-1.0, 0.5, -1.0, 1.0), vec4(-0.5, 0.5, -1.0, 1.0),
        vec4( 0.5, 0.5, -1.0, 1.0), vec4( 1.0, 0.5, -1.0, 1.0),
        vec4(-1.0, 0.0, -0.5, 1.0), vec4(-0.5, 0.0, -0.5, 1.0),
        vec4( 0.5, 0.0, -0.5, 1.0), vec4( 1.0, 0.0, -0.5, 1.0),
        vec4(-1.0, 0.0,  0.5, 1.0), vec4(-0.5, 0.0,  0.5, 1.0),
        vec4( 0.5, 0.0,  0.5, 1.0), vec4( 1.0, 0.0,  0.5, 1.0),
        vec4(-1.0, -0.5,  1.0, 1.0), vec4(-0.5, 0.3,  1.0, 1.0),
        vec4( 0.5, 0.3,  1.0, 1.0), vec4( 1.0, 0.3,  1.0, 1.0) };

    // compute an appropriate texture coordinate for the current vertex, shifted from [-1,+1] to [0..1]
    texCoord = vec2((vertices[gl_VertexID].x + 1.0) / 2.0, (vertices[gl_VertexID].z + 1.0) / 2.0);

    gl_Position = vertices[gl_VertexID];
}
```

### 细分控制着色器

```glsl
#version 430
in vec2 texCoord[];                 // The texture coords output from the vertex shader as scalars arrive
out vec2 texCoord_TCSout[];          // in an array and are then passed through to the evaluation shader

uniform mat4 mvp;
layout (binding = 0) uniform sampler2D tex_color;
layout (vertices = 16) out;          // there are 16 control points per patch
```

```glsl
float bu2 = 3.0 * u * u * (1.0-u);                 // 3u^2(1-u)
float bu3 = u * u * u;                             // u^3
float bv0 = (1.0-v) * (1.0-v) * (1.0-v);           // (1-v)^3
float bv1 = 3.0 * v * (1.0-v) * (1.0-v);           // 3v(1-v)^2
float bv2 = 3.0 * v * v * (1.0-v);                 // 3v^2(1-v)
float bv3 = v * v * v;                             // v^3

// output the position of this vertex in the tessellated patch
vec3 outputPosition =
    bu0 * ( bv0*p00 + bv1*p01 + bv2*p02 + bv3*p03 )
  + bu1 * ( bv0*p10 + bv1*p11 + bv2*p12 + bv3*p13 )
  + bu2 * ( bv0*p20 + bv1*p21 + bv2*p22 + bv3*p23 )
  + bu3 * ( bv0*p30 + bv1*p31 + bv2*p32 + bv3*p33 );
gl_Position = mvp * vec4(outputPosition, 1.0f);

// output the interpolated texture coordinates
vec2 tc1 = mix(texCoord_TCSout[0], texCoord_TCSout[3], gl_TessCoord.x);
vec2 tc2 = mix(texCoord_TCSout[2], texCoord_TCSout[1], gl_TessCoord.x);
vec2 tc = mix(tc2, tc1, gl_TessCoord.y);
texCoord_TESout = tc;
}
```

### 片段着色器

```glsl
#version 430
in vec2 texCoord_TESout;
out vec4 color;
uniform mat4 mvp;
layout (binding = 0) uniform sampler2D tex_color;

void main(void)
{   color = texture(tex_color, texCoord_TESout);
}
```

### Java / JOGL 应用程序

```java
// This time we also pass a texture to paint the surface.
// Load the texture in init() as usual, then enable it in display()

public void display(GLAutoDrawable drawable)
{   ...
    gl.glActiveTexture(GL_TEXTURE0);
    gl.glBindTexture(GL_TEXTURE_2D, textureID);
    ...
    gl.glFrontFace(GL_CCW);
    gl.glPatchParameteri(GL_PATCH_VERTICES, 16);    // number of vertices per patch = 16
    gl.glPolygonMode(GL_FRONT_AND_BACK, GL_FILL);
    gl.glDrawArrays(GL_PATCHES, 0, 16);             // total number of patch vertices: 16 x 1 patch = 16
}
```

顶点着色器现在指定 16 个控制点（“补片”顶点），表示一个特定的贝塞尔曲面。在本例中，它们都被归一化到范围 [-1..+1]。顶点着色器还使用控制点来确定适合细分网格的纹理坐标，其值在范围 [0..1] 内。需要再次强调，顶点着色器输出的顶点**并非**将被光栅化的顶点，而是贝塞尔控制点。使用细分时，补片顶点**绝不**会被光栅化——只有细分后的顶点会进入光栅化。

控制着色器仍然指定内部和外部细分级别。它现在还有额外的职责：将控制点和纹理坐标转发给求值着色器。注意，细分级别只需指定一次，因此该步骤仅在第一次调用（第 0 次调用）期间完成（回想一下，TCS 对每个顶点运行一次——因此本例中有 16 次调用）。为方便起见，我们为每个细分级别指定了 32 个细分段。

接下来，求值着色器执行所有贝塞尔曲面计算。main() 开头的大段赋值语句从每个传入的 gl_in 的传入 gl_Positions 中提取控制点（注意，这些对应于控制着色器的 gl_out 变量）。然后使用从细分器传入的网格点计算混合函数的权重，得到新的 outputPosition；随后对其应用模型-视图-投影矩阵，为每个网格点生成输出 gl_Position，从而形成贝塞尔曲面。

还必须创建纹理坐标。顶点着色器仅为每个控制点位置提供了一个纹理坐标。但正在渲染的并不是控制点——我们最终需要为数量多得多的细分网格点提供纹理坐标。实现这一点有多种方法——这里我们使用 GLSL 中方便的 *mix* 函数对它们进行线性插值。*mix()* 函数需要三个参数：(a) 起点，(b) 终点，以及 (c) 插值，其范围为 0 到 1。它返回起点和终点之间与插值对应的值。由于细分网格坐标的范围也是 0 到 1，因此可以直接用于此目的。
