# Now a ray cast is on the other side of the bot:

```
if (Physics.Raycast(myTransform.position, myTransform.forward +
    + myTransform.right * -0.5f, out hit, wallAvoidDistance ))
{
```

When the ray is cast, the code checks obstacleHitType to see whether it has been set by the previous raycast. If it has not been set, its value will be 0 at; this tells us that this ray is the first one to get a hit and that the function has only found an obstacle on this side—obstacleHitType gets set to 2:

```
// obstacle
if ( obstacleHitType==0 )
{
    // if we haven't hit anything yet, this is a
    // type 2
    obstacleHitType=2;
} else {
```

If we have found something on this side via the raycast and obstacleHitType is not at 0, we both raycasts have found obstacles (since the first raycast obstacle-HitType to 1 if it found something earlier). To represent obstacles on both sides, obstacleHitType gets set to 3:

```
// if we have hits on both left and right
    // raycasts, it's a type 3
    obstacleHitType=3;

```

The result of this function is the value of obstacleHitType. Earlier in this chapter, the main UpdateAI() function used this result to decide which way to turn or whether to go into reverse mode.

```
return obstacleHitType;

```

The next part of BaseAIController.cs is TurnTowardTarget(). This function does exactly what it seems–it will turn the bot (more specifically, the transform set in the variable-rotateTransform) toward the transform passed to it as a parameter:

```
public void TurnTowardTarget( Transform aTarget )
if (aTarget==null)
    return;
```

Earlier in this chapter, in the UpdateAI() function, we looked how AIState.translate_along_waypoint calculated the relative position of its target–it’s the same here, with the relative position of the target calculated with Unity’s Transform.InverseTransformPoint() function:

```
relativeTarget = rotateTransform.InverseTransformPoint(
( aTarget.position ) // // note we use rotateTransform as a rotation
// object rather than myTransform;
```