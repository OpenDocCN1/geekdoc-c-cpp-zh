

第4项之所以是个问题，是因为当今游戏渲染时常使用非常复杂的网格，但碰撞检测可能会使用精度较低的网格。困难在于，射线投射返回的交点可能与需要渲染贴花的位置相差很大。

### 20.2 总体思路

我们的技术提供的基本解决方案是：使用应用于贴花包围体的特殊片元着色器，将贴花投影到表面上，而不是在场景几何体上方渲染新的贴花多边形。实现此功能所需的唯一信息包括贴花的位置和方向、贴花的大小，以及包含当前渲染视口深度值的纹理。这些信息使得所有计算都可以在顶点着色器和片元着色器中完成。

渲染贴花时，我们自然会在“贴花空间”中工作，其中x轴和y轴位于贴花中心处底层表面的切平面上，z轴与贴花中心处表面的法向量平行。为了将数据移入贴花的局部坐标系，着色器需要提供贴花变换矩阵的逆矩阵。

清单20.1中的代码首先从片元位置的G缓冲区获取深度，并用它来重建片元的3D世界空间位置。`worldToDecal`常量是我们当前正在渲染的贴花变换矩阵的逆矩阵。使用此矩阵，我们可以将片元的位置转换到贴花的局部空间。然后可以使用此局部位置来计算采样贴花纹理的纹理坐标。在此第一个版本中，我们仅使用(x,y)位置，这只是沿贴花的局部z轴将贴花投影到底层几何体上，如图20.2所示。

![](img/7ba1225bb0e5a87be0fd35866408ffa7_436_0.png)

图20.2：将简单投影应用到局部x-y平面会导致贴花沿局部z轴方向被拉伸。

### 清单20.1：此代码确定正在渲染的片元的贴花空间坐标，并将其转换为贴花的纹理坐标。RT_Depth纹理包含视口的深度值，worldToDecal常量是贴花从贴花空间到世界空间的4x4矩阵变换的逆矩阵，recipDecalSize常量是1/s，其中s是场景中贴花的大小。

```
// Sample the depth at the current fragment
float pixelDepth = texture2DRect(RT_Depth, gl_FragCoord);
// Compute the fragment's world-space position
vec3 worldPos = ComputeWorldSpacePosition(gl_FragCoord);
// Transform into decal space
vec3 decalPos = worldToDecal * worldPos;
// Use the xy position of the position for the text
vec2 texcoord = decalPos.xy * recipDecalSize * 0.5;
// Fetch the decal texture color
gl_FragColor = texture2D(diffuseDecalTexture, texcoord);
```

### 20.3 几何体渲染

既然我们有了一些计算基本纹理坐标的代码，就必须考虑实际需要渲染什么样的几何体。使用贴花着色器渲染的每个片元都像一个“窗口”，我们可以通过它可能看到贴花。因此，我们可以只渲染一个与贴花大小和位置对应的表面对齐四边形。但是，我们希望贴花具有深度，因此我们改为渲染一个包围立方体，如图20.3所示。这样我们就可以从任何方向看到贴花，并且以后可以添加环绕功能。

![](img/7ba1225bb0e5a87be0fd35866408ffa7_437_0.png)

图20.3：以贴花为中心渲染包围立方体，可以确保我们从任何视角都能捕捉到贴花的影响。

作为包含大量贴花的场景的一种优化，通过硬件实例化渲染贴花可能很有优势[7]。因此，最好只是渲染一个单位立方体，并在顶点着色器中将其转换到正确的大小和位置，如清单20.2所示。请注意，我们可以轻松地将uniform常量decalSize和decalToWorld扩展为数组，并使用gl_InstanceID通过实例化渲染一批贴花。

### 清单20.2：此顶点着色器将单位立方体缩放到贴花的实际大小，并将其平移到贴花的世界空间位置。

```
uniform float decalSize;
uniform mat4 decalToWorld;

// scale the unit cube and position it in world space
vec4 worldPos = decalToWorld *
    vec4(gl_Vertex.xyz * decalSize, gl_Vertex.w);

// output the position in homogeneous clip space
gl_Position = gl_ModelViewProjectionMatrix * worldPos;
```

对于小贴花，此技术效果很好。但是，当启用背面剔除且深度测试设置为GL_LESS时，相机进入立方体的一瞬间贴花就会消失。解决此问题的一个方法是剔除正面并将深度测试设置为GL_GREATER。这样，只有世界位置实际上位于表面后面的片元才会被渲染，但当片元被更靠近相机的几何体遮挡时，会导致许多片元被不必要地渲染。

另一种解决方案是找到距离相机最近的立方体角，并在该深度处渲染一个足够大以包围整个立方体的相机对齐四边形。如果最近的角在近平面之前，则应在近平面处渲染全屏四边形。

### 20.4 淡出与环绕

我们已有基本的顶点着色器和片元着色器，但我们的投影沿贴花z轴无限延伸，产生了图20.2所示的拉伸效果。我们可以使用两种方法来解决此问题。更简单的方法是使用片元位置到贴花平面的距离作为淡出参数。此距离已在`decalPos.z`中可用，我们只需像清单20.3所示那样将其缩放到贴花的大小即可。

### 清单20.3：片元位置的贴花空间z坐标的绝对值被缩放到贴花的大小，并用作贴花颜色的淡出参数。如前所述，`recipDecalSize`常量是1/s，其中s是场景中贴花的大小。

```
// compute the distance of the fragment to the decal plane
float distance = abs(decalPos.z);

// scale the distance into the [0,1] range
// according to the size of the decal
float scaledDistance = min(distance * recipDecalSize, 1.0);

// somehow use that scaled distance to fade out
// here: simple linear fade out
float fadeOut = 1.0 - scaledDistance;

vec4 diffuseColor = texture2D(diffuseDecalTexture, texcoord);

gl_FragColor = vec4(diffuseColor.rgb, diffuseColor.a * fadeOut);
```

当贴花应该是平坦且不环绕几何体时，此方法很有用。用于淡出贴花的确切公式可以因贴花而异，以产生最佳效果，建议在引擎中将其设为可配置。

处理拉伸问题的一个更有趣的方法是让贴花环绕角落并遵循复杂表面的曲率。这对于血迹和其他溅射液体尤其有用，因为如果这样的贴花覆盖整个表面而与其曲率无关，会更加令人信服。

这很容易实现。我们只需要贴花中每个片元位置处的表面法线。如果将该法线旋转到贴花空间，其(x y)分量会给出表面相对于贴花平面的梯度。我们可以使用此梯度和片元到贴花平面的距离来修改纹理坐标。在没有相对斜率的区域，纹理查找保持不变，但在斜率较大的区域（例如，在角落处），纹理坐标会根据到贴花平面的距离向外移动。此技术在清单20.4中有所展示，结果如图20.4所示。

![](img/7ba1225bb0e5a87be0fd35866408ffa7_440_0.png)

图20.4：贴花根据表面法线环绕角落，并根据到贴花平面的距离进行淡出。

### 清单20.4：此代码演示了如何使用底层表面的法线来调整纹理坐标，使贴花能够环绕曲线和角落。RT_Normal纹理包含以RGB通道编码的视口法线向量。

