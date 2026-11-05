
Above, helper functions above provide access to the horizontal and vertical input variables.

## 10.3 Enemy Stats

The BaseEnemyStatsController class can be used to add stats to an enemy in a similar way to how we deal with players. The way we use it in this book, we have it derive from BaseAIController so that it can be layered – the Blaster game example from Chapter 15 has a blaster enemy class that derives from BaseEnemyStatsController. This way, we get all of the AI and stats merged together so we do not have to have any references to other script Components to deal with things like enemy health and so on.

If you wanted to use this script as a standalone in your own game, you can just change the class declaration to derive from MonoBehaviour rather than BaseAIController. You also need to remove the base.Init() from the Init() function and remove override from the Init() function declaration. Do these things and this class will work independently of the AI system and/or framework.

```csharp
using UnityEngine;

namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Base/Enemy Controller")]
    public class BaseEnemyStatsController : BaseAIController
    {
        [Header("Enemy stats")]
        public int myID;
        private static int enemyUniqueID;

        public int defaultHealthAmount = 1;

        public int enemyHealth;
        public int enemyScore;
        public string enemyName;

        public override void Init()
        {
            base.Init();
            myID = enemyUniqueID;
            enemyUniqueID++;

            enemyScore = 0;
            enemyHealth = defaultHealthAmount;
        }

        public virtual void AddScore(int anAmount)
        {
            enemyScore += anAmount;
        }

        public virtual void AddHealth(int anAmount)
        {
            enemyHealth += anAmount;
        }

        public virtual void LoseScore(int anAmount)
        {
            enemyScore -= anAmount;
        }
    }
}
```

```csharp
public virtual void ReduceHealth(int anAmount)
{
    enemyHealth -= anAmount;
}

public virtual void SetScore(int anAmount)
{
    enemyScore = anAmount;
}

public virtual void SetHealth(int anAmount)
{
    enemyHealth = anAmount;
}

public int GetHealth()
{
    return enemyHealth;
}

public int GetScore()
{
    return enemyScore;
}

public void SetName(string aName)
{
    enemyName = aName;
}
}
```

Above, the script is self-explanatory. The Init() function sets default values for our enemy stats and each function provides a way to change or enemy stat set values.

## 10.4 The AIBotController Class – Making an Enemy Bot Controller

Let's talk a little about how this AI is supposed to work. Its behavior is rather basic, but it should be a good start for your own bots. What happens is that the AI bot will patrol around randomly, avoiding walls, until a player comes into range. At that point, our bot will turn to face the player and then go into chase mode, trying to head directly for the player whenever it is in sight. Our AI will also fire its weapon at random intervals by using the weapon control outlined in Section 10.6 of this chapter.

The AIBotController class uses BaseAIController to move a bot around and derives from BaseEnemyStatsController from the previous Section 10.3 to deal with enemy health.

```csharp
using UnityEngine;
using AIStates;

namespace GPC
{
    public class AIBotController : BaseEnemyStatsController
    {
        private Vector3 moveVec;
        private Vector3 targetMoveVec;
        private float distanceToChaseTarget;
```

```csharp
[Header("Movement")]
public bool isStationary;
public float moveSpeed = 30f;
public bool faceWaypoints;
```

Skipping through the variables, the only thing to note above is the class declaration deriving from BaseEnemyStatsController as mentioned at the start of the section.

```csharp
public override void Update()
{
    UpdateCurrentState();
    DoMovement();
}
```

Update() is called by the engine automatically and it is where we call for main AI updates to happen. We call out to UpdateCurrentState() and DoMovement().

```csharp
public override void UpdateCurrentState()
{
    // reset our inputs
    horz = 0;
    vert = 0;

    obstacleFinderResult = IsObstacleAhead();
}
```

UpdateCurrentState() is at the core of our state machine. The BaseAIController had a placeholder function, but here we override it and put it to some real use. We start by resetting the horz and vert inputs so that they start out at zero each pass. We then call out to IsObstacleAhead() to check the path, with its return value going into the variable obstacleFinderResult. This variable will be used by one or more of the functions we call from the oncoming case statement that will react to the current state, so we populate it here to avoid having to repeat calls to it each time further on.

```csharp
switch (currentAIState)
{
    // -------------------------
    case AIState.move_looking_for_target:
        LookForTarget();
        break;
    case AIState.chasing_target:
        ChasingTarget();
        break;
    // -------------------------
}
```

This function is called every frame, which means the logic we place in this case statement will be called each frame too. This is, essentially, the main loop for our AI states.

The code above is relatively straightforward – in each case, we check to see if currentAIState matches our case and, if it does, call a function to perform everything we want to do every frame in that state. For example, we call LookForTarget() when the currentAIState is AIState.move_looking_for_target. When the state is AIState.chasing_target, we call ChasingTarget().

The code for each state has been split out into an individual function, which makes it easier to debug later. Having big chunks of code inside a massive case statement is a recipe for disaster, so it is better to split them out like this to save headaches!

```csharp
case AIState.
backing_up_looking_for_target:
    BackUpLookingForTarget();
    break;
case AIState.stopped_turning_left:
    StoppedTurnLeft();
    break;
case AIState.stopped_turning_right:
    StoppedTurnRight();
    break;
case AIState.
paused_looking_for_target:
    Paused(true);
    break;
case AIState.
move_along_waypoint_path:
    MoveAlongWaypointPath();
    break;
case AIState.paused_no_target:
    break;
default:
    // idle (do nothing)
    break;
}
```

Above, we go through all the AIStates we want the bot to react to and call functions to deal with each one. We only use the states chasing_target, move_looking_for_target, stopped_turning_right, stopped_turning_left and backing_up_looking_for_target.

When we have a target, the state is chasing_target unless an obstacle is found - if there is an obstacle, we change to either stopped_turning_left, stopped_turning_right or backing_up_looking_for_target to avoid it. Otherwise, chasing_target aims for the target and moves forward constantly.

If we are in any of the turning or backing up states, we remain in those until the ObstacleFinderResult – populated by a call to IsObstacleAhead() – reports that the path forward is clear. When there are no obstacles in the backing_up_looking_for_target state, we choose a random direction to turn in, to reduce the risk of getting stuck whenever the path directly in front is blocked.

Next, the functions themselves:

```csharp
public virtual void DoMovement()
{
    // move forward
    _TR.Translate(0, 0, vert * moveSpeed * Time.deltaTime);
    _TR.Rotate(0, horz * modelRotateSpeed * Time.deltaTime, 0);
}
```

Above, the DoMovement() function uses Transform.Translate to move the bot around and Transform.Rotate to handle turning. We take the vert value and multiply it by our moveSpeed and Time.deltaTime. Transform.Rotate() takes three parameters for x, y, and z. We only need to rotate the y axis to turn our bot, so our rotation goes in the second parameter. The actual rotation amount comes from the variable horz, holding our horizontal input value, which is multiplied by
