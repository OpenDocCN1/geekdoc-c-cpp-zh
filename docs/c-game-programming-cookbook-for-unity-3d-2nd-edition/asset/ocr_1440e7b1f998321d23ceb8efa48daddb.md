```
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

# 10.5 The AI SteeringController Class – An AI Steering Controller

AI SteeringController uses the waypoints system from Chapter 8 to provide inputs suitable for feeding into a vehicle script such as the BaseWheeledVehicle class from Chapter 6. This class will provide the variable horz (short for horizontal) with values between -1 and 1 suitable for steering toward waypoints and it will detect the angle to establish acceleration amounts. This script also ensures that the vehicle remains below a maximum speed.

```
using UnityEngine;
using AIStates;
namespace GPC
{
    public class AI SteeringController : BaseAIController
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