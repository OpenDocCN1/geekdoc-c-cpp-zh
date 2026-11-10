

```glsl
reflectColor = vec4((reflectColor.xyz * (ambient + diffuse) + 0.75 * specular), 1.0);
color = mix(refractColor, reflectColor, fresnel);
}
else
{
    // if below the surface, compute only the refractive contribution, and add fog
    refractColor = texture(refractTex, (vec2(gl_P...gl_P...) / (2.0 * gl.w) + 0.5));
    mixColor = (0.5 * blueColor) + (0.6 * refractColor);
    color = vec4((mixColor.xyz * (ambient + diffuse) + 0.75 * specular), 1.0);
    color = mix(fogColor, color, pow(fogFactor, 5.0));
}
```

### 片段着色器（用于地板平面）

```glsl
...
void main(void)
{
    // code for determining amount of fog to add – very similar to Section 14.1
    vec4 fogColor = vec4(0.0, 0.0, 0.2, 1.0);
    float fogStart = 10.0;
    float fogEnd = 300.0;
    float dist = length(varyingVertPos.xyz);
    float fogFactor = clamp((fogEnd - dist) / (fogEnd - fogStart), 0.0, 1.0);
    ...
    if (isAbove != 1) color = mix(fogColor, color, pow(fogFactor, 5.0));
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_398_0.png)

**图 15.8**  
菲涅耳效应（左图，位于水面之上）和雾效（右图，位于水面之下）。

## 15.5 为水面运动添加动画

为水面添加动画可以采用与云朵类似的方式，利用噪声图中的第三维（目前尚未使用）。回想第 14.8 节中的技巧：将第三维中的纹理查找常量替换为随时间变化的变量。随着检索到的噪声图“切片”发生变化，噪声细节也会变化。我们在这里可以使用同样的技巧，在查找要应用噪声图的哪个“切片”时，通过随时间调整沿第三轴的位置来移动正弦波。

这一修改在程序 15.7 中给出。虽然我们无法在此充分展示动画，但图 15.9 给出了一些帧，展示了表面和光照随时间的变化，分别从水面上方和水面下方观看。（或者，要查看实际运动，请运行随附磁盘上的代码。）

### 程序 15.7 为水面添加动画

Java/JOGL 应用程序

```java
…
private float depthLookup = 0.0f;
private int dOffsetLoc;

private double turbulence(double x, double y, double z, double maxZoom)
{
    double sum = 0.0, zoom = maxZoom;
    sum = sin((1.0/512.0)*(8*PI)*(x+z-4*y) + 1) * 8.0;
                      // this change moves the sine wave through the noise map
    …
}

private void prepForTopSurfaceRender() {
    …
    dOffsetLoc = gl.glGetUniformLocation(renderingProgram.SURFACE, "depthOffset");
    gl.glUniform1f(dOffsetLoc, depthLookup);
    …
}

private void prepForFloorRender()
{
    …
    dOffsetLoc = gl.glGetUniformLocation(renderingProgram.FLOOR, "depthOffset");
    gl.glUniform1f(dOffsetLoc, depthLookup);
    …
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_401_0.png)

**图 15.9** 水面之上和水面之下的水体效果动画。在上方三幅图中，相机位于水面顶部之上。在下方三幅图中，相机位于水面之下。

## 15.6 水下焦散

在水下地板上经常可以观察到弯曲的光带，因为来自水面上方的光会经由波浪表面的各种起伏透射到地板上。这些光带有时被称为*水焦散* [W19]，添加它们可以使水下场景更明显地呈现出水下效果。在本节中，我们只在相机位于水面之下时将它们添加到场景中（相机位于水面之上的情况见练习 15.4）。

模拟水焦散可以通过多种方式完成。使用光线追踪可以相当准确地实现它们，尽管这可能很复杂且计算开销很大 [G07]。然而，在大多数情况下，并不需要焦散完全准确，即使是粗略的模拟也足以传达水下效果。在大多数情况下，生成以与水面波浪一致的方式弯曲的白色线条就足够了。

我们可以直接在片段着色器中根据噪声图生成一种焦散图案，方法如下。首先计算噪声值的正弦；噪声值（范围为 0 到 1）先乘以 2π，使正弦值平滑循环。这会得到一个在 -1.0 和 1.0 之间循环的值。其绝对值在 0.0 和 1.0 之间循环，但在 0.0 附近斜率很陡，在 1.0 附近斜率较缓。然后从 1.0 中减去这个绝对值进行反转，从而在 0.0 附近产生长而平坦的区域，并在 1.0 附近产生尖峰。可以通过将其提升到一个可调指数来放大，使用名为 strength 的可调变量。结果是一个通常输出接近 0 的值、但偶尔会有输出值接近 1.0 的小区域的函数。当将其应用于给定世界坐标处的顶部表面颜色值时，它会生成跟随顶部表面波浪的周期性图案，然后我们可以将其合并到底部表面颜色中。程序 15.8 展示了添加到片段着色器中的这段代码，以及将计算得到的值添加到渲染到地板的颜色中的结果。输出如图 15.10 所示。

请注意，添加焦散后的地板颜色分量会被钳制到 [0..1] 范围，以确保它们处于 RGB 值的有效范围内。

### 程序 15.8 添加水下焦散

片段着色器（用于地板）

```glsl
...

float getCausticValue(float x, float y, float z)
{
    float w = 8;             // frequency of caustic curved bands
    float strength = 4.0;
    float PI = 3.14159;
    float noise = texture(noiseTex, vec3(x*w, y, z*w)).r;
    return pow((1.0-abs(sin(noise*2*PI))), strength);
}

void main(void)
{
    { ...
        color = vec4((mixColor * (ambient + diffuse) + specular), 1.0);

        // add caustics
        if (isAbove != 1)
        {
            float causticColor = getCausticValue(tc.s, depthOffset, tc.t);
            float colorR = clamp(color.x + causticColor, 0.0, 1.0);
            float colorG = clamp(color.y + causticColor, 0.0, 1.0);
```

相机和地板位置。不过，这不太可能对感知到的真实感产生影响。我们的实现中还有许多诸如此类的简化。

“Fresnel”读作“Fre-nel”——其中的“s”不发音。

对于有兴趣更深入地研究水和其他流体模拟主题的读者，有大量论文和资源可供参考。甚至还有关于该主题的整本书 [B15]。

本章描述的技术密切参照了 Chris Swenson 在加州州立大学萨克拉门托分校就读期间作为特别项目一部分所实现的一个方案。他的贡献极大地方便了我们的讲解，我们感谢他完成了出色的工作，形成了一套连贯且条理清晰的逐步方法。

## 练习

- 15.1 添加一个飞行的物体，例如一只鸟或一架飞机（甚至 NASA 航天飞机模型），让它在水面上方飞过。然后，当相机位于水面之上时，将其纳入水面顶部的反射中；当相机位于水面之下时，将其纳入穿过水面顶部的折射中。

- 15.2 添加一个在水下移动的物体，例如一条鱼或一艘潜艇（甚至 Studio 522 的海豚），位于水面顶部之下。然后，当相机位于水面顶部之下时，将其纳入场景中；当相机位于水面顶部之上时，将其纳入折射中。

- 15.3 在练习 15.2（上文）中，如果你还没有这样做，请为水下物体添加水焦散。

- 15.4 修改程序 15.8 中的片段着色器，使得当相机位于水面顶部*之上*时也能渲染水焦散。你认为在这种情况下包含焦散后，场景看起来更真实还是更不真实？如果是后者，请尝试找到一种调整焦散的方法，使其增强真实感而不是削弱真实感。

