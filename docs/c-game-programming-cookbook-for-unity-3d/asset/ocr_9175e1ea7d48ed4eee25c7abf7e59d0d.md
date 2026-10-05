As mentioned in this section, the TellGCnemyDestroyed() function (and also the TellGCBossDestroyed() function) is designed to be overridden if a new type of game controller is used. These functions call EnemyDestroyed() or BossDestroyed() on it.

GameController_IP.EnemyDestroyed() takes three parameters: the enemy destroyed, how much score the player should be awarded for blasting it, and finally, the owner ID of the projectile that the player may have identified. Without the ID, the game controller would not know which player to award the score to:

```
public virtual void TellGCnemyDestroyed()
```

```
GameController_IP.Instance.EnemyDestroyed(myTransform.position,
pointsValue, tempINT);
```

```
public virtual void TellGCBossDestroyed()
```

```
GameController_IP.Instance.BossDestroyed();
```

# 14.3.5 Waypoint Follower

Enemy spaceships move along waypoint paths as they fire at the player at the bottom of the screen. The BaseEnemy script controls firing, and the AI controller deals with path following through its translate_along_waypoint_path state. For the AI controller to do this, it needs to know which waypoint controller to use and has its AIState (its default state is to patrol, not follow, waypoints) and the BasepointFollower.cs script serves this purpose.

The BaseWaypointFollower.cs script:

```
// uses the translate_along_waypoint_path function of the AIController
// follow along a path
```

```
public class BaseWaypointFollower : ExtendedCustomMonoBehavior
{
    public BaseAIController AIController;

    public virtual void Start () {
        if(didInit)
            Init (
    }

    public virtual void Init () {
        // cache our transform
        myTransform= transform;

        // cache our gameObject
        myGO= gameObject;

        // cache a reference to the AI controller
        AIController= myGO. GetComponent<BaseAIController>();
    }
}
```