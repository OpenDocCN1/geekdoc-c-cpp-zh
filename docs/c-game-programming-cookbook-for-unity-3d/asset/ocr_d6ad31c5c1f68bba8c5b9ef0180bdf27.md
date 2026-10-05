```
{
if(Mathf.Abs(TEMPTrans.position.y - fromPos.y) < maxRange) {
    // set our current 'winner'
    // (closest transform) to the
    // transform we just found
    closest = TEMPTrans;

    // store the index of this
    // waypoint
    TEMPIndex=i;

    // set our 'winning' distance
    // to the distance we just
    // found
    distance = curDistance;
    }
}
// now we make sure that we did actually find
// something, then return it
if(closest) {
    // return the waypoint we found in this test
    return TEMPIndex;
} else {
    // no waypoint was found, return -1 (this
    // should be accounted for at the other end!)
    return -i;
}
}
```

GetWaypoint() returns the transform of the waypoint at the index passed in via the integer index.

```
public Transform GetWaypoint(int index) {
    if(shouldReverse) {
```

This is the only place in the class where shouldReverse is used. GetWaypoint will reverse the index numbers of the waypoints when shouldReverse is true (i.e., using GetWaypoint to get a waypoint with the index number of zero would return the last waypoint in the path, instead of the first).
To reverse the index passed in to this function, the variable index is modified by subtracting it from the number of transforms in totalTransforms.

```
// send back the reverse index'd waypoint
index=(totalTransforms)-index;
if(index<0)
    index=0;
}
```

# 7.1 Waypoint System