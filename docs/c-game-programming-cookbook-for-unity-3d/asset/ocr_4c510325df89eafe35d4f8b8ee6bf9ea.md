```
// The wheels should have a maximum rotation angle
targetAngle = Mathf.Clamp(targetAngle, -followTargetMaxTurnAngle-targetAngle, followTargetMaxTurnAngle);
```

```

// to turn towards the target at the rate of modelRotateSpeed
transform.Rotate(0, targetAngle * modelRotateSpeed * Time.deltaTime, 0);
```

```
public bool CanSee(Transform aTarget)
{
    // first, let's get a vector to use for raycasting
    // subtracting the target position from our AI position
tempDirVec=Vector3.Normalize(aTarget.position - myTransform.position);

    // let's have a debug line to check the distance between the
    // two manually, in case you ran into trouble!
Debug.DrawLine(myTransform.position, aTarget.position);

    // cast a ray from our AI, out toward the target passed in
    // (use the tempDirVec magnitude as the distance to cast)
if (Physics.Raycast(myTransform.position + 
    viewLightOffset * myTransform.up), tempDirVec, out
hit, maxDistance))
n        // check to see if we hit the target
        if(hit.transform.gameObject.layer == aTarget.gameObject.layer)
            return true;
    }
    // nothing found, so return false
    return false;
}
```

```
public void SetWayController(Waypoints_Controller aControl)
{
    myWayControl=aControl;
    aControl=null;

    // grab total waypoints
totalWaypoints = myWayControl.Total();

    // make sure that if you use SetReversePath to set
    // shouldReversePathFollowing that you call SetReversePath
    // for the first time BEFORE SetWayController, otherwise it
    // won't set the first waypoint correctly
if(shouldReversePathFollowing)
{
    currentWaypointNum= totalWaypoints-1;
} else {
    currentWaypointNum= 0;
}
```

```
Init();
```