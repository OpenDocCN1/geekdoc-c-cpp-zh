

Init() 负责设置该类核心工作所需的引用。这些是挂载到 gameObject 脚本的 transform，以及属于场景中主摄像机的 transform（通过 Unity 的 `camera.main` 找到）：

```cs
void Init() {
    // 缓存我们的 transform
    myTransform = transform;

    // 缓存相机
    Camera mainCam = Camera.main;
```

Camera.main 会寻找第一个标记为 `MainCamera` 标签的相机（参见 Unity 编辑器 Inspector 窗口中的标签下拉菜单）。如果场景中没有标记此标签的相机，该函数的主部分将无法正常工作。因此，如果 `mainCam` 为空，它将退出 `Init()`：

```cs
if (mainCam==null) {
    return;
}
```

摄像机的 transform 存储在 `cameraTransform` 中，它将在 `distanceBasedSpawnStart` 为 true 时用于触发生成：
```
cameraTransform = mainCam.transform;
```
它有一个自己的布尔值变量 `shouldReversePath`，由拥有它的路点控制器（waypoint controller）拥有。此行获取 `shouldReversePath` 布尔变量的值，并用它来覆盖路点控制器持有的现有保留值，所有生成的对象将使用该值。它通过调用 `waypointControl.SetReverseMode()` 实现：

```cs
// 告诉路点控制器我们想要反转路径
//还是不要
waypointControl.SetReverseMode(shouldReversePath);
```

统计 `spawnObjectPrefabs` 数组中有多少个对象：
```
totalSpawnObjects = spawnObjectPrefabs.Length;
```

如果 `AutoStartSpawningOnLoad` 为 true，则第一次生成将立即启动。
`TheWave()` 函数接收两个参数：它应该生成多少敌人，以及这里每次生成之间的时间间隔是多少。`StartWave()` 将调度未来的敌人生成：

```cs
if (shouldStartSpawningOnLoad) {
    StartWave(totalAmountToSpawn, timeBetweenSpawns);
}
```

`OnDrawGizmosSelected()` 函数每当此 gameObject 被选中时，都会在 Unity 编辑器中绘制辅助图形：

```cs
public void OnDrawGizmosSelected() {
}
```

一旦通过 `Gizmos.color` 设置了颜色，此之后绘制的所有内容都将采用设置的颜色：

```cs
Gizmos.color = new Color(0,0,1,0.5f);
```

`Gizmos.DrawCube()` 用于显示一个立方体，以显示相机多近才能触发生成。这是基于 `ndistanceFromCameraToSpawnAt` 的值：

```cs
Gizmos.DrawCube(transform.position,new Vector3(200,0,0,distanceFromCameraToSpawnAt));
```

此脚本派自 `MonoBehaviour` 的主要原因是可以使用 `Update()` 等系统函数。`Update()` 函数每帧被调用：

```cs
public void Update()
{
```

`aDist` 是一个临时浮点变量，用于计算此 transform 的 z 轴位置与相机位置之间的差异。使用 z 轴位置（而不是其他轴）是因为相机穿过关卡。相机沿着 z 轴推进关卡，因此对于该系统设计的游戏类型，只使用 z 轴是有意义的：

```cs
aDist=Math.Abs(Transform.position.z-cameraTransform.position.z);
```

如果组件使用了 `distanceBasedSpawnStart`，且当前没有正在进行的生成且距离小于 `distanceFromCameraToSpawnAt`，则可以生成下一波：

```cs
if(distanceBasedSpawnStart && !spawning && aDist<distanceFromCameraToSpawnAt)
{
  StartWave(totalAmountToSpawn,timeBetweenSpawns);
  spawning=true;
}
```

`StartWave()` 开始时重置几个将在生成周期期间使用的变量。使用计数器来跟踪生成的敌人数量（`spawnCounter`），并将名为 `HowMany` 的参数复制到另一个变量 `totalAmountToSpawn` 中，用以跟踪这一波应该包含多少对象：

```cs
public void StartWave(int HowMany, float timeBetweenSpawns)
{
  spawnCounter=0;
  totalAmountToSpawn=HowMany;
}
```

```cs
// 重置
currentObjectNum=0;
```

## 4.3 生成脚本

将使用 Unity 的 `InvokeRepeating` 反复调用 `doSpawn()` 函数。`InvokeRepeating` 会在 `CancelInvoke()` 告诉它停止之前持续调用 `doSpawn()`，或者场景从内存中移除。在调度新的重复调用之前，此代码使用 `CancelInvoke()` 确保任何之前的调用都已完全停止：

```cs
CancelInvoke("doSpawn");
InvokeRepeating("doSpawn", timeBetweenSpawns, timeBetweenSpawns);
```

`doSpawn()` 是由 `InvokeRepeating` 反复调用的函数。它调用 `SpawnObject()` 将新对象添加到场景：

```cs
void doSpawn()
{
SpawnObject();
}
```

`SpawnObject()` 首先检查生成计数器以判断该波是否已结束。当变量 `spawnCounter` 大于 `totalAmountToSpawn` 时，需要通过 `CancelInvoke()` 取消重复调用调用：

```cs
public void SpawnObject()
{
if(spawnCounter>totalAmountToSpawn)
{
// 在这里告诉你的脚本波已结束
CancelInvoke("doSpawn");
```

当这一波结束时，此脚本将禁用自身并退出，而不消耗不必要的 CPU 周期：

```cs
this.enabled=false;
return;
```

对象（敌人）通过单例实例创建。`SpawnController.Instance.SpawnGO()` 创建对象并返回新对象的 transform：

```cs
// 创建对象
tempObj=SpawnController.Instance.SpawnGO(spawnObjectPrefs[currentObjectNum],myTransform.position,quaternion.identity);
```

告诉对象是否需要反转路径：

```cs
// 告知路径反转
tempObj.SendMessage("SetReversePath", shouldReversePath);
```

新生成的对象需要知道使用哪个路点。与其通过 gameObject 寻找脚本，不如通过 `SendMessage` 调用。任何挂载在 gameObject 上的具有 `SetWaypoint` 函数的脚本都能接收它：

```cs
// 告知路点控制器
tempObj.SendMessage("SetWaypoint", waypointControl, MessageOptions.DontRequireReceiver);
```

如果 `shouldSetSpeed` 为 true，此函数将根据 `speedToSet` 的值设置对象的速度。与路点控制器一样，使用 `gameObject.SendMessage()` 来告知对象速度，而不是找到特定的脚本并调用其上的函数：

```cs
// 告知速度
if (shouldSetSpeed)
tempObj.SendMessage("SetSpeed", speedToSet, MessageOptions.DontRequireReceiver);
```

当 `shouldSmoothing` 为 true 时，使用 `gameObject.SendMessage()` 将平滑速率发送给名为 `SetSmoothingRate` 的函数。这将影响对象在路径上的转向速度：

```cs
// 告知平滑速率
if (shouldSmoothing)
tempObj.SendMessage("SetSmoothingRate", smoothingToSet, MessageOptions.DontRequireReceiver);
```

如果 `shouldRotateSpeed` 为 true，`gameObject.SendMessage()` 尝试将旋转速度值（来自变量 `rotateToSet`）发送给 `SetRotateSpeed()` 函数：

```cs
// 告知旋转速度
if (shouldRotateSpeed)
tempObj.SendMessage("SetRotateSpeed", rotateToSet, MessageOptions.DontRequireReceiver);
```

现在生成和设置完成后，我们增加 `spawnCounter` 和 `currentObjectNum` 计数器：

```cs
// 增加“已生成数量”计数器
spawnCounter++;
// 增加“下一个生成对象”计数器
currentObjectNum++;
```

变量 `currentObjectNum` 用于指向生成数组中的下一个对象。当它达到 `totalSpawnObjects-1` 的值时，即到达数组末尾，需要重置为零：

```cs
// 检查是否到达生成
// 对象数组的末尾
```

