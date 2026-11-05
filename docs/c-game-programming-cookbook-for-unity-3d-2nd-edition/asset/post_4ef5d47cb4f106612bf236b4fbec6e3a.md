
modelRotateSpeed and Time.deltaTime. Time.deltaTime is used here to make sure that the rotations and movements will be the same regardless of frame rate or frame glitches, basing the movement amounts on time rather than relying on each frame happening at the exact same time.

```
void LookForTarget()
{
    // look for chase target
    LookAroundFor();

    // if there are obstacles, this is where we'll switch to a state that can avoid hitting them
    switch (obstacleFinderResult)
    {
        case 1: // go right
            SetAIState(AIState.stopped_turning_right);
            break;

        case 2: // go left
            SetAIState(AIState.stopped_turning_left);
            break;

        case 3: // back up!
            SetAIState(AIState.backing_up_looking_for_target);
            break;

        default: // default is just keep moving forward
            MoveForward();
            break;
    }
}
```

The LookForTarget() function calls LookAroundFor(), which will ensure that we have a suitable target and change the AI state to chase it if we do. LookAroundFor() is in the BaseAIController class, explained back in Section 10.2 of this book.

From there on, we take a look at what obstacleFinderResult is currently set to (you may remember this was set near the start of the UpdateCurrentState() function by calling the IsObstacleAhead() function). Depending on what obstacleFinderResult returns, we react to potential obstacles by either turning left, right, or backing up when obstacles are found on both left and right sides. If no obstacles are found, our switch statement will drop through to the default case, which calls MoveForward() to continuously move the bot forward until either it gets a suitable target to chase or happens upon an obstacle.

```
void ChasingTarget()
{
    // chasing
    if (_followTarget == null)
    {
        SetAIState(AIState.move_looking_for_target);
        return;
    }
}
```

The ChasingTarget() function above is called by UpdateCurrentState() when the AI state is AIState.chasing_target. The first thing to check is that we have a valid target in _followTarget. If we do not, SetAIState() is called on to change the state to move_looking_for_target, instead, then we drop out of the function with a return.

```
TurnTowardTarget(_followTarget);
distanceToChaseTarget =
    Vector3.Distance(_TR.position, _followTarget.position);
// check the range
if (distanceToChaseTarget > minChaseDistance)
    MoveForward();
```

When the bot is chasing, the code above calls TurnTowardTarget() to turn the bot toward _followTarget. TurnTowardTarget() is in BaseAIController. The next step is to find the distance between our bot (_TR.position) and the target (_followTarget.position), and assign it to the variable distanceToChaseTarget. We then compare distanceToChaseTarget to our minChaseDistance to make sure that we are not too close to the target. If the distance is higher than minChaseDistance, we continue to call MoveForward() which will set the vert input variable to continue to move the bot forward toward the target.

```
bool canSeePlayer = CanSee(_followTarget);
if (distanceToChaseTarget > maxChaseDistance
    || !canSeePlayer)
    SetAIState(AIState.move_looking_for_target);
```

Next, above, we declare a Boolean variable named canSeePlayer to store the result of a call to the CanSee() function. CanSee() will use Physics.Raycast to cast a ray between the bot and the player to tell if there is anything between them. CanSee() relies on collision layers to identify the player, referring to layers in the variable targetLayer (declared in BaseAIController) to ensure that the path to the player is clear. CanSee() returns true if the line is clear, false when there is an obstacle.

Above, we then check the distance to see if the target is too far away from the bot – further than maxChaseDistance. If distanceToChaseTarget is greater than maxChaseDistance, or CanSee() returned false, we call SetAIState() to change the state back to look for a new suitable target in AIState.move_looking_for_target.

```
void BackUpLookingForTarget()
{
    LookAroundFor();
    MoveBack();
    if (obstacleFinderResult == 0)
    {
        if (Random.Range(0, 100) > 50)
            SetAIState(AIState.stopped_turning_left);
        else
            SetAIState(AIState.stopped_turning_right);
    }
}
```

BackUpLookingForTarget() is called each frame from the UpdateCurrentState() function. It moves the bot backward when obstacles are found on both left and right sides in front of it, blocking the path forward. We start the function by calling LookAroundFor(), which tries to find a suitable target to chase. MoveBack() sets the input variable vert to -1, to move backward. Then, we look at obstacleFinderResult to see if any obstacles were found in front of the bot. If none were found, we now know that we have backed up enough to avoid whatever it was that was blocking the path prior to the state going into AIState.backing_up_looking_for_target. To help avoid the bot moving forward and moving right back into the obstacle that got it here, we generate a random number to decide which way to turn. If the number is above 50, the bot turns left. If less, it turns right. It will only turn a small amount, but it should be enough to avoid getting stuck.

```
void StoppedTurnLeft()
{
    // look for chase target
    LookAroundFor();

    // stopped, turning left
    TurnLeft();

    if (obstacleFinderResult == 0)
        SetAIState(AIState.move_looking_for_target);
}
void StoppedTurnRight()
{
    // look for chase target
    LookAroundFor();

    // stopped, turning right
    TurnRight();

    // check results from looking, to see if path ahead is clear
    if (obstacleFinderResult == 0)
        SetAIState(AIState.move_looking_for_target);
}
```

StoppedTurnRight() and StoppedTurnLeft() are identical except for a single line which calls out to either TurnLeft() or TurnRight() respectively. Both functions start with a call to LookAroundFor() to try to find a suitable target, and both functions will change the AI state to AIState.move_looking_for_target whenever no obstacles are found in front of the bot (via the obstacleFinderResult variable we set back in UpdateCurrentState()).

```
void MoveAlongWaypointPath()
{
    // make sure we have been initialized before trying to access waypoints
    if (!didInit && !reachedLastWaypoint)
        return;

    UpdateWaypoints();

    if (!isStationary)
    {
        targetMoveVec =
            Vector3.Normalize(_currentWaypointTransform.position - _TR.position);
        moveVec =
            Vector3.Lerp(moveVec, targetMoveVec, Time.deltaTime * pathSmoothing);
        _TR.Translate(moveVec * moveSpeed * Time.deltaTime);
    }

    if (faceWaypoints)
        TurnTowardTarget(_currentWaypointTransform);
}
```

Although none of the examples in this book use it, the function MoveAlongWaypointPath() is provided here should you need it. It uses the waypoints system from Chapter 8 to move the bot along a path set by waypoints. The bool isStationary can be used to start or stop the bot along its path. You can also set the bool faceWaypoints to decide whether or not to have the bot face the waypoint it is moving toward, or to just move, and keep its rotation.

```
public void SetMoveSpeed(float aNum)
{
    moveSpeed = aNum;
}
```

Finally, in this class, we have the SetMoveSpeed() function which can be used by other scripts to change the movement speed of our bot.

## 10.5 The AI Steering Controller Class – An AI Steering Controller

AI Steering Controller uses the waypoints system from Chapter 8 to provide inputs suitable for feeding into a vehicle script such as the BaseWheeledVehicle class from Chapter 6. This class will provide the variable horz (short for horizontal) with values between -1 and 1 suitable for steering toward waypoints and it will detect the angle to establish acceleration amounts. This script also ensures that the vehicle remains below a maximum speed.

```
using UnityEngine;
using AIStates;

namespace GPC
{
    public class AISteeringController : BaseAIController
    {
```

This class is derived from BaseAIController to use its state machine system.

```
public Vector3 relativeWaypointPosition;
public float turnMultiplier = 3f;
public float maxSpeed = 10f;
public BaseInputController _inputController;
```

Above, the few variables will become clearer as we go through the script. The _inputController should reference a BaseInputController or class deriving from BaseInputController that this AI is using for its inputs to drive the vehicle.

```
public override void Start()
{
    base.Start();
    SetAIState(AIState.move_along_waypoint_path);
}
```
