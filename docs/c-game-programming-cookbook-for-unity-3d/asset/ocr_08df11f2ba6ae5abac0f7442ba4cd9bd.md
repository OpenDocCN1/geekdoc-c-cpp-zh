```
private int totalWaypoints;

private Vector3 nodePosition;
private Vector3 myPosition;
private Vector3 diff;
private float currentWayDist;
```

```
[System.Serialized]
public bool reachedLastWaypoint;
private Vector3 moveVec;
private Vector3 targetMoveVec;
private float distanceToChaseTarget;
```

```
public float waypointDistance = 5f;
public float moveSpeed = 30f;
public float pathSmoothing = 2f;
public bool shouldReversePathFollowing;
public bool loopPath;
public bool destroyAEndOfWaypoints;
```

```
public bool faceWaypoints;
public bool startAtFirstWaypoint;
[System.Serialized]
public bool isRespawning;
```

```
private int obstacleFinderResult;
public Transform rotateTransform;
```

```
[System.Serialized]
public Vector3 RelativeWaypointPosition;
```

```
public bool AIControlled;
```

```
public void Start ()
{
  Init ();
}
```

```
public virtual void Init ()
{
  // cache ref to gameObject
  myGO= gameObject;

  // cache ref to transform
  myTransform= transform;

  rotateTransform may be get if the object we rotate is
  // different to the main transform
  if ( rotateTransform==null)
    rotateTransform= myTransform;

  // cache ref to our rigidbody
  myBody= transform.rigidbody;

  // init done!
  didInit= true;
}
```