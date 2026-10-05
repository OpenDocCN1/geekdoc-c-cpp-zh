```
// find the distance between us and the chase target
// to see if it is within range
distanceToChaseTarget=Vector3.Distance
(myTransform.position,followTarget.position);
```

If the target is further than minChase3D units away, the bot will continue to move forward. The MoveForward() function takes keeping of things moving:

```
// check the range
if(distanceToChaseTarget>minChaseDistance)
{
    // keep charging forward
    MoveForward();
}
```

When the target transform is too far away, the AIState needs to switch back to the search/patrol state of AIState.moving_looking_for_target:

```
// we do a quick check to test the distance
// between AI and target. If it's higher than
our maxChaseDistance variable, we drop out of
// chase mode and go back to patrolling.
if(distanceToChaseTarget>maxChaseDistance ||
CanSee(followTarget)==false)
{
    // set our state to 1 - moving_looking_for_
    // target
    SetAIState(AIState.moving_looking_for_target);
}
```

```
break;
//
```

The next case is AIState.backing_up_for_target, which calls upon the MoveBack() function to take care of moving the bot backward:

```
case AIState.backing_up_for_target:
// look for chase target
if(followTarget!=null)
    LookAroundFor(followTarget);

// backing up
MoveBack();
```

Once IsObstacleAhead() returns a zero (no obstacles) into obstacleFinderResult, we try to avoid hitting the same obstacles by going into turning mode. Which direction to turn is randomized in the hope that if one proves unsuccessful in getting the bot out of the trap status, perhaps the other way will free it. To randomize, we use Random.Range(min,max) to represent a 50/50 percentage split over which direction it will turn:

```
if (obstacleFinderResult==0)
{
    // now we've backed up, let's randomize
    // whether to go left or right
    if (Random.Range(0,100)>50)
```