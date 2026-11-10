
### 顶点着色器：

```glsl
...
uniform mat4 texRot_matrix;
void main(void)
{
    ...
    originalPosition = vec3(texRot_matrix * vec4(position,1.0)).xyz;
    ...
}
```

### 片段着色器：

```glsl
...
void main(void)
{
    ...
    uniform mat4 texRot_matrix;
    ...
    // combine lighting with 3D texturing
    fragColor =
        0.5 * (...)
        +
        0.5 * texture(s,originalPosition / 2.0 + 0.5);
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_363_0.png)

**图 14.20**
使用“wood”3D 噪声贴图添加纹理的海豚。

最终得到的带 3D 纹理的木纹海豚如图 14.20 所示。片段着色器中还有一个值得注意的额外细节。由于我们在 3D 纹理中旋转模型，有时这种旋转会导致顶点位置超出纹理坐标通常的 [0..1] 范围。如果发生这种情况，我们可以通过将原始顶点位置除以一个更大的数（例如用 4.0 而不是 2.0），然后再加上一个稍大的数（例如 0.6）使其在纹理空间中居中，来针对这种可能性进行调整。由于我们的噪声贴图会环绕，超出 [0..1] 范围的顶点坐标不会造成问题。

## 14.8 噪声应用——*云*

前面在图 14.15 中构建的“湍流”噪声贴图已经看起来有点像云了。当然，它的颜色并不合适，因此我们首先把它从灰度改为浅蓝色和白色的适当混合。一种直接的方法是：根据噪声贴图中的值，为蓝色分量分配最大值为 1.0 的颜色，并为红色和绿色分量分配在 0.0 到 1.0 之间变化（但彼此相等）的值。新的 fillDataArray() 函数如下：

```java
private void fillDataArray(byte data[])
{
    double maxZoom = 32.0;
    for (int i=0; i<noiseWidth; i++)
    {
        for (int j=0; j<noiseHeight; j++)
        {
            for (int k=0; k<noiseDepth; k++)
            {
                float brightness = 1.0f - (float)(turbulence[i, j, k, maxZoom]) / 256.0f;
                Color c = new Color(brightness, brightness, 1.0f, 1.0f);
                data[i*(noiseWidth*noiseHeight*4)+j*(noiseHeight*4)+k*4+0] = (byte) c.getRed();
                data[i*(noiseWidth*noiseHeight*4)+j*(noiseHeight*4)+k*4+1] = (byte) c.getGreen();
                data[i*(noiseWidth*noiseHeight*4)+j*(noiseHeight*4)+k*4+2] = (byte) c.getBlue();
                data[i*(noiseWidth*noiseHeight*4)+j*(noiseHeight*4)+k*4+3] = (byte) 255;
            }
        }
    }
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_364_0.png)

得到的蓝色版噪声贴图现在可用于给天空穹顶添加纹理。回想一下，天空穹顶是一个球体或半球体，它带有纹理、在禁用深度测试的情况下渲染，并被放置为包围相机（类似于天空盒）。

构建天空穹顶的一种方式是像处理其他 3D 纹理那样，使用顶点坐标作为纹理坐标来给它添加纹理。然而，在这种情况下，改用天空穹顶的 2D 纹理坐标反而会生成更像云的图案，因为球面畸变会稍微水平拉伸纹理贴图。我们可以通过将 GLSL texture() 调用中的第三维设置为常量值，从噪声贴图中获取一个 2D 切片。假设天空穹顶的纹理坐标具有

```java
private double logistic(double x)
{ double k = 0.2;        // tunable haziness of clouds, smaller values are more hazy
  return (1.0 / (1.0 + Math.pow(2.718, -k*x)));
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_366_0.png)

**图 14.22**
带有指数云纹理的天空穹顶。

logistic 函数使颜色更倾向于白色或蓝色，而不是介于两者之间的值，从而产生云层边界更分明的视觉效果。变量 cloudQuant 调整噪声贴图中白色（相对于蓝色）的相对量，进而在应用 logistic 函数时生成更多（或更少）白色区域（即明显的云）。

最终得到的天空穹顶现在具有更明显的云层形态，如图 14.22 所示。

最后，真实的云并非静止不动。为了增强云的真实感，我们应该让它们动起来：(a) 使它们随时间移动或“漂移”，以及 (b) 在漂移时逐渐改变其形态。

让云“漂移”的一种简单方法是缓慢旋转天空穹顶。这并不是完美的解决方案，因为真实的云倾向于沿直线方向漂移，而不是围绕观察者旋转。不过，如果旋转很慢，而且云只是用于装饰场景，那么这种效果可能就足够了。

让云在漂移时逐渐改变形态，乍看之下可能很棘手。然而，鉴于我们已使用 3D 噪声贴图来给云添加纹理，实际上有一种非常简单而巧妙的方法来实现这种效果。回想一下，尽管我们为云构建了 3D 纹理噪声贴图，但到目前为止只使用了其中一个“切片”，并结合天空穹顶的 2D 纹理坐标（我们将纹理查找的“Z”坐标设置为常量值）。3D 纹理的其余部分到目前为止一直未被使用。

我们的技巧是用一个随时间逐渐变化的变量替换纹理查找中的常量“Z”坐标。也就是说，当我们旋转天空穹顶时，逐渐递增深度变量，使纹理查找使用不同的切片。回想一下，当我们构建 3D 纹理贴图时，我们对

```glsl
layout(binding=0) uniform sampler3D s;
void main(void)
{ fragColor = texture(s, vec3(tc.x, tc.y, 0));    // gradually-changing "d" replaces previous constant
}
```

随附 CD 上的完整实现还包括对 turbulence() 函数的一些额外细微修改，以增强云的漂移效果。虽然我们无法在单张静态图像中展示逐渐变化、漂移且动态的云的效果，但图 14.23 通过一系列快照展示了这种变化：3D 生成的云从右向左飘过天空穹顶，并在漂移时缓慢改变形状。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_368_0.png)

**图 14.23**
漂移时不断变化的 3D 云。

## 14.9 噪声应用——*特殊效果*

噪声纹理可用于各种特殊效果。事实上，其可能用途如此之多，以至于它的适用性只受想象力的限制。

我们将在此演示的一个非常简单的特殊效果是*溶解效果*。在这种效果中，我们让一个物体看起来逐渐溶解成小颗粒，直到最终消失。给定 3D 噪声纹理，只需很少的额外代码即可实现这种效果。

为了方便实现溶解效果，我们引入 GLSL discard 命令。该命令仅在片段着色器中合法；执行时，它会使片段着色器丢弃当前片段（即不渲染它）。

我们的策略很简单。在 Java/JOGL 应用程序中，我们创建一个细粒度噪声纹理贴图，与前面图 14.12 所示的贴图相同，并创建一个随时间逐渐递增的 float 变量 counter。然后，该变量通过 uniform 变量传入着色器管线，噪声贴图也被放入带有相关采样器的纹理贴图中。随后，片段着色器使用采样器访问噪声纹理——在这种情况下，我们使用返回的噪声值来决定是否丢弃该片段。我们通过将灰度噪声值与 counter 进行比较来实现这一点，counter 充当一种“阈值”值。由于阈值随时间逐渐变化，我们可以这样设置，使得越来越多的片段被逐渐丢弃。结果是物体看起来逐渐溶解。程序 14.9 展示了相关代码段，这些代码段被添加到程序 6.1 中渲染地球的球体上。生成的输出如图 14.24 所示。

### 程序 14.9 使用 discard 命令的溶解效果

*Java / JOGL 应用程序：*

```java
float threshold = 0.0f;    // gradually-increasing threshold for retaining/discarding fragment
```

```java
in display():
…
glC = gl.glGetUniformLocation(renderingProgram, "...");
threshold += (System.currentTimeMillis() - prevTime) * 0.0001f;
prevTime = System.currentTimeMillis();
…
gl.glActiveTexture(GL_TEXTURE0);
```
