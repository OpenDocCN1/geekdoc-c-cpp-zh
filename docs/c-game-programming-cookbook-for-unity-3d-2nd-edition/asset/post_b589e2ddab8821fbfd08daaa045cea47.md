
_rotateTransform is an optional parameter which may be set in the Unity editor Inspector window to provide a Transform for rotation which is different to the one that the script is attached to. This is used in cases where we do not wish to rotate the main Transform.

```
didInit= true;
```

As with all of the other scripts in this book, didInit is a Boolean variable used to determine whether or not the Init() function has successfully completed.

```
public void SetAIControl( bool state )
{
    AIControlled= state;
}
```

Above, a Boolean variable named AIControlled is used to decide whether this script should take control. The SetAIControl() function just provides an easy way for other scripts to enable or disable AI control.

// set up AI parameters -------------------------
public void SetObstacleAvoidDistance(float aNum)
{
    obstacleAvoidDistance = aNum;
}
public void SetWaypointDistance(float aNum)
{
    waypointDistance = aNum;
}
public void SetMinChaseDistance(float aNum)
{
    minChaseDistance = aNum;
}
public void SetMaxChaseDistance(float aNum)
{
    maxChaseDistance = aNum;
}
// -----------------------------------------------

Above, functions to set several main parameters. Those are:

obstacleAvoidDistance(float) – In 3d units, how far the bot should look ahead in its attempts to avoid running into obstacles when it is patrolling.

wayPointDistance(float) – In 3d units, how close the bot will be allowed to get to a waypoint before it advances to the next waypoint.

minChaseDistance (float) – In 3d units, minChaseDistance determines how close the bot should get to its target, when chasing a target, before it stops moving toward it. This is to prevent the bot from getting too close and pushing the player around.

maxChaseDistance (float) – In 3d units, how far away from its target the bot can acknowledge a target.

```
public virtual void SetAIState(AIState newState)
{
    // update AI state
    targetAIState = newState;
    UpdateTargetState();
}
```

There will be times when we may need to force the state of the bot from another script, such as telling it which state to start in when the game begins. Use the function SetAIState() for that, passing in an AIState.

```
public virtual void SetChaseTarget(Transform theTransform)
{
    // set a target for this AI to chase, if required
    _followTarget= theTransform;
}
```

At the end of the SetAIState() function, above, we call UpdateTargetState() to do anything that needs to be done before we can fully switch mode to the new state. For example, you could call out to your animation system to play an animation when the AI changes state between patrolling and chasing. In the base version of this script, there is no extra logic in UpdateTargetState() and the function is there to maintain protocol of having a target state and a current state with a good place to trigger action when the target state is changed. If chasing is required, the SetChaseTarget() function should be used to pass in a reference to the Transform that needs chasing. When you pass a Transform into SetChaseTarget() the Transform will be stored in a variable named followTarget.

```
public virtual void Update()
{
    // make sure we have initialized before doing anything
    if (!didInit)
        Init();
}
```

The Update() function is called by Unity each frame update, but we need to be sure that the script has properly initialized before doing anything significant with it because it may be possible for Update() to be called before Init() has finished its run.

```
if (!AIControlled)
    return;

    // do AI updates
    UpdateCurrentState();
```

Above, remembering that we are still in the main Update() function, if AIControlled is not set to true this function drops out before it has chance to do anything. The Boolean variable AIControlled makes it possible to turn on or off AI control. For an example of where this may come in handy, it is great for situations where we may want AI to take control of the player; such as at the end of a racing game when the race is complete and we want the car to continue driving but take the player out of the game. The AI script would be attached to all players, but in the case of the user's vehicle it is only activated after the race finishes. This is what happens in the example racing game in this book, in Chapter 14.

UpdateCurrentState() is right at the core of the script – it is called by the Update() function and deals with coordinating the bot to do what it should:

```
public virtual void UpdateCurrentState()
{
```

In some cases, the AI script does not manipulate its GameObject's physics directly but instead acts as an input provider to another script which deals with the actual physics. The reason it works this way is so that AI can use the same movement controllers as the player without having to recode movement each time. For example, in the example racing game in Chapter 14, the AI cars use the exact same car physics as the user. When a car is set to use AI, the car physics controller script uses input from the AI script rather than a user input controller.

// reset our inputs
horz=0;
vert=0;

Above, the AI script uses horz and vert (both floats) to store horizontal and vertical input, which are the standard variable names used in other scripts in this book. Here in the UpdateCurrentState() function, they are reset to zero. This is centering the inputs before other functions change them.

```
switch (currentAIState)
{
    case AIState.paused_no_target:
        // do nothing
    break;
    default:
        // idle (do nothing)
    break;
}
```

Above, if there is anything that needs to be done when the AI is in a particular state, this is the place. The switch statement above takes the variable currentAIState and we run the corresponding code for whatever the current state is.

In BaseAIController, the UpdateCurrentState() function is a placeholder – it is assumed that you will override this function in a derived version of this class to put your own logic into it. You can find examples of this in the AIBotController and AISteeringController scripts in GPC_Framework/Scripts/COMMON/AI.

Before the state is changed from targetAIState to currentAIState, we need to go through the UpdateTargetState() function:

```
public virtual void UpdateTargetState()
{
    switch (targetAIState)
    {
        default:
            // idle (do nothing)
        break;
    }
    currentAIState = targetAIState;
}
```

As we know that this will only happen when a new current state is about to be set, we can call code that only needs to be called when the AI enters the new state. Just as UpdateCurrentState(), UpdateTargetState() is a placeholder that should be overridden by your own logic.

Next is a collection of functions to set inputs for turning left and right or moving forwards and backward:

```
public virtual void TurnLeft ()
{
    horz= -1;
}
```

```
public virtual void TurnRight ()
{
    horz= 1;
}
```

```
public virtual void MoveForward ()
{
    vert= 1;
}
```

```
public virtual void MoveBack ()
{
    vert= -1;
}
```

```
public virtual void NoMove ()
{
    vert= 0;
}
```

Each function above is there to make it easier to interface with other types of control systems. You can override them in a derived class or call them from another.

Next up is the LookAroundFor() function. This will be called when we need a bot to chase a target. For an example of using it, check out the AIBotController.cs script.

```
public virtual void LookAroundFor()
{
    if (_followTarget != null)
    {
        float theDist = Vector3.Distance
        (_TR.position, _followTarget.position);
        bool canSee = CanSee(_followTarget);
        if (theDist < maxChaseDistance)
        {
            if (canSee == true)
                SetAIState(AIState.chasing_target);
        }
    }
    else
    {
        GameObject potential =
GameObject.FindGameObjectWithTag(potentialTargetTag);
        _followTarget = potential.transform;
    }
}
```

The LookAroundFor() function, above, starts by making sure we have something in the _followTarget variable. The target may be set by this script or another outside script. If we have a target to follow already, we can go ahead and do a distance check using Unity's built in function Vector3.Distance() – the result of which we put into a local variable named theDist. We also do a test to see if our target is visible to the AI by calling CanSee() and storing the result in the local variable canSee. The CanSee() function is further down in the script. It will return true if the AI has a clear line between it and the target.
