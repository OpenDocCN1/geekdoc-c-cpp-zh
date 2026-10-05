
Comment out the line above if you find you are having trouble with automatically rotating points.

As the function continues, we continue to iterate through the waypoints and then close the path, if the Boolean variable is set to true (you can set that in the Inspector window of the editor when the GameObject has this script attached to):

```c
// update 'last' waypoint to become this one as
// we move on to find the next...
lastPos = currentPos;

// update the pointing transform
pointT=(Transform) transforms[i];

// close the path
if(closed)
{
    Gizmos.color=Color.red;
    Gizmos.DrawLine(currentPos, firstPoint);
}
```

After the GetTransforms() function discussed, the rest of the class is made up of publicly accessible utility functions for other scripts to access:

| Method | Description |
| :--- | :--- |
| SetReverseMode | Sets the value of a Boolean variable called shouldReverse, which determines whether or not the path should be reversed. |
| FindNearestWaypoint | Finds the nearest waypoint to a given position, within a given distance, and returns its index number as an integer. There are two implementations of the FindNearestWaypoint function, one of which adds the extra parameter of exceptThis. This function will find the closest waypoint as normal, when exceptThis will ignore the specified transform. |
| GetWaypoint | Returns the transform of the waypoint at the index number passed in (as an integer). |
| GetTotal | Returns an integer value representing the total number of waypoints this class has control over. |

```csharp
public void SetReverseMode(bool rev)
{
    shouldReverse=rev;
}

public int FindNearestWaypoint(Vector3 fromPos, float maxRange)
{
    // make sure that we have populated the transforms
    // list, if not, populate it
    if (transforms==null)
        GetTransforms();
    // make sure that we have populated the transforms
    // list, if not, populate it
    if (transforms==null)
        GetTransforms();
}
```

```csharp
// the distance variable is just used to hold the
// 'current' distance when we are comparing, so that
// we can find the closest
distance = Mathf.Infinity;
```

To find the nearest waypoint to the 3D vector fromPos, the variable distance starts out at a very large number—Mathf.Infinity. We use this to compare distances during the iteration loop below:

```csharp
// Iterate through them and find the closest one
for(int i = 0; i < transforms.Count; i++)
{
    // grab a reference to a transform
    TEMPtrans = (Transform)transforms[i];

    // calculate the distance between the current
    // transform and the passed in transform's
    // position vector
    diff = (TEMPtrans.position - fromPos);
    curDistance = diff.sqrMagnitude;

    // now compare distances - making sure that
    // we are not
    if (curDistance < distance)
}
```

As Mathf.Infinity is, well, infinity, this condition will always be satisfied at least once. There should be something closer than infinity, meaning that as long as there are transforms to compare, we should always get at least some kind of return no matter how far away they are in the 3D world.

```csharp
if( Mathf.Abs( TEMPtrans.position.y - fromPos.y ) < maxRange )
{
```

In some case, returning far away transforms may not always be the desired result, so maxRange is provided to at least some kind of cap on distance needed.

```csharp
// set our current 'winner'
// (closest transform) to the
// transform we just found
closest = TEMPtrans;
```

```csharp
// store the index of this
// waypoint
TEMPtransIndex=i;
```

```csharp
// set our 'winning' distance
// to the distance we just
// found
distance = curDistance;
```

![](img/041dca164b58875f4f1a64abb3328f5c_174_0.png)

# 7.1 Waypoint System

With the addition of the maxRange we can no longer be 100% sure of a return result, so a quick check makes sure that closest has something other than a zero in it before returning the result:

```csharp
// now we make sure that we did actually find
// something, then return it
if (closest) {
    // return the waypoint we found in this test
    return currentIndex;
} else {
    // no waypoint was found, return -1 (this
    // should be accounted for at the other end!)
    return -1;
}

// this function has the addition of a check to avoid finding the
// same transform as the one passed in. We use this to make sure
// that we are looking for the nearest waypoint we don't find
// the same one as we just passed
```

It is possible to have two different implementations of the same function, each with its own set of required parameters. Here, a second version of the FindNearestWaypoint() follows almost the same course as the first with the exception of a new transform passed in via exceptThis parameter discussed in this section.

```csharp
public int FindNearestWaypoint(Vector3 fromPos , Transform exceptThis, float maxRange) {
    // make sure that we have populated the transforms
    // list, if not, populate it
    if (transforms==null)
        GetTransforms();

    // the distance variable is just used to hold the
    // 'current' distance when we are comparing, so that
    // we can find the closest
    distance = Mathf.Infinity;

    // Iterate through and find the closest closest one
    for(int i = 0; i < transforms.Count; i++) {
        // grab a reference to a transform
        TEMPTrans = (transforms[i]);

        // calculate the distance between the current
        // transform and the passed in transform's
        // position vector
        diff = (TEMPTrans.position - fromPos);
        curDistance = diff.magnitude;

        // now compare distances - making sure that
        // we are not
        if (curDistance < distance && TEMPTrans != exceptThis)
    }
}
```

```csharp
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
    return currentIndex;
} else {
    // no waypoint was found, return -1 (this
    // should be accounted for at the other end!)
    return -1;
}
}
```

GetWaypoint() returns the transform of the waypoint at the index number passed in (as an integer).

```csharp
public Transform GetWaypoint(int index) {
    if(shouldReverse) {
```

This is the only place in the class where shouldReverse is used. GetWaypoint will reverse the index numbers of the waypoints when shouldReverse is true (i.e., using GetWaypoint to get a waypoint with the index of zero would return the last waypoint in, instead of the first).
To reverse the index passed in this function, the variable index is modified by subtracting it from the number of transforms in totalTransforms.

```csharp
// send back the reverse index'd waypoint
index=totalTransforms-index;
if(index<0)
    index=0;
}
```

Obviously, before trying to make sure that the waypoint transforms have been set up; send out a return value, it is not null. so there's a quick check to make sure that transforms is null. If transforms is null, we know that there will be no transforms to work with so GetTransforms() is called to get everything set up:

```csharp
// make sure we populated the transforms list,
// not, populate it
if(transforms==null)
    GetTransforms();
```

If the index being requested is too high, rather than return a wrong waypoint it will return a null value. The code on the requesting side can then check for a null return value and act accordingly:

```csharp
// first let's check to see if this index is higher than
// our waypoint count
// if so, we return null which needs to be handled on the
// other side
if(index>totalTransforms-1)
    return null;
```

Now that everything has been set up correctly (the transforms list contains waypoints and the index number is within range), all that is left to do is return the transform for the array:

```csharp
return (Transform) transforms[index];
```

The final piece in the waypoints controller script is GetTotal(), which is used by other scripts to find out how many waypoints there are:

```csharp
public int GetTotal()
{
    return totalTransforms;
}
```
