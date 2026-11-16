

Renderer 的简化声明。

### 清单 6.5 渲染器的简化声明

单击此处查看代码图片

```
class Renderer
{
public:
    Renderer();
    ~Renderer();
    // Initialize and shutdown renderer
    bool Initialize(float screenWidth, float screenHeight);
    void Shutdown();
    // Unload all textures/meshes
    void UnloadData();
    // Draw the frame
    void Draw();
    void AddSprite(class SpriteComponent* sprite);
    void RemoveSprite(class SpriteComponent* sprite);
    class Texture* GetTexture(const std::string& fileName);
    class Mesh* GetMesh(const std::string& fileName);

private:

    bool LoadShaders();

    void CreateSpriteVerts();

    // Member data omitted

    // ...

};
```

Game 类随后在 Game::Initialize 中构造并初始化一个 Renderer 实例。请注意，Initialize 函数接收屏幕的宽度/高度，并将这些参数保存在成员变量中。接下来，Game::GenerateOutput 在渲染器实例上调用 Draw。已加载纹理的映射、已加载网格的映射以及 SpriteComponents 向量也移至 Renderer。这需要对整个代码库进行一些更改。然而，这些代码都不是新的；只是被移动了。从这一点开始，所有与渲染相关的代码都将放在 Renderer 中，而不是 Game 中。

## 再次探讨转换到裁剪空间

回顾第 5 章中实现的 OpenGL 2D 渲染，简单的视图-投影矩阵将世界空间坐标缩放为裁剪空间坐标。对于 3D 游戏，这种视图-投影矩阵是不够的。相反，你需要将视图-投影矩阵分解为独立的视图矩阵和投影矩阵。

### 视图矩阵

视图矩阵表示世界中相机（或“眼睛”）的位置和方向。第 9 章“摄像机”介绍了几种不同的摄像机实现，但目前我们先保持简单。至少，观察矩阵表示相机的位置和方向。

在构建观察矩阵的典型方法中，有三个参数：眼睛的位置、眼睛“看向”的目标位置以及上方向。给定这些参数后，你首先计算四个不同的向量：

```
$$\hat{k} = \frac{target - eye}{\|target - eye\|}

\hat{i} = \frac{up \times \hat{k}}{\|up \times \hat{k}\|}

\hat{j} = \frac{\hat{k} \times \hat{i}}{\|\hat{k} \times \hat{i}\|}

\vec{t} = \langle -\hat{i} \cdot eye, -\hat{j} \cdot eye, -\hat{k} \cdot eye \rangle$$
```

这些向量随后按如下方式定义观察矩阵的元素：

LookAt =
| i_x | j_x | k_x | 0 |
|---|---|---|---|
| i_y | j_y | k_y | 0 |
| i_z | j_z | k_z | 0 |
| t_x | t_y | t_z | 1 |

让相机移动的快速方法是为相机创建一个角色。该角色的位置表示眼睛位置。目标位置是相机角色前方的某个点。对于上方向，如果角色不能翻转倒置（目前正是这种情况），则 +z 可行。将这些参数传递给 `Matrix4::CreateLookAt`，即可获得有效的视图矩阵。

例如，如果相机角色是 mCameraActor，以下代码构建一个视图矩阵：

单击此处查看代码图片

```
// Location of camera
Vector3 eye = mCameraActor->GetPosition();
// Point 10 units in front of camera
Vector3 target = mCameraActor->GetPosition() +
mCameraActor->GetForward() * 10.0f;
Matrix4 view = Matrix4::CreateLookAt(eye, target, Vec
```

### 投影矩阵

**投影矩阵**决定了 3D 世界如何压平为屏幕上绘制的 2D 世界。3D 游戏中常见的两种投影矩阵是正交投影和透视投影。

在**正交投影**中，距离相机较远的物体与距离相机较近的物体大小相同。这意味着玩家无法感知物体距离相机是近是远。大多数 2D 游戏使用正交投影。图 6.3 展示了使用正交投影渲染的场景。

![](img/e9afcec1487716b0ef80d7e7c09869c8_447_0.png)

![](img/e9afcec1487716b0ef80d7e7c09869c8_447_1.png)

图 6.3 (a) 正交投影的俯视图和 (b) 屏幕上生成的 2D 图像

在*透视投影*中，距离相机较远的物体比较近的物体更小。因此，玩家感知到场景中有深度。大多数 3D 游戏使用这种投影，你将在本章的游戏项目中使用它。图 6.4 显示了与图 6.3 相同的 3D 场景，但这次使用透视投影。

![](img/e9afcec1487716b0ef80d7e7c09869c8_448_0.png)

![](img/e9afcec1487716b0ef80d7e7c09869c8_448_1.png)

**图 6.4** (a) 透视投影的俯视图和 (b) 屏幕上生成的 2D 图像

这些投影都有近平面和远平面。近平面通常非常靠近相机。相机与近平面之间的任何物体在屏幕上都不可见。这就是为什么当相机离物体太近时，游戏中的物体会部分消失。同样，远平面距离相机很远，超过它的任何物体也不可见。游戏有时允许玩家降低“绘制距离”以提高性能。这通常只是将远平面拉近的问题。

正交投影矩阵有四个参数：视图宽度、视图高度、到近平面的距离以及到远平面的距离。给定这些参数，正交投影矩阵如下：

```
Orthographic = [
  2/width   0         0         0
  0         2/height  0         0
  0         0         1/(far-near) 0
  0         0         near/(near-far) 1
]
```

请注意，这个正交投影矩阵类似于第 5 章中的 SimpleViewProjection 矩阵，只是多了考虑近平面和远平面的额外项。

透视投影有一个额外参数，称为水平视野（FOV）。这是投影中相机周围可见的水平角度。更改视野决定了 3D 世界中可见的部分。这是透视矩阵：

```
yScale = cot( fov / 2 )
xScale = yScale * height / width
Perspective = [ xScale 0 0 0 ; 0 yScale 0 0 ; 0 0 far/(far-near) 1 ; 0 0 -near*far/(far-near) 0 ]
```

### 注意

此处省略了正交投影矩阵和透视投影矩阵的推导。

两种投影矩阵在 `Math.h` 库中都有辅助函数。你可以使用 `Matrix4::CreateOrtho` 创建正交矩阵，使用 `Matrix4::CreatePerspectiveFOV` 创建透视矩阵。

### 计算视图-投影

视图-投影矩阵只是独立视图矩阵和投影矩阵的乘积：

ViewProjection = (View)(Projection)

顶点着色器随后使用此视图-投影矩阵将顶点位置从世界空间转换到裁剪空间。

### 告别画家算法，拥抱 Z 缓冲

第 2 章“游戏对象和 2D 图形”介绍了画家算法。回顾一下，画家算法从后向前绘制物体。虽然这对于 2D 游戏很棒，但在 3D 中会面临复杂情况。

### 画家算法的困境

3D 游戏中画家算法的一个主要问题是，从后到前的顺序不是静态的。随着相机在场景中移动和旋转，哪个物体在前面或后面会发生变化。要使用

