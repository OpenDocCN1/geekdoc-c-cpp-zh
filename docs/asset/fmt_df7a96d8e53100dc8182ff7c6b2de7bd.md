
```csharp
// AI 状态定义在 AIStates 命名空间

private Transform proxyTarget;

private Vector3 relativeTarget;

private float targetAngle;

private RaycastHit hit;

private Transform tempTransform;

private Vector3 tempDirVec;

public float horz;

public float vert;

private int obstacleHitType;

// 编辑器可更改/可见

public bool isStationary;

public AIState currentAIState;

public float patrolSpeed=5f;

public float patrolTurnSpeed=10f;

public float wallAvoidDistance=40f;

public Transform followTarget;

public float modelRotateSpeed=15f;

public int followTargetMaxTurnAngle=120;

public float minChaseDistance=2f;

public float maxChaseDistance=10f;

public float visionHeightOffset=1f;

[System.Serializable]

public Vector3 moveDirection;

// 路点跟随相关变量

public Waypoints_Controller myWayControl;

public int currentWaypointNum;

[System.Serializable]

public Transform currentWaypointTransform;

}
```

```csharp
private int totalWaypoints;

private Vector3 nodePosition;

private Vector3 myPosition;

private Vector3 diff;

private float currentWayDist;
```

```csharp
[System.Serialized]

public bool reachedLastWaypoint;

private Vector3 moveVec;

private Vector3 targetMoveVec;

private float distanceToChaseTarget;
```

```csharp
public float waypointDistance = 5f;

public float moveSpeed = 30f;

public float pathSmoothing = 2f;

public bool shouldReversePathFollowing;

public bool loopPath;

public bool destroyAEndOfWaypoints;
```

```csharp
public bool faceWaypoints;

public bool startAtFirstWaypoint;

[System.Serialized]

public bool isRespawning;
```

```csharp
private int obstacleFinderResult;

public Transform rotateTransform;
```

```csharp
[System.Serialized]

public Vector3 RelativeWaypointPosition;
```

```csharp
public bool AIControlled;
```

```csharp
public void Start ()
{
  Init ();
}
```

```csharp
public virtual void Init ()
{
  // cache ref to gameObject
  myGO= gameObject;
  // cache ref to transform
  myTransform= transform;
  // rotateTransform may be get if the object we rotate is
  // different to the main transform
  if ( rotateTransform==null)
    rotateTransform= myTransform;
  // cache ref to our rigidbody
  myBody= transform.rigidbody;
  // init done!
  didInit= true;
}
```

```csharp
public void SetAIControl( bool state )
{
    AIControlled= state;
}
// set up AI parameters --------------------
```

```csharp
public void SetPatrolSpeed( float aNum )
{
    patrolSpeed= aNum;
}
```

```csharp
public void SetPatrolTurnSpeed( float aNum )
{
    patrolTurnSpeed= aNum;
}
```

```csharp
public void SetWallAvoidDistance( float aNum )
{
    wallAvoidDistance= aNum;
}
```

```csharp
public void SetWaypointDistance( float aNum )
{
    waypointDistance= aNum;
}
```

```csharp
public void SetMoveSpeed( float aNum )
{
    moveSpeed=aNum;
}
```

```csharp
public void SetMinChaseDistance( float aNum )
{
    minChaseDistance= aNum;
}
```

```csharp
public void SetMaxChaseDistance( float aNum )
{
    maxChaseDistance= aNum;
}
```

```csharp
public void SetPathSmoothing( float aNum )
{
    pathSmoothing= aNum;
}
// --------------------------------------
```

```csharp
public virtual void SetAIState( AIState newState )
{
    // update AI state
    currentAIState= newState;
}
```

```csharp
public virtual void SetChaseTarget( Transform theTransform )
{
    // set a target for this AI to chase, if required
    followTarget=theTransform;
}
public virtual void Update ()
{
    // make sure we have initialized before doing anything
    if(! didInit )
        Init ();
    // check to see if we're supposed to be controlling the player
    if (! AIControlled )
        return;
    // do AI updates
    UpdateAI();
}
public virtual void UpdateAI()
{
    // reset our inputs
    horz=0;
    vert=0;
}
int obstacleFinderResult= IsObstacleAhead();
witch (currentState)
{
    //
    case AIState.moving_looking_for_target:
        // look for chase target
        if(followTarget==null)
            LookAroundFor(followTarget);
        // the AvoidWalls function looks to see if there's
        // anything in front. If there is, it will
        // automatically change the value of moveDirection
        // before we do the actual move
        if( obstacleFinderResult==1 ) // 向左移动
            SetAIState( AIState.stopped_turning_left);
        if(obstacleFinderResult==2 ) // 向右移动
            SetAIState(AIState.stopped_turning_right);
        if(obstacleFinderResult==3 ) // 向后退
            SetAIState( AIState.backing_up_looking_for_target );
    // 全安全！向前移动
    MoveForward();
    break;
    case AIState.chasing_target:
        // in chase mode, we point toward the target
        // and go right at it!
        // quick check to make sure that we have a target
        // (if not, we drop back to patrol mode)
        if( followTarget==null )
            SetAIState(AIState.moving_looking_for_target);
        // the TurnTowardTarget function does just that, so
        // to chase we just throw it to the current target
        TurnTowardTarget(followTarget);
        // find the distance between us and the chase target
        // to see if it is within range
        distanceToChaseTarget=Vector3.Distance(myTransform.position,followTarget.position);
        // check the range
        if(distanceToChaseTarget==minChaseDistance )
        {
            // 保持前进
            MoveForward();
        }
        // here we do a quick check to test the distance
        // between AI and target. If it's higher than
        // our maxChaseDistance variable, we drop out of
        // chase mode and patrolling
        if(distanceToChaseTarget>maxChaseDistance || CanSee(followTarget)==false)
        {
            SetAIState(AIState.moving_looking_for_target);
        }
        break;
    case AIState.backing_up_looking_for_target:
        // look for chase target
        if(followTarget==null)
            LookAroundFor(followTarget);
        // 向后退
        MoveBack();
        if(obstacleFinderResult==0)
        {
            // now we've backed up, let's randomize whether go left or right
            if(Random.Range(0,100)>50)
            {
                SetAIState(AIState.stopped_turning_left);
            } else{
                SetAIState(AIState.stopped_turning_right);
            }
        }
        break;
    case AIState.stopped_turning_left:
        // look for chase target
        if(followTarget==null)
            LookAroundFor(followTarget);
        // 停止，向左转
        TurnLeft();
        if(obstacleFinderResult==0)
        {
            SetAIState(AIState.moving_looking_for_target);
        }
        break;
    case AIState.stopped_turning_right:
        // look for chase target
        if(followTarget==null)
            LookAroundFor(followTarget);
        // 停止，向右转
        TurnRight();
        if(obstacleFinderResult==0)
        {
            SetAIState(AIState.moving_looking_for_target);
        }
        break;
    case AIState.paused_looking_for_target:
        // 停顿，寻找目标
        if(followTarget==null)
            LookAroundFor(followTarget);
        break;
    case AIState.translate_along_waypoint_path:
        // 遵循路点（朝它们移动，而不是指向它们）以移动速度移动
        if(!isStationary)
        {
            targetMoveVec = Vector3.Normalize(currentWaypointTransform.position - myTransform.position);
            moveVec = Vector3.Lerp(moveVec, targetMoveVec, Time.deltaTime * pathSmoothing);
        }
        myTransform.Translate(moveVec * moveSpeed * Time.deltaTime);
        MoveForward();
        if( faceWaypoints )
        {
            TurnTowardTarget( currentWaypointTransform );
        }
        break;
    case AIState.steer_to_waypoint:
        // 确保在尝试访问路点之前已经初始化
```
