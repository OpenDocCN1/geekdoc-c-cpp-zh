```
public Transform GetWaypointTransform () {
    // if we have no waypoint transform already 'in the system'
    // then we need to grab one
    if(currentWaypointTransform==null) {
        currentWaypointNum=0;
        currentWaypointTransform=
        waypointManager.GetWaypoint(currentWaypointNum);
    }
    return currentWaypointTransform;
}
```

```
public Transform GetRespawnWaypointTransform () {
    // if we are past the first waypoint, let's go back a
    // waypoint and return that one rather than the
    // current one. That way, the car will appear roughly where
    // it despawned rather than ahead of it.
    if(currentWaypointNum>0) {
        currentWaypointNum--;
    }
    currentWaypointTransform=
    waypointManager.GetWaypoint(currentWaypointNum);
    return currentWaypointTransform;
}
```

```
public void UpdateWaypoints() {
    if(!doInit) {
        Init();
    }
    // quick check to make sure that we have a reference to the
    // waypoint manager
    if (waypointManager==null) {
        return;
    }
    // because of the order that scripts run and are
    // initialized, it is possible for this function
    // to be called before we have actually finished running the
    // initialization, which means we need to drop out
    // to avoid doing anything silly or before it breaks the
    // game.
    if(totalWaypoints==0) {
        // grab total waypoints
        totalWaypoints = waypointManager.GetTotal();
        return;
    }
    // here, we deal with making sure that we always have a
    // waypoint set up and if not take the steps to find out
    // what our current waypoint transform should be
    if(currentWaypointTransform==null);
```