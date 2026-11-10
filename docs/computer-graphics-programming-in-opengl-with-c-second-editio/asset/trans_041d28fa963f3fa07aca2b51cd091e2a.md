

### 程序 15.6——添加“雾”和“菲涅尔”效果

*片段着色器（用于顶面）*

```glsl
...
void main(void)
{ // code for determining amount of fog to add - very similar to Section 14.1
  vec4 fogColor = vec4(0.0, 0.0, 0.2, 1.0);
  float fogStart = 10.0;
  float fogEnd = 300.0;
  float dist = length(varyingVertPos.xyz);
  float fogFactor = clamp((fogEnd-dist) / (fogEnd-fogStart), 0.0, 1.0);

...

  // angle between normal vector and view vector (for Fresnel effect)
  vec3 Nfres = normalize(varyingNormal);
  float cosFres = dot(v, Nfres);
  float fresnel = acos(cosFres);
  fresnel = pow(clamp(fresnel-0.3, 0.0, 1.0), 3);  // tuning for this particular application

  if (isAbove == 1)
  { // if above the surface, compute reflection and refraction contributions separately, then mix
    refractColor = texture(refractTex, (vec2(gl_FragCoord.x, gl_FragCoord.y))/(2.0*gl_FragCoord.w)+0.5);
    reflectColor = texture(reflectTex, (vec2(gl_FragCoord.x, gl_FragCoord.y))/(2.0*gl_FragCoord.w)+0.5);
    reflectColor = vec4((reflectColor.xyz * (ambient + diffuse) + 0.75*specular), 1.0);
    color = mix(refractColor, reflectColor, fresnel);
  }
  else
  { // if below the surface, compute only the refractive contribution, and add fog
    refractColor = texture(refractTex, (vec2(gl_FragCoord.x, gl_FragCoord.y))/(2.0*gl_FragCoord.w)+0.5);
    mixColor = (0.5 * blueColor) + (0.6 * refractColor);
    color = vec4((mixColor.xyz * (ambient + diffuse) + 0.75*specular), 1.0);
    color = mix(fogColor, color, pow(fogFactor,5));
  }
}
```

*片段着色器（用于地面）*

```glsl
...
void main(void)
{ // code for determining amount of fog to add - very similar to Section 14.1
  vec4 fogColor = vec4(0.0, 0.0, 0.2, 1.0);
  float fogStart = 10.0;
  float fogEnd = 300.0;
  float dist = length(varyingVertPos.xyz);
  float fogFactor = clamp((fogEnd-dist) / (fogEnd-fogStart), 0.0, 1.0);
  ...
  if (isAbove == 1) color = mix(fogColor, color, pow(fogFactor,5.0));
}
```

![](img/1695de1bc7486362f86c143285f3fb40_396_0.png)

**图 15.8**
菲涅尔效果（左，水面上方）和雾效果（右，水面下方）

## 15.5 为水面运动添加动画

为水面添加动画可以采用与云层类似的方式，即利用噪声图中第三维（目前尚未使用）来实现。回顾第 14.8 节中的技巧：将第三维中用于纹理查找的常量替换为一个随时间变化的变量。随着检索到的噪声图“切片”发生变化，噪声细节也会改变。我们在这里可以使用同样的技巧：在查找要应用的噪声图“切片”时，随时间调整沿第三轴的位置，从而移动正弦波。

该修改见程序 15.7。尽管我们无法在此充分展示动画效果，但图 15.9 给出了一些帧，展示了水面和光照随时间的变化，分别从水面上方和水面下方观察。（或者，要查看实际运动效果，请运行随附文件中的代码。）

### 程序 15.7——为水面添加动画

C++/OpenGL 应用程序

```cpp
...
float depthLookup = 0.0f;
GLuint dOffsetLoc;

double turbulence(double x, double y, double z, double maxZoom) {
    double sum = 0.0, zoom = maxZoom;
    sum = sin((1.0/512.0)*(PI*x*z*4.0)) + 1.0;  //this change moves the sine wave through the noise map
    ...
}

void prepForTopSurfaceRenderer() {
    ...
    dOffsetLoc = glGetUniformLocation(renderingProgramSURFACE, "depthOffset");
    glUniform1f(dOffsetLoc, depthLookup);
    ...
}

void prepForFloorRenderer() {
    ...
    dOffsetLoc = glGetUniformLocation(renderingProgramFLOOR, "depthOffset");
    glUniform1f(dOffsetLoc, depthLookup);
    ...
}

void display(GLFWwindow* window, double currentTime) {
    depthLookup += (currentTime - prevTime) * 0.05f;
    prevTime = currentTime;    // prevTime is a global variable initialized to glfwGetTime() in init()
    ...
}
```

*顶点着色器（用于顶面及地面）*

```glsl
...
uniform float depthOffset;
...
```

*片段着色器（用于顶面及地面）*

```glsl
...
uniform float depthOffset;
vec3 estimateWaveNormal(float offset, float mapScale, float hScale)
{
    ...
}

void main(void)
{
    . . .
    color = vec4((mixColor * (ambient + diffuse) + specular), 1.0);

    //add caustics
    if (isAbove >= 1)
    {
        float causticColor = getCausticValue(tc.s, depthOffset, tc.t);
        float colorR = clamp(color.r + causticColor, 0.0, 1.0);
        float colorG = clamp(color.g + causticColor, 0.0, 1.0);
        float colorB = clamp(color.b + causticColor, 0.0, 1.0);
        color = vec4(colorR, colorG, colorB, 1.0);
    }

    // add fog
    if (isAbove >= 1) color = mix(fogColor, color, pow(fogFactor,5.0));
}
```

![](img/1695de1bc7486362f86c143285f3fb40_400_0.png)

**图 15.10**
相机位于水面下方时添加的焦散效果

## 补充说明

在实时图形应用程序中模拟水是一个复杂的主题，而我们只是触及了表面。我们也只关注了一种类型的水。要模拟从花园软管中喷出的水或酒杯中飞溅的葡萄酒，则需要完全不同的技术。

甚至我们对游泳池或湖面的模拟也是有限的。例如，使用所述方法只能在水面上产生小波纹。更大的波浪需要修改表面几何形状。一种实现方式是使用细分阶段增加顶点数量，然后使用高度映射根据噪声图中的值移动这些顶点。

我们对地面可见扭曲的模拟存在一个根本性的不准确之处：它们基于对应地面位置正上方表面位置的噪声值。实际上，给定地面位置的扭曲应基于相机与该地面位置之间表面位置的噪声值。不过，这不太可能对感知到的真实感产生影响。在我们的实现中，有许多这样的简化。

“Fresnel”读作“Fre-nel”——其中的“s”不发音。

对于有兴趣更深入研究模拟水和其他流体主题的读者，有大量论文和资源。甚至还有关于该主题的整本书 [315]。

本章描述的技术紧密参考了 Chris Swenson 在加利福尼亚州立大学萨克拉门托分校学习期间作为特别项目一部分所实现的方法。他的贡献极大地促进了我们的讲解，我们感谢他出色的工作，生成了非常连贯的逐步方法。

## 练习

- 15.1 添加一个飞行物体，例如鸟或飞机（甚至 NASA 航天飞机模型）在水面顶面上方飞过。然后，当相机位于水面上方时，将其纳入水面顶面的反射中；当相机位于水面下方时，将其纳入穿过顶面的折射中。
- 15.2 在水面顶面下方添加一个水下移动的物体，例如鱼或潜艇（甚至 Studio 522 海豚）。然后，当相机位于顶面下方时，将其纳入场景中；当相机位于顶面上方时，将其纳入折射中。
- 15.3 在练习 15.2（上述）中，如果你尚未这样做，请为水下物体添加水面焦散效果。

## 第 16 章 光线追踪与计算着色器

- 16.1 计算着色器 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 385
- 16.2 光线投射 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 394
- 16.3 光线追踪 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 424
- 补充说明 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 456

![](img/1695de1bc7486362f86c143285f3fb40_403_0.png)

在本章中，我们研究一种用于创建高度逼真光照效果的方法，称为*光线追踪*。我们之前在第 7 章研究过光照，然后在第 9 章看到了一种模拟反射的简单方法，称为环境映射。然而，所有这些方法都只能部分模拟光照效果。例如，ADS 光照模型只考虑光源对表面的影响，而不考虑场景中物体之间反射光的影响。同样，环境映射仅限于模拟立方体贴图的反射，而不模拟邻近物体的反射。相比之下，光线追踪更贴近地模拟光在场景中的实际路径，考虑物体之间的反射、阴影，甚至穿过透明物体的折射。光线追踪能够生成高度详细且照片级真实的效果，尽管它需要大量计算资源，并且并不总是能够实时完成。

光线追踪源于一个简单的想法：如果我们能够追踪光线从光源到我们眼睛的路径，就能忠实再现我们所看到的内容。然而，在实践中这是不可行的——光线实在太多，其中大多数甚至最终不会到达我们的眼睛（或者对我们所感知的内容只有边际影响）。

一个非常巧妙的替代方案是反转这一想法。我们不是从光源向眼睛追踪光线，而是从眼睛开始追踪光线，让它们在场景中的物体上“反弹”若干次，累积并组合

