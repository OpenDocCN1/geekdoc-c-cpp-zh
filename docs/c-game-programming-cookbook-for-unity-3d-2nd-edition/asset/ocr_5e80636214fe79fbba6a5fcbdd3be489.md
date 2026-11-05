```
```csharp
public bool GetIsFinished ()
{
    return isFinished;
}

public bool GetIsLapDone ()
{
    return isLapDone;
}
```
```

Above, GetIsFinished() and GetIsLapDone() both return Boolean values.

```
```csharp
public void SetWaypointsController ( Waypoints_Controller
aControl )
{
    _waypointsController= aControl;
}
```
```

As this script uses a waypoint controller to track the player's progress around the track, its _waypointsController variable (of type WaypointsController) needs to be set by another script. In the case of this game, it is set by the RaceGameManager when players are first spawned into the game Scene.

```
```csharp
public Transform GetWaypointTransform()
{
    if (_currentWaypointTransform == null)
    {
        currentWaypointNum = 0;
        _currentWaypointTransform =
_waypointsController.GetWaypoint(currentWaypointNum);
    }
    return _currentWaypointTransform;
}
```
```

Above, the current waypoint can be retrieved as a Transform with a call to GetWaypointTransform(). We hold a reference to the current waypoint Transform in the variable _currentWaypointTransform. If this variable is null, this function will detect that and retrieve the Transform from the _waypointsController instance instead.

```
```csharp
public Transform GetRespawnWaypointTransform()
{
    _currentWaypointTransform =
_waypointsController.GetWaypoint(currentWaypointNum);
    return _currentWaypointTransform;
}
```
```

GetRespawnWaypointTransform() is used to get the Transform that our waypoint system is currently aiming for. One example of where this is used is the respawn function. Respawn() gets the current waypoint Transform and sets our players rotation and position to match those of the waypoint, so that the player is in a safe place on the track and facing in the correct direction.

```
```csharp
public void UpdateWaypoints()
{
```
```

RaceController.cs keeps track of waypoints in UpdateWaypoints(). This function is not called from this class but will be called by the player control script.