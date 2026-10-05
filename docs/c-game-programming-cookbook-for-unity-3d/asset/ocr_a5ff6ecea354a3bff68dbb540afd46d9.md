```
// get waypoint position and 'flatten' it
nodePosition = currentWaypointTransform.position;
nodePosition.y=0;
```

The Unity Vector3.Distance takes two Vector3 positions and returns the distance between:

```
// check distance from this car to the waypoint

currentWaypointDist = Vector3.Distance(nodePosition,
myPosition);
```

When the distance in currentWaypointDist drops below waypointDistance, increments currentWaypointNum, advancing to the next waypoint:

```
if (currentWaypointDist < waypointDistance) {
// we are close to the current node, so let's move
// to the next one!
currentWaypointNum++;
```

When currentWaypointNum is greater than or equal to the number in totalWaypoints, we know that the player has been all the way around the track. This is not the place to increase the lap counter, however, as the player needs to cross the start/finish line before the lap may be increased. true when currentWaypointNum goes beyond the total number of waypoints, the variable isLapDone is set to true, and the value of currentWaypointNum is set back to 0 ready to aim for the next waypoint (which is now the first waypoint):

```
// now check to see if we have been all the way
// around the track and need to start again
if(currentWaypointNum==totalWaypoints) {
// completed a lap set the lapDone flag to
// true, which will be checked when we go over
// the first waypoint (so that you can't)
// almost complete a race then go back around
// the other way to confuse it)
isLapDone=true;
// reset our current waypoint to the first
// one again
currentWaypointNum=0;
```

The next part of the code will deal with the updating of currentWaypointTransform variable to reflect any changes to currentWaypointNum. Here the code calls upon waypointManager.GetWaypoint() and stores the return value in the currentWaypointTransform variable:

```
// grab our transform reference from the waypoint
// controller
currentWaypointTransform=waypointManager.GetWaypoint(currentWaypointNum);
```