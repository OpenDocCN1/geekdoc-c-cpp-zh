The variable waypointManager must contain a reference to a waypoint controller to continue:

```
// quick check to make sure that we have a reference to the
// waypointManager
if (waypointManager==null) {
    return;
```

It may be possible for this function to be called before the waypoint controller has finished setting up, to avoid any problems we check if there are any waypoints set up, and if not, make a quick call to waypointManager.GetTotal() to get the total waypoints and drop out of the function:

```
// because of the order that scripts run and are
// initialized, it is possible for this function
// to be called before we have actually finished running the
// waypoints initialization, which means we need to drop out
// to avoid doing anything silly or before it breaks the game.
if(totalWaypoints==0) {
    // grab total waypoints
    totalWaypoints = waypointManager.GetTotal();
    return;
```

If there is no transform referenced in the currentTransform, this code assumes that this is the first run and sets currentWaypointNum to 0 before making a call out to the waypointManager.Get() function to return a usable transform:

```
// here, we deal with making sure that we always have a
// waypoint set up and if not take the steps to find out
// what our current waypoint should be
if (currentWaypointTransform==null) {
    currentWaypointNum=0;
    currentWaypointTransform=waypointManager.GetWaypoint(currentWaypointNum);
}
```

The checkpoint checking works by looking at the distance between the player and the waypoint and moving on to the next waypoint when distance gets too low. For this type of waypoint following, steering is employed to turn left or right depending on the direction of the waypoint, the y-axis may be discounted. It will serve only to make the distance checking more complicated (since it will be on three axes instead of two) the first part of this code takes the positions of the player and waypoint and copies them into variables. The copies have the y positions set to 0, removing the y-axis from further calculation:

```
// now we need to check if we are close enough to the
// current waypoint to advance to the next one

myPosition = myTransform.position;
myPosition.y=0;
```