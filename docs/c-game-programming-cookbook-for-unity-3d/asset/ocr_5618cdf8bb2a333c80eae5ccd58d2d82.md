```
currentWaypointTransform=
waypointManager.GetWaypoint(currentWaypointNum);
```

```
}

return currentWaypointTransform;
}
```

It is inevitable that a player will need to respawn at some point. This might be due to a player getting stuck, a player falling out of the game area, or perhaps a player choosing to respawn when the car is facing the wrong way along the track. Whatever the reason, there should be a little penalty involved in respawning players from using it as an escape button when trouble hits.

GetRespawnWaypointTransform() is used to return a transform that the respawning code uses for positioning and rotation data. It does not return the current waypoint but instead the last waypoint passed. When this happens, it is also important to change the value of currentWaypointNum too, so that the current waypoint is not too far away from the respawn point.

When the function is called, it first checks if currentWaypointNum is more than 0 so that it can be decremented without breaking the code:

```
public Transform GetRespawnWaypointTransform ()
{
    // if we are past the first waypoint, let's go back a
    // waypoint and return that rather than the
    // current one. That way, the car will appear roughly where
    // it despawned rather than ahead of it.
}
```

As long as it is above 0, currentWaypointNum gets decremented by 1 here:

```
if (currentWaypointNum>0)
    currentWaypointNum--;

```

The new current waypoint is returned by the waypointManager via its GetWaypoint() function and then held in the currentWaypointTransform variable ready to be returned at the end of this function:

```
currentWaypointTransform=
waypointManager.GetWaypoint(currentWaypointNum)
```

next function is UpdateWaypoints(), which deals with keeping track of which waypoint the player should be aiming for and updates the waypoint counter as needed. UpdateWaypoints() is called by the player control script as part of its own update sequence:

```
public void UpdateWaypoints()
{
```

Before any waypoint checking can happen, the class must have run its initialization Init() function and set doneInit to true

```
if (!doneInit)
    Init();

```