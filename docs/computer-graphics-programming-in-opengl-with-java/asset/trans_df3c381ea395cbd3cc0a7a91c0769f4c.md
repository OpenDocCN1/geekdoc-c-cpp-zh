
当我们已经有全局环境光时，再为某个光源加入环境光贡献，似乎显得多余。然而，将两者分开是有意为之的，并且当光源“开启”或“关闭”时这种区分会很明显。当处于“开启”状态时，总环境光贡献会如预期那样增加。在上面的示例中，我们只为该光源加入了很小的环境光贡献。重要的是根据场景的需要平衡这两种贡献。

*位置*光源在 3D 场景中具有特定位置。靠近场景的光源，例如台灯、蜡烛等，就是例子。与定向光一样，位置光源的效果取决于入射角；但是，它的方向并未指定，因为在我们场景中每个顶点的方向都不同。位置光源还可以包含*衰减因子*，以模拟其强度如何随距离而减弱。与我们见过的其他类型光源一样，位置光源具有以 RGBA 值指定的环境光、漫反射和高光属性。例如，位于 (5,2,-3) 的红色位置光源可以按如下方式指定：

```java
float[] posLightAmbient = new float[] { 0.1f, 0.0f, 0.0f, 1.0f };
float[] posLightDiffuse = new float[] { 1.0f, 0.0f, 0.0f, 1.0f };
float[] posLightSpecular = new float[] { 1.0f, 0.0f, 0.0f, 1.0f };
float[] posLightLocation = new float[] { 5.0f, 2.0f, -3.0f };
```

衰减因子可以通过多种方式建模。一种方式是为*常量*、*线性*和*二次*衰减分别包含可调的非负参数（分别为 \(k_c\)、\(k_l\) 和 \(k_q\)）。然后结合这些参数，并考虑距光源的距离（\(d\)）：

$$\text{attenuationFactor} = \frac{1}{k_c + k_l d + k_q d^2}$$

将此因子乘以光强，会使距离光源越远的光强越低。请注意，\(k_c\) 应始终设置为大于或等于 1.0，并且其他参数中至少有一个大于 0.0，这样衰减因子将始终处于 [0..1] 范围内，并随着距离 \(d\) 的增加而趋近于 0。

*聚光灯*同时具有位置和方向。聚光灯“锥形”的效果可以通过 0° 到 90° 之间的*截止角*（指定光束的半宽）以及*衰减指数*（模拟强度随光束角度变化的情况）来模拟。如图 7.2 所示，我们确定聚光灯方向与从聚光灯指向像素的向量之间的角度 ϕ。然后，当 ϕ 小于 θ 时，我们通过将 ϕ 的余弦提高到衰减指数来计算*强度因子*（当 ϕ 大于 θ 时，强度因子设为 0）。结果是一个范围从 0 到 1 的强度因子。衰减指数调整强度因子随着角度 ϕ 增大而趋于 0 的速率。然后，将强度因子乘以光源强度，以模拟锥形效果。

位于 (5,2,-3)、指向负 Z 轴的红色聚光灯可以按如下方式指定：

```java
float[] spotLightAmbient = new float[] { 0.1f, 0.0f, 0.0f, 1.0f};
float[] spotLightDiffuse = new float[] { 1.0f, 0.0f, 0.0f, 1.0f};
float[] spotLightSpecular = new float[] { 1.0f,0.0f, 0.0f, 1.0f};
float[] spotLightLocation = new float[] { 5.0f, 2.0f, -3.0f };
float[] spotLightDirection = new float[] { 0.0f, 0.0f, -1.0f };
float spotLightCutoff = 20.0f;
float spotLightExponent = 10.0f;
```

聚光灯也可以包含衰减因子。我们在上述设置中没有展示它们，但可以按照前面针对位置光源所述的方式定义它们。

从历史上看，自从皮克斯广受欢迎的动画短片*《小台灯》*于 1986 年问世以来，聚光灯在计算机图形学中一直具有标志性地位 [D12]。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_185_0.png)

**图 7.2**
聚光灯组件。

在设计包含多种光源的系统时，程序员应考虑创建类层次结构，例如定义一个“Light”类，以及“Global Ambient”“Directional”“Positional”和“Spotlight”子类。由于聚光灯同时具有定向光和位置光的特征，而且 Java 缺少多重继承，因此在确定类层次结构时可能会有些棘手。在本书的上一版中，我们使用了一个名为 graphicslib3D 的库，其中包含针对每种光源类型的容器类，其中 SpotLight 是 PositionalLight 的子类。我们的示例足够简单，因此本版中省略了为光照构建这样的类层次结构。

## 7.3 材质

到目前为止，我们场景中对象的“外观”一直仅通过颜色和纹理来处理。加入光照后，我们还可以考虑表面的反射特性。我们指的是对象如何与我们的 ADS 光照模型相互作用。这可以通过将每个对象视为由某种材质“制成”来建模。

在 ADS 光照模型中，可以通过指定四个值来模拟材质，其中三个值我们已经熟悉——环境光、漫反射和高光 RGB 颜色。第四个值称为光泽度；正如我们将看到的，它用于为预期材质构建合适的高光反射。人们已经为许多不同类型的常见材质开发了 ADS 和光泽度值。例如，“白镴”可以按如下方式指定：

```java
float[] pewterMatAmbient = new float[] { .11f, .06f, .11f, 1.0f }; 
float[] pewterMatDiffuse = new float[] { .43f, .47f, .54f, 1.0f }; 
float[] pewterMatSpecular = new float[] { .33f, .33f, .52f, 1.0f }; 
float pewterMatShininess = 9.85f;
```

其他一些材质的 ADS RGBA 值在图 7.3 中给出（来自 [BA16]）。

有时，材质属性中还会包含其他属性。透明度通过 RGBA 规范中的第四个（或“alpha”）通道处理，该通道指定不透明度；值 1.0 表示完全不透明，0.0 表示完全透明。对于大多数材质，它通常被简单地设为 1.0，不过对于某些材质，轻微透明度会起作用。例如，在图 7.3 中，请注意“翡翠”和“珍珠”材质包含少量透明度（值略小于 1.0），以增加真实感。

自发光有时也会包含在 ADS 材质规范中。这在模拟自身发光的材质（例如磷光材质）时很有用。

| 材质 | 环境光 RGBA<br>漫反射 RGBA<br>高光 RGBA | 光泽度 |
| --- | --- | --- |
| 金 | 0.2473, 0.1995, 0.0745, 1.0<br>0.7516, 0.6065, 0.2265, 1.0<br>0.6283, 0.5558, 0.3661, 1.0 | 51.200 |
| 翡翠 | 0.1350, 0.2225, 0.1575, 0.95<br>0.5400, 0.8900, 0.6300, 0.95<br>0.3162, 0.3162, 0.3162, 0.95 | 12.800 |
| 珍珠 | 0.2500, 0.2073, 0.2073, 0.922<br>1.0000, 0.8290, 0.8290, 0.922<br>0.2966, 0.2966, 0.2966, 0.922 | 11.264 |
| 银 | 0.1923, 0.1923, 0.1923, 1.0<br>0.5075, 0.5075, 0.5075, 1.0<br>0.5083, 0.5083, 0.5083, 1.0 | 51.200 |

**图 7.3**
材质 ADS 与光泽度系数。

当渲染一个没有纹理的对象时，通常希望指定材质特征。因此，准备一些预定义材质会非常方便。于是，我们在“Utils.java”工具程序中添加以下几行代码：

```java
// GOLD material - ambient, diffuse, specular, and shininess
public static float[] goldAmbient() { return new float[] { 0.2473f, 0.1995f, 0.0745f, 1 }; }
public static float[] goldDiffuse() { return new float[] { 0.7516f, 0.6065f, 0.2265f, 1 }; }
public static float[] goldSpecular() { return new float[] { 0.6283f, 0.5558f, 0.3661f, 1 }; }
public static float goldShininess() { return 51.2f; }

// SILVER material - ambient, diffuse, specular, and shininess
public static float[] silverAmbient() { return new float[] { 0.1923f, 0.1923f, 0.1923f, 1 }; }
public static float[] silverDiffuse() { return new float[] { 0.5075f, 0.5075f, 0.5075f, 1 }; }
public static float[] silverSpecular() { return new float[] { 0.5083f, 0.5083f, 0.5083f, 1 }; }
public static float silverShininess() { return 51.2f; }

// BRONZE material - ambient, diffuse, specular, and shininess
public static float[] bronzeAmbient() { return new float[] { 0.2125f, 0.1275f, 0.0540f, 1 }; }
public static float[] bronzeDiffuse() { return new float[] { 0.7140f, 0.4284f, 0.1814f, 1 }; }
public static float[] bronzeSpecular() { return new float[] { 0.3935f, 0.2719f, 0.1667f, 1 }; }
public static float bronzeShininess() { return 25.6f; }
```
