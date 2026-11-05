Start() calls Start() on the class we derive from (BaseAIController) and starts things off with our AI state set to AIState.move_along_waypoint_path, which will serve as the main state for our steering behavior to work in when driving the vehicle.

```
public override void UpdateCurrentState()
{
    // reset our inputs
    horiz = 0;
    vert = 0;

    // look for obstacles
    obstacleFinderResult = IsObstacleAhead();

    switch (currentAIState)
    {
        case AIState.move_along_waypoint_path:
            SteerToWaypoint();
            break;

        case AIState.chasing_target:
            SteerToTarget();
            break;

        case AIState.paused_no_target:
            // do nothing
            break;

        default:
            // idle (do nothing)
            break;
    }
}
```

Above, just like the placeholder version of UpdateCurrentState in the BaseAIController class, we check each state, and call functions to run relevant code for each one. For the steering system, we only use three states: move_along_waypoint_path, chasing_target and paused_no_target.

```
void SteerToWaypoint()
{
    if (!didInit)
        return;
    UpdateWaypoints();
    if (_currentWaypointTransform == null)
        return;
}
```

Above, we check that the class has initialized (didInit is true) then make a call to UpdateWaypoints() which is an inherited function from the BaseAIController class. We then check that __currentWaypointTransform has a Transform in it. The UpdateWaypoints() function takes care of updating our current waypoint, checking the distances and so on, including setting _currentWaypointTransform to provide us with a target to steer toward.

```
relativeWaypointPosition = TR.InverseTransformPoint(_currentWaypointTransform.position);
// by dividing the horz position by the magnitude, we get a decimal percentage of the turn angle that we can use to drive the wheels
horz = (relativeWaypointPosition.x / relativeWaypointPosition.magnitude);
```