
AI 控制器将路径点控制纳入其中，使用 WaypointsController 类来管理它们：

```
public void SetWayController( WaypointsController aControl )
{
    _waypointsController=aControl;
    aControl=null;
}
```

由于 AI 机器人不知道使用哪些路径点，因此另一个脚本（例如游戏控制器）将调用 SetWayController 并传入一个 WaypointsController 对象。

```
// grab total waypoints
totalWaypoints = _waypointsController.GetTotal();
```

上面，totalWaypoints 包含来自路径点控制器的路径点总数的缓存值，以避免每次需要时都去查找。

```
if( shouldReversePathFollowing )
{
    currentWaypointNum = totalWaypoints - 1;
} else {
    currentWaypointNum = 0;
}
```

如果 shouldReversePathFollowing 为 true，则起始路径点将是 Waypoint_Controller 脚本创建的路径点列表中最后一个。

```
Init();

// get the first waypoint from the waypoint controller
currentWaypointTransform = myWayControl.GetWaypoint(currentWaypointNum);
if(startAtFirstWaypoint)
{
    _TR.position= _currentWaypointTransform.position;
}
```

除其他事项外，此类中的 Init() 函数将 AI 机器人的 Transform 的引用缓存到变量 _TR 中。SetWayController() 函数调用 Init() 以确保引用已设置并准备好使用，因为它会将 _TR 重新定位到第一个路径点（当布尔变量 startAtFirstWaypoint 设置为 true 时）。

此类中的接下来两个函数是接口函数，供其他脚本在需要时更改值：

```
public void SetReversePath( bool shouldRev )
{
    shouldReversePathFollowing= shouldRev;
}
public void SetRotateSpeed( float aRate )
{
    modelRotateSpeed= aRate;
}
```

UpdateWaypoints() 负责保持当前目标路径点为最新，并在 AI 到达路径末端时（如有需要）执行自我销毁：

```
void UpdateWaypoints()
{
    // If we don't have a waypoint controller, we safely drop out
    if(_waypointsController==null)
        return;
}
```

上面，UpdateWaypoints() 首先检查 _waypointsController（对 WaypointsController 类实例的引用）是否不为 null，这应该意味着 SetWayController() 已被调用并成功设置。

AI 控制器脚本可以选择在到达最后一个路径点时自动销毁自己。当 destroyAtEndOfWaypoints 设置为 true 时，GameObject 会被销毁，并且此代码会立即退出 UpdateWaypoints() 脚本。

```
if( reachedLastWaypoint && destroyAtEndOfWaypoints )
{
    // destroy myself()
    Destroy( gameObject );
    return;
}
else if( reachedLastWaypoint )
{
    currentWaypointNum= 0;
    reachedLastWaypoint= false;
}
```

当 destroyAtEndOfWaypoints 为 false 时，假设路径点跟随应返回到开头；currentWaypointNum 设置为零，reachedLastWaypoint 被重置，AI 可以自由重新开始。

为了使此函数保持安全（以防在 WaypointsController 类中正确设置路径点之前以某种方式调用它），会进行检查以确保找到了多个路径点。如果 totalWaypoints 为零，则在退出 UpdateWaypoints() 函数之前会再次尝试从 _waypointsController 获取总数。

```
if( totalWaypoints==0 )
{
    // grab total waypoints
    totalWaypoints= _waypointsController.GetTotal();
    return;
}

if( _currentWaypointTransform==null )
{
    // grab our transform reference from the waypoint controller
    _currentWaypointTransform= _waypointsController.GetWaypoint( currentWaypointNum );
}
```

如果此时尚未设置 currentWaypointTransform 对象，则会调用 _waypointsController 使用变量 _currentWaypointNum 中保存的索引号提供一个。

计算两个 Transform 之间的距离会考虑 x、y 和 z 坐标。在大多数情况下，路径点跟随只需在二维平面上工作，y 轴可以完全去掉。这样做可以解决因高度与 x 和 y 轴差异结合导致当前路径点在正确时间未推进的问题。特别是对于转向或角色驱动的 AI，在路径点距离检查中几乎完全不需要 y 轴。

```
// now we check to see if we are close enough to the current waypoint
// to advance on to the next one
myPosition= _TR.position;
myPosition.y= 0;

// get waypoint position and 'flatten' it
nodePosition= _currentWaypointTransform.position;
nodePosition.y= 0;
```

在上面的代码中，myPosition（机器人位置的缓存 Vector3）和 nodePosition（缓存的路径点位置）都被去除了 y 轴。

```
currentWayDist= Vector3.Distance(
nodePosition,myPosition );
if ( currentWayDist < waypointDistance ) {
// we are close to the current node, so let's move on to the next one!
```

AI 机器人与下一个路径点之间的距离使用下面两个缓存的位置变量计算。当 resulting currentWayDist 值小于 waypointDistance 的值时，表示机器人已足够接近当前路径点，可以推进到下一个。

```
if( shouldReversePathFollowing )
{
    currentWaypointNum--;
}
```

在推进到下一个路径点之前，会检查 shouldReversePathFollowing 以确定 AI 沿路径需要去的方向。如果路径被反转，则 currentWaypointNum 的值会递减而不是递增。

```
// now check to see if we have been all the way around
if( currentWaypointNum<0 ){
    // just in case it gets referenced before we are destroyed, let's keep it a safe index number
    currentWaypointNum= 0;
    // completed the route!
    reachedLastWaypoint= true;
    // if we are set to loop, reset the currentWaypointNum to 0
    if(loopPath)
    {
        currentWaypointNum= totalWaypoints;
        reachedLastWaypoint= false;
    }
    return;
}
```

在上面的代码块中，如果路径被反转，当 currentWaypointNum 降到零以下时，它需要重置为路径另一端的路径点（仅在 loopPath 设置时）。为此，currentWaypointNum 将被设置为变量 totalWaypoints 的值。

在此代码段中发生的另一件事是，当我们知道已到达路径末端时，reachedLastWaypoint 的值会被设置为 true。这将在下一次 UpdateWaypoints() 调用时检查，以执行路径末端需要完成的操作（例如当 destroyAtEndOfWaypoints 设置为 true 时销毁 GameObject）。

```
} else {
    currentWaypointNum++;
    // now check to see if we have been all the way around
    if( currentWaypointNum==totalWaypoints ){
        // completed the route!
        reachedLastWaypoint= true;
        // if we are set to loop, reset the currentWaypointNum to 0
        if(loopPath)
        {
            currentWaypointNum= 0;
            // the route keeps going in a loop, so we don't want reachedLastWaypoint to ever become true
            reachedLastWaypoint= false;
        }
        // drop out of this function before we grab another waypoint into currentWaypointTransform, as
        // we don't need one and the index may be invalid
        return;
    }
}
```

shouldReversePathFollowing 布尔值必须已设置为 false 才能执行以下代码，这意味着 currentWaypointNum 已超过由路径点控制器保存的列表中的最后一个路径点，并且如果变量 loopPath 设置为 true，则 currentWaypointNum 需要重置为零。

```
// grab our transform reference from the waypoint controller
_currentWaypointTransform= myWayControl.GetWaypoint( currentWaypointNum );
}
```

对 currentWaypointNum 的操作完成后，我们可以使用其值作为索引号询问路径点控制器 myWayControl，以提供下一个路径点的 Transform。currentWaypointTransform 被设置为对 Waypoint_Controller.cs 函数 GetWaypoint() 的调用结果。

```
public float GetHorizontal()
{
    return horz;
}
public float GetVertical()
{
    return vert;
}
}
```
