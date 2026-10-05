
汽车会悬浮在地面静止位置上方，直到比赛开始，由于重力的作用，它会下落：

```csharp
public void CheckLock()
{
    if (isLocked)
    {
        // 控制被锁定，我们应该停止
        steer = 0;
        brake = 0;
        motor = 0;
        // 保持我们的位置刚性（但允许 Y 轴移动，
        // 如果没有与地形完全匹配，车辆可能会掉到地面上）
        Vector3 tempVEC = myBody.velocity;
        tempVEC.x = 0;
        tempVEC.z = 0;
        myBody.velocity = tempVEC;
    }
}
```

steer、motor 和 brake 是用于移动车辆的浮点变量。`GetInput()` 使用 `Math.Clamp` 将它们保持在合理范围内，因为它们是由默认输入设置的：

```csharp
public virtual void GetInput()
{
    // 计算转向量
    steer= Math.Clamp(default_input.GetHorizontal() , -1, 1);

    // 加油力度多少？
    motor= Math.Clamp(default_input.GetVertical() , 0, 1);

    // 刹车力度多少？
    brake= -1 * Math.Clamp(default_input.GetVertical() , -1, 0);
}
```

## 5.3.2 轮轴对齐

WheelCollider 在模拟轮胎方面表现出色，但如果我们想看到轮胎，仍然有更多工作要做完成；每个轮子网格都需要定位，以与其对应的 WheelCollider 匹配。
完整的脚本看起来如下：

> // 基于此论坛帖子中的工作：
// http://forum.unity3d.com/threads/50643-How-to-make-a-physically-real-
// stable-car-with-WheelColliders
// 由 Edy 完成。

```csharp
using UnityEngine;
using System.Collections;
```

```csharp
public class BaseWheelAlignment : MonoBehaviour
{

// 定义脚本中使用的变量，对应的
// 碰撞器位于可见轮子网格滑移位置的轮子碰撞器，slip prefab 是轮子打滑时实例化的 prefab，
// 旋转值是用于绕轴心旋转轮子的值。
public WheelCollider CorrespondingCollider;
public GameObject slipPrefab;
public float slipAmountForTireSmoke = 50f;
```

```csharp
private float RotationValue = 0.0f;
private Transform myTransform;
private Quaternion zeroRotation;
private Transform colliderTransform;
private float slipSuspensionDistance;
```

```csharp
void Start () {
    // 缓存一些常用项...
    myTransform = transform;
    zeroRotation = Quaternion.identity;
    colliderTransform = CorrespondingCollider.transform;
}
```

```csharp
void Update () {
    // 为射线检测碰撞定义一个击中点
    RaycastHit hit;
// 找到碰撞器的中心点，你需要这样做，
// 因为如果 transform 有偏移，碰撞器的中心点可能并不是
// 真实的位置。
Vector3 ColliderCenterPoint = colliderTransform.TransformPoint(CorrespondingCollider.center);
// 现在从轮子碰撞器的中心发射一条射线，距离为
// 悬挂，如果它击到了某些东西，则使用
// "hit" 变量的数据找到轮子
// 击中的位置，如果没有，则让轮子
// 沿着悬挂完全伸展。
    if (Physics.Raycast(ColliderCenterPoint, colliderTransform.up, hit, CorrespondingCollider.suspensionDistance + CorrespondingCollider.radius)) {
        myTransform.position = hit.point + (colliderTransform.up * CorrespondingCollider.radius);
    }
    else {
        myTransform.position = ColliderCenterPoint -
        (colliderTransform.up * CorrespondingCollider.suspensionDistance);
    }

// 现在将轮子旋转设置为碰撞器的旋转
// 结合一个新的旋转值。这个新值是
// 绕轴的旋转，以及来自
// 转向输入的旋转。

myTransform.rotation= colliderTransform.rotation *
Quaternion.Euler( RotationAngle, CorrespondingCollider.steerAngle, 0 );

// 通过旋转速度（每秒度数）增加该值
RotationValue+= CorrespondingCollider.rpm * ( 360 / 60 ) *
Time.deltaTime;

// 定义一个 wheelhit 对象，它存储了来自
// 轮子碰撞器的所有数据，并将允许我们确定
// 轮胎的打滑。
WheelHit correspondingGroundHit= new WheelHit();
CorrespondingCollider.GetGroundHit(out correspondingGroundHit );

// 如果轮胎的打滑大于 2.0f，且
// slip prefab 存在，则在地面上创建一个零旋转实例。
if ( Math.Abs(correspondingGroundHit.sidewaysSlip) > slipAmountForTireSmoke ) {
    if ( slipPrefab ) {
      SpawnController.Instance.Spawn( slipPrefab,
correspondingGroundHit.point, zeroRotation );
    }
}
```

## 5.3.3 脚本详解

BaseWheelAlignment.cs 脚本用于将轮子网格与轮子碰撞器对齐，并在打滑时提供生成轮胎烟雾的额外功能。当然，烟雾是可选的，但放在这里以防你之后需要。

每个轮子都应该挂载一个 BaseWheelAlignment 脚本（即轮子网格而非 WheelCollider），然后通过 Unity 编辑器检查器将 WheelCollider 组件的引用提供此脚本，到名为 `CorrespondingCollider` 的变量中。轮子应该与轮子碰撞器保持独立的，以便它们能够正确移动；不要将轮子网格设为碰撞器的子物体。

在示例 Metal Vehicle Doom 中，车辆在层级结构中所示：

- Car
- Body
- Colliders (body)
- WheelColliders
- Wheel_FL
- Wheel_FR
- Wheel_RL
- Wheel_RR
- WheelMeshes
- Wheel_FL
- Wheel_FR
- Wheel_RL
- Wheel_RR

