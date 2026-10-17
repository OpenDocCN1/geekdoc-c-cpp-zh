
```csharp
if (!didInit && !reachedWaypoint)
    return;

UpdateWaypoints();

if (currentWaypointTransform == null)
{
    return;
}

// 现在我们只需要找到路点相对于汽车变换的坐标
// 这样我们就可以确定路点在左侧还是右侧
RelativeWaypointPosition = transform.InverseTransform(currentWaypointTransform.position);

// 通过将水平位置除以幅度，
// 我们得到了转角角度的小数百分比
// 可用于驱动轮子
horz = (RelativeWaypointPosition.x / RelativeWaypointPosition.magnitude);

// 现在我们对扭矩执行相同的操作，但要确保
// 在转急弯时不会应用任何引擎扭矩...
if (Mathf.Abs(horz) < 0.5f)
    vert = RelativeWaypointPosition.z / RelativeWaypointPosition.magnitude - Math.Abs(horz);
else {
    NoMove();
}
break;
}
```

```cs
{
  // 此函数可能在目标（target）设置好之前
  // 被调用，所以
  // 我们在这里捕获任何空值
  return;
}

// 现在我们只需要找到路点相对于汽车变换（transform）
// 的相对位置，这样我们就可以
// 确定路点在左侧或右侧有多远。
RelativeWaypointPosition = transform.InverseTransformPoint(followTarget.position);

// 通过将水平位置除以模长，
// 我们得到转弯角度的小数百分比，
// 我们可以用它来驱动轮子
horz = RelativeWaypointPosition.x / RelativeWaypointPosition.magnitude;

// 如果我们处于最小追逐距离之外，
// 移动吧！
if (Vector3.Distance(followTarget.position, myTransform.position) > minChaseDistance) {
  MoveForward();
} else {
  NoMove();
}
if (followTarget != null) {
  LookAroundFor(followTarget);
}

// 避墙函数（avoidWalls）检查前方是否有
// 东西。如果有，它将
// 自动改变移动方向（moveDirection）的值
// 在在我们执行实际移动之前
if (obstacleFinderResult == 1) { // 向左转
  TurnLeft();
}
if (obstacleFinderResult == 2) { // 向右转
  TurnRight();
}
if (obstacleFinderResult == 3) { // 向后退
  MoveBack();
}
break;
case AIState.paused_no_target:
  // 暂停且无目标 (paused_no_target)
  break;
default:
  // 空闲（什么都不做）
  break;
}
public virtual void TurnLeft()
{
    horz = -1;
}
public virtual void TurnRight()
{
    horz = 1;
}
public virtual void MoveForward()
{
    vert = 1;
}
public virtual void MoveBack()
{
    vert = -1;
}
public virtual void NoMove()
{
    vert = 0;
}
public virtual void LookAroundFor(Transform aTransform)
{
    // 在这里我们进行快速检查，测试 AI 与
    // 目标之间的距离。如果超过了我们的最大追逐距离
    // 变量，我们将退出追逐模式并返回
    // 巡逻。
    if (Vector3.Distance(myTransform.position, aTransform.position) < maxChaseDistance)
    {
        // 在进入追逐模式之前
        // 检查目标是否可见
        if (CanSee(followTarget) == true)
        {
            // 将状态设为追逐目标
            SetAIState(AIState.chasing_target);
        }
    }
}
private int obstacleFinding;
public virtual int IsObstacleAhead()
{
    obstacleHitType = 0;
}
// 快速检查以确保 myTransform 已设置
if (myTransform == null)
{
    return 0;
}
// 绘制出这条射线，我们可以看到它在做什么
debug.DrawRay(myTransform.position, (myTransform.forward + myTransform.right * 0.5f) * wallAvoidDistance);
debug.DrawRay(myTransform.position, (myTransform.forward + myTransform.right * -0.5f) * wallAvoidDistance);
// 从我们的 AI 发射一条射线，并将“结果”
// 放入名为 hit 的变量中
if (Physics.Raycast(myTransform.position, myTransform.forward + myTransform.right * 0.5f, out RaycastHit hit)) {
    // 障碍物
    // 它是左侧碰撞，所以现在是类型 1（尽管
    // 当我们检查另一侧时可能会改变）
    obstacleHitType = 1;
}
if (Physics.Raycast(myTransform.position, myTransform.forward + myTransform.right * -0.5f, out RaycastHit hit)) {
    // 障碍物
    if (obstacleHitType == 0) {
        // 如果我们还没有击到任何东西，这就是
        // 类型 2
        obstacleHitType = 2;
    } else {
        // 如果左右射线都击中了，
        // 它是类型 3
        obstacleHitType = 3;
    }
}
```

```cpp
// 在我们将另一个路点抓取到
// currentWaypointTransform 之前先跳出此函数，
// 因为我们不需要它，且索引
// 可能是无效的
return;
} else {
    currentWaypointNum++;
    // 现在检查是否已经到达所有的路点
    if (currentWaypointNum >= totalWaypoints) {
        // 路线已完成！
        reachedWaypoint = true;
        // 如果设置为循环，则将
        // currentWaypointNum 重置为 0
        if (loopPath) {
            currentWaypointNum = 0;
            // 路线将持续循环，
            // 所以我们不希望 reachedWaypoint
            // 变为 true
            reachedWaypoint = false;
        }
        // 在我们将另一个路点抓取到
        // currentWaypointTransform 之前先跳出此函数，
        // 因为我们不需要，且索引
        // 可能是无效的
        return;
    }
}
// 从路点控制器获取我们的变换引用
currentWaypointTransform = myControl.GetWaypoint(currentWaypointNum);
public float GetHorizontal() {
    return horz;
}
public float GetVertical() {
    return vert;
}
```

### 9.2.1 脚本解析

脚本以常用的命名空间开始（Unity 为所有 C# 脚本添加的默认命名空间），以及本章前面的 `AIStates`。通过将 `AIStates` 作为命名空间引入，可以像它是同一脚本的一部分一样访问它：

### 9.2 基础 AI 控制脚本

```csharp
using UnityEngine;
using System.Collections;
using AIStates;
```

有很多变量需要声明，所以暂时先不用担心它们。我们将在后的解析中看到它们是如何被使用的。

`Init()` 函数负责对 GameObject、transform 和其 rigidbody 创建缓存引用（注意：脚本假设 AI gameObject 上总是挂载有一个 rigidbody）：

```csharp
public void Init()
{
    // 缓存 gameObject 的引用
    myGO = gameObject;
    // 缓存 transform 的引用
    myTransform = transform;
    // 缓存 rigidbody 的引用
    myBody = myTransform.rigidbody;
}
```

`rotateTransform` 是一个可选参数，可以在 Unity 编辑器窗口中设置，以提供一个与脚本挂载的物体不同的旋转变换。这用于我们不希望旋转主变换的情况：

```csharp
// 如果我们要旋转的物体与
// 主变换不同，则可以设置 rotateTransform
if (rotateTransform == null)
    rotateTransform = myTransform;
```

与书中所有其他脚本一样，`didInit` 是一个布尔变量，用于确定 `Init()` 函数是否成功完成。

```csharp
// 初始化完成；
didInit = true;
```

一个名为 `AIControl` 的布尔变量用于决定此脚本是否应该接控制。`SetAIControl()` 函数为其他脚本启用或禁用 AI 控制提供了一种方便的方法：

```csharp
public void SetAIControl(bool state)
{
    AIControlled = state;
}
```

脚本继续包含了一些用于设置 AI 行为中几个参数的函数。它们如下：

- `patrolSpeed` (float) 决定机器人在巡逻时移动有多快。
- `patrolTurnSpeed` (float) 决定机器人在巡逻时转弯有多快。
- `wallAvoidDistance` (float) 以 3D 单位为单位，决定机器人在巡逻时尝试避免撞墙时向前看多远。
- `waypointDistance` (float) 以 3D 单位为单位，决定机器人在移动到下一个路点之前被允许距离路点多近。
- `speed` (float) 表示机器人在沿着路点路径移动时的速度。
- `targetDistance` (float) 以 3D 单位为单位，决定机器人在追逐目标时，在停止移动目标之前允许距离目标多近。这是为了防止机器人离太近而推开玩家。
- `chaseDistance` (float) 以 3D 单位为单位，决定机器人在放弃追逐回到巡逻模式之前，允许距离目标多远。

当机器人沿着路点路径移动时，每个路点之间的旋转是经过阻尼的（而不是机器人直接跳到每个点上）。这用于决定如何进行插值。

设置它们的函数如下：

```csharp
// 设置 AI 参数
public void SetPatrolSpeed(float aNum) {
    patrolSpeed = aNum;
}
public void SetPatrolTurnSpeed(float aNum) {
    patrolTurnSpeed = aNum;
}
public void SetWallAvoidDistance(float aNum) {
    wallAvoidDistance = aNum;
}
public void SetWaypointDistance(float aNum) {
    waypointDistance = aNum;
}
public void SetSpeed(float aNum) {
    speed = aNum;
}
public void SetTargetDistance(float aNum) {
    targetDistance = aNum;
}
public void SetChaseDistance(float aNum) {
    chaseDistance = aNum;
}
public void SetPathSmoothing(float aNum) {
    pathSmoothing = aNum;
}
```

某些时候我们需要更改 AI 状态，传入 `newState`：

```csharp
// 更新 AI 状态
public void SetAIState(AIState newState) {
    currentState = newState;
}
```

如果需要追逐，`SetAIControl` 函数传入变换：

```csharp
// 设置 Chase目标
public void SetChaseTarget(Transform theTransform) {
    followTarget = theTransform;
}
```

`Update()` 函数是脚本的核心，每帧调用一次：

```csharp
// 更新 AI
public virtual void Update() {
    if (!AIControlled) {
        return;
    }
    // ...
}
```

```cs
// 在执行实际移动之前，
// 自动改变 moveDirection 的值
if (obstacleFinderResult == -1) { // 向左移动
    SetAIState(AIState.stopped_running_length );
}
if (obstacleFinderResult == 2) { // 向右移动
    SetAIState(AIState.stopped_running_right );
}
```

当机器人左右两侧都检测到障碍物时，`IsObstacleAhead()` 的返回结果为 3。机器人并没有尝试避开前方挡住的物体，而是进入了后退状态——`AIState.backing_looking_for_target`：

```cs
if (obstacleFinderResult == 3) { // 后退
    SetAIState(AI State.backing_looking_for_target );
}
```

现在机器人已经决定了是否要转向或后退以避开障碍，剩下的工作就是向前移动。在下一个 `case` 的 处，调用了 `MoveForward()` 函数：

```cs
// 道路畅通！向前前进
MoveForward();
break;
```

下一个状态是 `AIState.chasing_target`：

```cs
case AIState.chasing_target:
// 在追逐模式下追逐，我们面向目标
// 并直接向它冲去！
```

由于此模式的主要目标是追逐 `followTarget` 中的 `transform`，我们需要确保其中确实有一个可以跟随的 `transform`。如果 `followTarget` 为空（`null`），脚本将将状态切回 `AIState.moving_looking_for_target`：

```cs
// 快速检查以确保我们有一个目标
// （如果没有，则退回到巡逻模式）
if (followTarget == null )
    SetAIState(AI State.moving_looking_for_target );
```
