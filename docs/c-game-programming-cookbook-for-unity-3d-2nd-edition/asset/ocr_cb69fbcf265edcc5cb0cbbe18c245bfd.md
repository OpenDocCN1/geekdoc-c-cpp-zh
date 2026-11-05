```
{
    Gizmos.color=Color.red;
    Gizmos.DrawLine(currentPoint, firstPoint);
}
public void GetTransforms()
{
    _transforms = new List<Transform>();
}
```

To make the waypoints control script easy to use, we need to make sure that our waypoints are set up in a way in the scene where we want to use them. This format is an empty GameObject with the WaypointsController.cs component attached to it, with all waypoints as child objects in the Hierarchy. All of the Transforms found in the GetTransforms() function are added to a List named _ transforms like this:

```
foreach(Transform t in transform)
{
    // add this transform to our arraylist
    _transforms.Add(t);
}

totalTransforms=(int)_transforms.Count;
```

At the end of GetTransforms(), we store the total number of transforms in an integer for easy access later (so that we don't have to count the List each time we need to know how many Transforms it contains).

The rest of the class is made up of publicly accessible utility functions for other scripts to access:

| SetReverseMode | SetReverseMode sets the value of a Boolean variable called shouldReverse, which determines whether the path should be reversed. |
| FindNearestWaypoint | Finds the nearest waypoint to a given position, within a given distance, and returns its index number as an integer. There are two implementations of the FindNearestWaypoint, one adds the extra parameter of exceptThis. The function will find the closest waypoint as normal, but when exceptThis is used it will ignore the specified transform. |
| GetWaypoint | Returns the transform of the waypoint at the index number passed in (as an integer). |
| GetTotal | Returns an integer value representing the total number of waypoints this class has control over. |

```
public void SetReverseMode(bool rev)
{
    shouldReverse=rev;
}

public int FindNearestWaypoint ( Vector3 fromPos, float maxRange)
{
    if(transforms==null)
        GetTransforms();
    distance = Mathf.Infinity;
    int tempIndex = 0;
```

To find the nearest waypoint to the 3d vector fromPos, the variable distance starts out at Mathf.Infinity (the computer equivalent of an infinite number!). We use