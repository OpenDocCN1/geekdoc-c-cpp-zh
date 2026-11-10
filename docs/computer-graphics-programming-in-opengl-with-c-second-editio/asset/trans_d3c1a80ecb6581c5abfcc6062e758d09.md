

![](img/1695de1bc7486362f86c143285f3fb40_265_0.png)

**图10.4**  
法线映射示例。

图10.4展示了两个不同的法线贴图图像文件（两者都是由Luna [LU16]的纹理构建的），以及在Blinn-Phong光照下将它们应用于球体的结果。

从法线贴图中获取的法线向量不能直接使用，因为它们如前所述是相对于一个任意的X-Y平面定义的，没有考虑它们在物体上的位置以及在相机空间中的朝向。我们解决此问题的策略是构建一个变换矩阵，将法线转换到相机空间，如下所示。

在物体上的每个顶点，我们考虑一个与该物体相切的平面。该顶点处的物体法线垂直于这个平面。我们在这个平面中定义两个互相垂直且同样垂直于法线的向量，称为*切线*（tangent）和*副切线*（bitangent）（有时称为*次法线*（binormal））。构建我们所需的变换矩阵要求模型为每个顶点包含一个切线向量（副切线可以通过计算切线与法线的叉积来构造）。如果模型尚未定义切线向量，则可以计算它们。对于球体，可以精确计算，如下面对程序6.1的修改所示：

…

```cpp
for (int i=0; i<=prec; i++) {
    for (int j=0; j<=prec; j++) {
        float y = (float)cos(toRadians(180.0f - i*180.0f / prec));
        float x = -(float)cos(toRadians(j*360.0f / prec)) * (float)abs(cos(asin(y)));
        float z = (float)sin(toRadians(j*360.0f / prec)) * (float)abs(cos(asin(y)));
        vertices[i*(prec+1)+j] = glm::vec3(x, y, z);
    }
}

// calculate tangent vector
if (((x==0) && (y==1) && (z==0)) || ((x==0) && (y==-1) && (z==0))) // if north or south pole,
{ tangent[prec+1] = glm::vec3(0.0f, 0.0f, -1.0f); // set tangent to -Z axis
}
else // otherwise, calculate tangent
{ tangent[prec+1] = glm::cross(glm::vec3(0.0f, 1.0f, 0.0f), glm::vec3(x,y,z)); }
... // remaining computations are unchanged
}
```

对于不适合精确解析推导表面切线的模型，可以近似计算切线，例如在构造（或加载）顶点时，从每个顶点指向下一个顶点绘制向量。请注意，这种近似可能导致切线向量并不严格垂直于相应的顶点法线。因此，实现适用于多种模型的法线映射需要考虑这种可能性（我们的解决方案将做到这一点）。

切线向量从缓冲区（VBO）发送到顶点着色器中的一个顶点属性，就像顶点、纹理坐标和法线向量所做的那样。然后，顶点着色器以与法线向量相同的方式处理它们，即应用MV矩阵的逆转置，并将结果沿管线传递，供光栅化器插值，最终送入片段着色器。应用逆转置将法线和切线向量转换到相机空间，之后我们使用叉积构造副切线。

一旦我们在相机空间中有了法线、切线和副切线向量，就可以用它们构造一个矩阵（称为“TBN”矩阵，以其组成分量命名），该矩阵将从法线贴图获取的法线转换为相对于物体表面在相机空间中的对应朝向。

在片段着色器中，新法线的计算在calcNewNormal()函数中完成。函数第三行（包含dot(tangent, normal)的那一行）的计算确保切线向量垂直于法线向量。新的切线与法线的叉积产生副切线。

然后我们把TBN创建为一个3×3的mat3矩阵。mat3构造函数接收三个向量，生成一个矩阵，该矩阵第一行包含第一个向量，第二行包含第二个向量，第三行包含第三个向量（类似于从相机位置构建视图矩阵——参见图3.13）。

着色器使用片段的纹理坐标来提取对应当前片段的法线贴图条目。为此使用了采样器变量“normMap”，在本例中它绑定到纹理单元0（注意：因此C++/OpenGL应用程序必须已将法线贴图图像附加到纹理单元0）。要将颜色分量从存储范围[0..1]转换回其原始范围[-1..+1]，我们将其乘以2.0并减去1.0。

然后将TBN矩阵应用于所得法线，为当前像素生成最终法线。着色器的其余部分与用于Phong光照的片段着色器相同。片段着色器显示在程序10.2中，基于Etay Meiri [ME11]的一个版本。

存在多种工具用于生成法线贴图图像。一些图像编辑工具，如GIMP [GI20]和Photoshop [PH20]，具备此类功能。这些工具分析图像中的边缘，推断出峰和谷，然后生成对应的法线贴图。

图10.5展示了由Hastings-Trew [HT12]基于NASA卫星数据创建的月球表面纹理贴图。相应的法线贴图是通过将GIMP法线贴图插件[GP16]应用于同样由Hastings-Trew创建的黑白缩减图而生成的。

![](img/1695de1bc7486362f86c143285f3fb40_267_0.png)

**图10.5**  
月球、纹理和法线贴图。

## 程序10.2 法线映射片段着色器

```glsl
#version 430
in vec3 varyingLightDir;
in vec3 varyingVertPos;
in vec3 varyingNormal;
in vec3 varyingTangent;
in vec3 originalVertex;
in vec2 tc;
in vec3 varyingHalfVector;
out vec4 fragColor;

layout(binding=0) uniform sampler2D normMap;
// remaining uniforms same as before
...
vec3 calcNewNormal()
{
    vec3 normal = normalize(varyingNormal);
    vec3 tangent = normalize(varyingTangent);
    tangent = normalize(tangent - dot(tangent, normal) * normal);  // tangent is perpendicular to normal
    vec3 bitangent = cross(tangent, normal);
    mat3 tbn = mat3(tangent, bitangent, normal); // TBN matrix to convert to camera space
    vec3 retrievedNormal = texture(normMap, tc).xyz;
    retrievedNormal = retrievedNormal * 2.0 - 1.0; // convert from RGB space
    vec3 newNormal = tbn * retrievedNormal;
    newNormal = normalize(newNormal);
    return newNormal;
}

void main(void)
{ // normalize the light, normal, and view vectors:
  vec3 L = normalize(varyingLightDir);
  vec3 V = normalize(-varyingVertPos);
  vec3 N = calcNewNormal();

  // get the angle between the light and surface normal:
  float cosTheta = dot(L, N);

  // compute half vector for Blinn optimization:
  vec3 H = normalize(varyingHalfVector);

  // angle between the view vector and reflected light:
  float cosPhi = dot(H, N);

  // compute ADS contributions (per pixel):
  fragColor = globalAmbient * material.ambient
            + light.ambient * material.ambient
            + light.diffuse * material.diffuse * max(cosTheta,0.0)
            + light.specular * material.specular * pow(max(cosPhi,0.0), material.shininess*3.0);
}
```

![](img/1695de1bc7486362f86c143285f3fb40_269_0.png)

**图10.6** 使用月球纹理（左）和法线贴图（右）绘制的球体。

图10.6展示了以两种不同方式渲染月球表面的球体。左侧仅使用原始纹理贴图进行纹理映射；右侧使用图像法线贴图（供参考）。这两种情况都没有应用法线映射。尽管带纹理的“月球”十分逼真，但仔细检查可以发现，纹理图像显然是在月球从左侧被照亮时拍摄的，因为山脊的阴影投射到了右侧（在底部中央附近的陨石坑中最为明显）。如果我们要用Phong着色为此场景添加光照，然后通过移动月球、相机或光源来制作场景动画，这些阴影并不会像我们预期的那样改变。

此外，当光源移动（或相机移动）时，我们期望山脊上会出现许多镜面高光。但是，如图10.6左侧那样的普通纹理球体只会产生一个镜面高光，相当于平滑球体上会出现的高光，这看起来非常不真实。加入法线贴图可以大大改善此类物体上光照的真实感。

如果我们在球体上使用法线映射（而不是应用纹理），就会得到图10.7所示的结果。虽然（目前）还不及标准纹理映射逼真，但它现在确实会对光照变化做出响应。第一幅图像从左侧照亮，第二幅从右侧照亮。注意蓝色和黄色箭头显示了山脊周围漫反射光照的变化以及镜面高光的移动。

图10.8展示了在Phong光照下将法线映射与标准纹理映射相结合的效果。月球的图像通过漫反射光照区域和镜面高光得到增强，这些高光响应……的移动
