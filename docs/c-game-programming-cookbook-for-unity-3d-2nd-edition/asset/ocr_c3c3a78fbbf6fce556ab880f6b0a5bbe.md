The next step is to find out the relative position of the waypoint from the (_TR) Transform. Transform.InverseTransformPoint converts a position from world space into local space. In this case, we take the position of the waypoint and convert it into the local space of our Transform. _TR.

The result of the Transform.InverseTransformPoint space conversion is stored in a Vector3 type variable called relativeWaypointPosition. This vector now represents the direction that the AI would need to travel to reach the next waypoint.

By dividing the x value of relativeWaypointPosition by its magnitude, we end up with a number that says how much we would need to turn left or right to be facing the waypoint; the code places the calculated steer value into the variable horz (the variable name used for horizontal input throughout this book).

```
if (Mathf.Abs(horz) < 0.5f)
    vert = relativeWaypointPosition.z /
    relativeWaypointPosition.magnitude - Mathf.Abs(horz);
```

Now that horz contains the amount required to turn toward the next waypoint, this value may be used to slow down the bot if it is moving too fast.

The absolute (never negative) value of horz is checked against 0.5 to decide whether acceleration should be used. If the turn is more than 0.5, vert is unmodified at this stage, leaving it at its default value of 0. If the turn is less than 0.5, the acceleration put into the variable vert is calculated by taking the relativeWaypointPosition z value divided by its magnitude, with the horizontal turn amount subtracted from it.

The idea is, the more the turn the less the acceleration. In many cases, this should help the AI to get around corners without crashing.

```
if (obstacleFinderResult == 1)
    TurnRight();
if (obstacleFinderResult == 2)
    TurnLeft();
```

Above, we check the result of obstacleFinderResult and turn to avoid them, if needed. I would recommend not using the obstacle avoidance system to avoid other vehicles by not adding the vehicle layer to the Inspectors Obstacle Avoid Layers field. If you are using this with a racing game, trying to avoid other vehicles as obstacles this way tends to force the AI to drive off the track. Not ideal behavior!

```
horz *= turnMultiplier;
if (_RB.velocity.magnitude >= maxSpeed)
    vert = 0;
}
```

Next, we multiply horz by a variable named turnMultiplier. Different vehicles and different physics systems may require different values of input to make them turn in a reliable manner that gets your vehicles around the world. To compensate for this, you can adjust the turnMultiplier field via the Inspector on your AI vehicle to scale the turn amount as needed.

The last part of this function checks the magnitude of our vehicle's Rigidbody against a maxSpeed value. If we are going faster than the allowed maxSpeed, the vertical input is set to 0 to avoid any further acceleration and slow the vehicle.

```
void SteerToTarget()
{
```