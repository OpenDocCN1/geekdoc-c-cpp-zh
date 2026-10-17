
```cs
{
// 3
if (camTarget != null) {
// 4
  var newPos = Vector2.Lerp(transform.position,
    camTarget.position,
    Time.deltaTime * trackingSpeed);
  var camPosition = new Vector3(newPos.x, newPos.y, -10f);
  var v3 = camPosition;
  var clampX = Math.Clamp(v3.x, minX, maxX);
  var clampY = Math.Clamp(v3.y, minY, maxY);
  transform.position = new Vector3(clampX, clampY, -10f);
}
}
```

1. 这些公共变量字段允许你设置相机将跟踪的目标、跟踪速度和相机的边界。
2. `FixedUpdate()` 在每个固定频率帧中被调用 —— 这是处理任何类型的 `Rigidbody` 组件的最佳方法。结果是相机将跟踪附载了 `Rigid2D` 的玩家。
3. 这个空值检查确保了在编辑器中已为 `camTarget` 字段分配了 `Transform` 组件。
4. `Vector2.Lerp()` 通过第三个参数的值（0 到 1 之间的值）在两个向量之间执行线性插值。通常情况下，你会使用它来随时间在位置之间移动。

## 添加 2D 物理的设置

现在是时候让你的精灵图与 2D 物理引擎愉快相处了...

## 脚本编写：平滑相机跟随

脚本编写是 Unity 中工作的重要部分，你将从一个简单的脚本开始，让相机平滑地跟随玩家移动。使其平滑的因素之一是你将其限制在具有 X 和 Y 边界的特定平面上。

打开 `Scripts` 文件夹并双击 `CameraLerpTransform` 在代码编辑器中打开它。

## 添加 2D 物理

现在，你的精灵图无法与物理引擎相互作用。它们只是悬浮在空中。如果存在反应，会让你认为你创建了一个平行宇宙。

Unity 的 2D 物理系统与 3D 系统类似。主要区别在于你使用每种类型的 2D 版本。

- `Rigidbody2D`: 使精灵图或对象受物理引擎的控制。通常每个使用碰撞器的项目都需要一个。
- `BoxCollider2D`: 为对象定义对齐矩形碰撞区域。
- `CircleCollider2D`: 为对象创建圆形碰撞区域。
- `PolygonCollider2D`: 根据设置的顶点创建任意多边形碰撞区域。它们通常比其他碰撞器更多的边，因此开销更高。使用这些时要小心！
- `EdgeCollider2D`: 由顶点定义的任意边。
- `CapsuleCollider2D`: 一个平滑的连续胶囊形碰撞器。因为它不容易在其他碰撞形状上卡住。
- `CompositeCollider2D`: 允许你将多个 `Box` 和 `Polygon` 形状合并成单个复合碰撞器。

下图显示了每个 `Collider2D` 的示例。绿色线条代表碰撞边界。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_338_0.png)

## 设置碰撞器
