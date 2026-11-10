
```cpp
sum = 256.0 * logistic(sum - cloudQuant);
return sum;
}

double logistic(double x) {
    double k = 0.2; // tunable laziness of clouds, smaller values are more hazy
    return (1.0 / (1.0 + pow(2.718, -k*x)));
}
```

logistic 函数会使颜色更趋向白色或蓝色，而不是介于两者之间的值，从而产生云边界更清晰的视觉效果。变量 cloudQuant 调整噪声图中白色（相对于蓝色）的相对数量，这反过来会在应用 logistic 函数时导致生成更多（或更少）的白色区域（即清晰的云朵）。最终得到的天空穹顶现在具有更清晰的云层形态，如图 14.22 所示。

![](img/1695de1bc7486362f86c143285f3fb40_364_0.png)

最后，真实的云并不是静止的。为了增强云的逼真感，我们应该让云动起来：（a）让它们随时间移动或漂移；（b）让它们在漂移时逐渐改变形状。

让云漂移的一种简单方法是缓慢旋转天空穹顶。这并不是一个完美的方案，因为真实的云往往沿直线方向漂移，而不是围绕观察者旋转。不过，如果旋转速度很慢，并且云只是用于装饰场景，那么这种效果可能就足够了。

让云在漂移时逐渐改变形状看似棘手。然而，鉴于我们已经使用三维噪声图来为云添加纹理，实际上有一种非常简单而巧妙的方法可以实现该效果。回想一下，虽然我们为云构建了三维纹理噪声图，但到目前为止只使用了其中一个“切片”，并结合天空穹顶的二维纹理坐标（我们将纹理查找的“Z”坐标设为常量值）。三维纹理的其余部分迄今尚未使用。

我们的技巧是：将纹理查找中的常量“Z”坐标替换为一个随时间逐渐变化的变量。也就是说，当我们旋转天空穹顶时，逐渐增加深度变量，使纹理查找使用不同的切片。回想一下，在构建三维纹理图时，我们沿三个轴对颜色变化进行了平滑处理。因此，纹理图中相邻的切片非常相似，但略有不同。这样，通过逐渐改变 texture() 调用中的“Z”值，云的外观就会逐渐变化。

使云随时间缓慢移动和变化的代码修改如程序14.8所示。

### 程序 14.8 为云纹理添加动画

*C++ / OpenGL 应用程序：*

```cpp
...
double prevTime = 0.0;
double rotAmt = 0.0;             // Y-axis rotation amount to make clouds appear to drift
float depth = 0.01f;             // depth lookup for 3D noise map, to make clouds gradually change
...
void display(GLFWwindow* window, double currentTime) {
    ...
    // gradually rotate the skydome
    mMat = glm::translate(glm::mat4(1.0f), glm::vec3(domeLocX, domeLocY, domeLocZ));
    rotAmt += (float) ((currentTime - prevTime) * 0.1);
    mMat = glm::rotate(mMat, rotAmt, glm::vec3(0.0f, 1.0f, 0.0f));
    ...
    // gradually alter the third texture coordinate to make clouds change
    dOffsetLoc = glGetUniformLocation(program, "d");
    depth += (float)((currentTime - prevTime) * 0.003f);
    if (depth >= 0.99f) depth = 0.01f;    // wrap-around when we get to the end of the texture map
    glUniform1f(dOffsetLoc, depth);
    ...
}
```

片段着色器：

```glsl
#version 430

in vec2 tc;
out vec4 fragColor;

uniform mat4 mv_matrix;
uniform mat4 proj_matrix;
uniform float d;

layout (binding=0) uniform sampler3D s;

void main(void)
{
    fragColor = texture(s, vec3(tc.x, tc.y, d));    // gradually-changing "d" replaces previous constant
}
```

虽然我们无法在单张静态图像中展示云逐渐漂移和动画变化的效果，但图14.23通过一系列快照展示了三维生成的云在从右向左飘过天空穹顶、并在漂移过程中缓慢改变形状时的此类变化。

![](img/1695de1bc7486362f86c143285f3fb40_366_0.png)

**图 14.23**
三维云在漂移过程中发生变化。

## 14.9 噪声应用——特殊效果

噪声纹理可用于各种特殊效果。事实上，其用途如此之多，适用性仅受人的想象力限制。

我们将在这里演示的一种非常简单的特殊效果是溶解效果。在这种效果中，我们让一个物体看起来逐渐分解成小颗粒，直到最终消失。给定三维噪声纹理，只需很少的额外代码就能实现该效果。

为实现溶解效果，我们引入 GLSL 的 discard 命令。该命令仅在片段着色器中合法；执行时，它会使片段着色器丢弃当前片段（即不渲染它）。

我们的策略很简单。在 C++/OpenGL 应用程序中，我们创建一个细粒度噪声纹理图，与前面图14.12所示相同，并创建一个随时间逐渐增大的浮点变量计数器。然后通过 uniform 变量将该变量传入着色器管线，同时将噪声图放入带有相关采样器的纹理图。片段着色器随后使用采样器访问噪声纹理——在此情况下，我们使用返回的噪声值决定是否丢弃片段。我们通过将灰度噪声值与计数器比较来实现这一点，计数器充当一种“阈值”。由于阈值随时间逐渐变化，我们可以设置成逐渐丢弃越来越多的片段。结果是物体看起来逐渐溶解。程序14.9展示了相关代码段，这些代码段被添加到程序6.1中渲染地球的球体上。生成结果如图14.24所示。

### 程序 14.9 使用 discard 命令的溶解效果

*C++ / OpenGL 应用程序：*

```cpp
float threshold = 0.0f;          // gradually-increasing threshold for retaining/discarding fragment
...
```

*在 display 中：*

```cpp
...
Loc = glGetUniformLocation(renderingProgram, "t");
threshold = (float) currentTime * 0.1f;
glUniform1f(Loc, threshold);
...
glActiveTexture(GL_TEXTURE0);
glBindTexture(GL_TEXTURE_3D, noiseTexture);
glActiveTexture(GL_TEXTURE1);
glBindTexture(GL_TEXTURE_2D, earthTexture);
...
glDrawArrays(GL_TRIANGLES, 0, numSphereVertices);
```

片段着色器：

```glsl
#version 430
in vec2 tc;              // texture coordinates for this fragment
in vec3 origPos;          // original vertex positions in the model, for accessing 3D texture
...
layout (binding=0) uniform sampler3D n;       // sampler for noise texture
layout (binding=1) uniform sampler2D e;       // sampler for earth texture
...
uniform float t;          // threshold for retaining or discarding fragment

void main(void)
{
    float noise = texture(n, origPos).x;      // retrieve noise value for this fragment.
    if (noise > t)                           // if the noise value > current threshold value,
    {   fragColor = texture(e, tc);           // render the fragment using the earth texture.
    }
    else
    {   discard;       // otherwise, discard the fragment (do not render it)
    }
}
```

![](img/1695de1bc7486362f86c143285f3fb40_368_0.png)

**图 14.24**
使用 discard 着色器的溶解效果。

## 练习

- 14.1 修改程序14.2，使物体的 alpha 值逐渐减小，从而使其逐渐淡出并最终消失。

- 14.2 修改程序14.3，沿水平方向裁剪圆环，形成一个圆形“槽”。

- 14.3 修改程序14.4（包含图14.10中生成三维立方纹理的修改版本），使其改为为 Studio 522 海豚添加纹理。然后观察结果。许多人首次观察结果时（例如龙身上显示的结果，甚至更简单物体上的结果），会认为程序存在某种错误。即使简单情况下，从三维纹理中“雕刻”物体也可能产生意外的表面图案。

- 14.4 用于定义木材“年轮”的简单正弦波（如图14.18所示）生成的环中，亮区和暗区宽度相等。尝试修改相关的 fillDataArray() 函数，目标是使暗环比亮环更窄。然后观察对最终木纹物体效果的影响。

- 14.5（项目）将（程序14.7中的）logistic 函数融入程序14.5的大理石龙中，并试验不同设置以创建更清晰的纹理脉络。

- 14.6 修改程序14.9，纳入前面各节描述的缩放、平滑、湍流和 logistic 步骤。观察所得溶解效果的变化。

## 参考文献

- [AF14] S. Abraham 和 D. Fussell，《Smoke Brush》，*Proceedings of the Workshop on Non-Photorealistic Animation and Rendering (NPAR’14)*，2014，2020年7月访问，https://www.cs.utexas.edu/~theshark/smokebrush.pdf。

- [AS04] D. Astle，《Simple Clouds Part 1》，gamedev.net，2004（Francis Huang 编写的教程），2020年7月访问，http://www.gamedev.net/page/resources/_/technical/game-programming/simple-clouds-part-1-r2085。
