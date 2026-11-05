modelRotateSpeed and Time.deltaTime. Time.deltaTime is used here to make sure that the rotations and movements will be the same regardless of frame rate or frame glitches, basing the movement amounts on time rather than relying on each frame happening at the exact same time.

```
void LookForTarget()
{
    // look for chase target
    LookAroundFor();

    // if there are obstacles, this is where we'll switch to a state that can avoid hitting them
    switch(obstacleFinderResult)
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

The LookForTarget() function calls to LookAroundFor(), which will ensure that we have a suitable target and change the AI state to chase it if we do. LookAroundFor() is in the BaseAIController class, explained back in Section 10.2. of this book.

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

The ChasingTarget() function above is called by UpdateCurrentState() when the AI state is AIState.chasing_target. The first thing to check is that we have a valid target in _followTarget. If we do not, SetAIState() is called on