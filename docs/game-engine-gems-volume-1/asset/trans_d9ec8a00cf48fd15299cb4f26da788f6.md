
将顶点位置转换为屏幕空间，分别针对使用矩阵 motionA 的前一帧和使用矩阵 motionB 的当前帧。生成的位置作为纹理坐标输出，将由片元着色器读取。

```
uniform mat4   mvp, motionA, motionB;

void main()
{
    // Transform the position using the ordinary MVP
    gl_Position = mvp * gl_Vertex;

    // Transform the position into screen space using
    // from the preceding frame (A) and the current
    gl_TexCoord[0] = motionA * gl_Vertex;
    gl_TexCoord[1] = motionB * gl_Vertex;
}
```

顶点着色器执行的矩阵乘法会生成两个四维齐次屏幕空间位置。重要的是，这些位置应以齐次形式进行插值，并且透视除法（按 w 坐标除）应在片元着色器中进行。否则，三角形内部的插值位置将不正确，尤其是对于顶点位于相机后方的三角形。

在用于渲染到速度缓冲区的片元着色器中，我们通过将齐次插值位置 P^A_screen 和 P^B_screen 除以它们的 w 坐标，来获取帧 A 和帧 B 的二维屏幕空间位置，如清单 17.2 所示。然后通过以下公式相减得到屏幕空间速度 V：

(17.4)
$$ V = \frac{\mathbf{P}^{B}_{\text{screen}}}{(\mathbf{P}^{B}_{\text{screen}})_w} - \frac{\mathbf{P}^{A}_{\text{screen}}}{(\mathbf{P}^{A}_{\text{screen}})_w}, $$

其中仅计算速度的 x 和 y 分量。

清单 17.2：这个 GLSL 片元着色器计算屏幕空间速度，并将其写入输出颜色的红色和绿色分量。velocityScale 参数保存公式 (17.6) 中显示的 s/r_max 的值。深度直接从当前位置的 w 坐标获取，并写入输出颜色的蓝色分量。深度梯度使用硬件导数函数计算，其分量中较大的一个被写入输出颜色的 alpha 分量。

```
uniform vec2   velocityScale;

void main()
{
  // Divide by the w-coordinates to get 3D position
  vec2 posA = gl_TexCoord[0].xy / gl_TexCoord[0].w;
  vec2 posB = gl_TexCoord[1].xy / gl_TexCoord[1].w;

  // Subtract the positions and scale to get velocity
  vec2 veloc = (posB.xy - posA.xy) * velocityScale;

  // Clamp the velocity to a max magnitude of 1.0.
  float vmax = max(abs(veloc.x), abs(veloc.y));
  gl_FragColor.xy = veloc / max(vmax, 1.0);

  // Pass the current depth through.
  gl_FragColor.z = gl_TexCoord[1].w;

  // Calculate the max component of the depth gradient
  vec2 grad = vec2(ddx(gl_TexCoord[1].w), ddy(gl_TexCoord[1].w));

  gl_FragColor.w = max(abs(grad.x), abs(grad.y));
}
```

速度 V 的大小是无界的，但在后处理阶段，我们每个像素只能读取有限数量的颜色样本，并且不希望它们离被处理的像素太远。因此，为了确保平滑的模糊效果，我们需要对速度的大小施加某种限制。首先，我们将速度除以我们希望在像素位置与用于模糊的任何颜色样本之间允许的最大距离 r_max。值 1/r_max 是一个常数，作为参数传递给片元着色器，速度乘以该参数。我们还可以在此参数中包含一个归一化因子 s，它考虑两帧之间的时间并调整运动模糊效果的整体强度。我们定义 s 为

(17.5) \( s = \frac{t_0}{\Delta t} m, \)

其中 \( t_0 \) 是帧间的目标时间间隔，\( \Delta t \) 是前一帧与当前帧之间的实际时间，而 \( m \) 是控制运动模糊强度的可调因子。缩放后的屏幕空间速度 V' 由以下公式给出：

(17.6) \( \mathbf{V}' = \frac{s}{r_{\max}} \mathbf{V} \).

应用此缩放因子后，我们使用以下公式将速度的大小限制在 [0,1] 范围内，以保持其方向：

(17.7)
$$ \mathbf{V}_{final} = \frac{\mathbf{V}'}{\max \{|V'_x|, |V'_y|, 1\}}. $$

速度 V_final 的 x 和 y 分量存储在输出到速度缓冲区的颜色的红色和绿色通道中。

剩下的工作是将深度和梯度信息写入速度缓冲区的蓝色和 alpha 通道。线性相机空间深度由当前帧位置的 w 坐标提供，并直接复制到输出颜色的蓝色通道。为了获取深度梯度，我们向硬件查询位置 w 坐标在 x 和 y 屏幕方向上的导数。为了获得略高的性能，我们在 alpha 通道中输出两个导数中较大的绝对值，而不是计算梯度的实际大小。（也就是说，我们计算的是最大范数而不是欧几里得范数。）在清单 17.2 所示的片元着色器中，存储在 alpha 通道中的梯度大小 g 由以下公式给出：

(17.8) \( g = \max \left\{ \left| \frac{\partial z}{\partial x} \right|, \left| \frac{\partial z}{\partial y} \right| \right\} \).

## 17.3 渲染后处理效果

在帧结束时，通过在整个屏幕上渲染后处理着色器来为最终图像生成运动模糊效果。该着色器使用速度-深度-梯度缓冲区中的信息来选择一组采样位置，从中读取颜色缓冲区。所有满足最小深度要求的颜色样本都会被平均，以生成每个像素的最终颜色。由于采样位置源自像素所具有的速度的大小和方向，结果是一张包含逼真运动模糊的图像。

清单 17.3 所示的片元着色器执行运动模糊操作。它首先在正在渲染的像素位置（我们称之为“中心像素”）对颜色缓冲区进行采样，并将有效样本数初始化为一。有效样本数存储在颜色的 w 分量中，中心像素处的样本始终有效。这个特定的实现从颜色缓冲区沿速度平行方向以等间距取样八个额外等权重样本。在选择样本数量及其权重方面有一定的自由度，有些实现甚至可能根据速度的大小决定采取可变数量的颜色样本。

清单 17.3：这个 GLSL 片元着色器在后处理通道中应用运动模糊效果。九个颜色样本累积在颜色向量的 x、y 和 z 分量中，有效样本数存储在颜色向量的 w 分量中。minDepth 的值使用公式 (17.9) 计算，只有深度至少距离相机平面这么远的样本才用于生成最终模糊像素。

```
#extension GL_ARB_texture_rectangle : require

uniform sampler2DRect           colorTexture;
uniform sampler2DRect           velocityTexture;

void main()
{
   vec4       color, sample;

// Read the center sample from the color buffer.
color.xyz = texRECT(colorTexture, gl_FragCoord.xy);
color.w = 1.0;

// Read the velocity buffer at the current pixel
float4 velo = texRECT(velocityTexture, gl_FragCoord.xy);

// Calculate the minimum depth for other color samples
float minDepth = velo.z - max(velo.w, 0.001) * 7.0;

// Initialize constant sample weight.
sample.w = 1.0;

// Calculate coordinates for first sample on either side
vec4 coord = velo.xyxy * vec4(1.75, 1.75, -1.75, -1.75) + gl_FragCoord.xyxy;

// Read a color and depth at the sample location
sample.xyz = texRECT(colorTexture, coord.xy).xyz;
float depth = texRECT(velocityTexture, coord.xy).z;

// Add the sample to the final color if it's deep enough
if (depth >= minDepth) color += sample;

// Grab the sample on the opposite side of the center pixel
sample.xyz = texRECT(colorTexture, coord.zw).xyz;
depth = texRECT(velocityTexture, coord.zw).z;
if (depth >= minDepth) color += sample;
}
```
