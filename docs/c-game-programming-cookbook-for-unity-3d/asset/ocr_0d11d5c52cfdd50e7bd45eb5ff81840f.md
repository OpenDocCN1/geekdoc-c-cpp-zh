using UnityEngine;
using System.Collections;
using AIStates;

There are a lot of variables to declare, so don't worry about those right away. We will see how they are used later in the breakdown.

The Init() function takes care of making cached references to the GameObject, the transform, and its rigidbody (note the script assumes that there will always be a rigidbody- attached to the AI gameObject):

```
public void Init()
{
    // cache ref to gameObject
    myGO = gameObject;

    // cache ref to transform
    myTransform = transform;

    // cache a ref to our rigidbody
    myBody = myTransform.rigidbody;
```

rotateTransform is an optional parameter that may be set in the Unity editor window to provide a transform for rotation that is different from the one to which the script is attached. This is used in cases where we do not wish to rotate the main transform:

```
// rotateTransform may be set if the object we rotate is
// different to the main transform
if(rotateTransform==null)
    rotateTransform=myTransform;
```

With all of the other scripts in this book, didnt it a Boolean variable used to determine or not the Init() function has successfully completed.

```
// init done;
didInit=true;
```

A Boolean variable named AIControl is used to decide whether or not this script should take control. The SetAIControl() function provides an easy way for other scripts to enable or disable AI control:

```
public void SetAIControl( bool state)
{
    AIControlled= state;
}
```

The script continues with some functions to set several of the main parameters in the AI behavior. Those are the following:

+   - patrolSpeed (float) Determines quickly the bot should move when it is patrolling.
- patrolTurnSpeed (float) Determines quickly the bot should turn when patrolling.
- wallAvoidDistance (float) Determines, in 3D units, how far the bot should look ahead in its attempts to avoid running into walls when it is patrolling.