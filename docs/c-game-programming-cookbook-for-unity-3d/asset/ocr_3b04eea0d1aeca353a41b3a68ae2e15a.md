```
{
  // clear target
  AIControl.SetChaseTarget( null );

  // change AI state
  AIControl.SetAIState(AIState.moving_looking_
  for (_target) );

}
```

```
public bool CanSee( Transform aTarget ) {
  // first, let's get a vector to use for raycasting by
  // subtracting the target position from our AI position
  tempDirVec:Vector3.Normalize(aTarget.position -
  myTransform.position);

  // let's have a debug line to check the distance between the
  // two manually, in case you run into trouble!
  Debug.DrawLine(myTransform.position, aTarget.position);

  // cast a ray from our AI, out toward the target passed in
  // (use the tempDirVec magnitude as the distance to cast)
  if (Physics.Raycast(myTransform.position +
  ( visionHeightOffset * myTransform.up), tempDirVec, out hit,
  chaseDistance) {
    // check to see if we hit the target
    if (hit.transform.gameObject == aTarget.gameObject) {
      return true;
    }
  }
  // nothing found, so return false
  return false;
}
```

#  13.8.1 Script Breakdown

This script will utilize some of the functionality provided by MonoBehavior, which is where it derives from:

using UnityEngine;
using System.Collections;

The AIStates namespace is used by this script to make accessing the AIStates enumeration easier:

using AIStates;

```
public class SetAIChaseTargetBasedOnTag : MonoBehavior {
}
```