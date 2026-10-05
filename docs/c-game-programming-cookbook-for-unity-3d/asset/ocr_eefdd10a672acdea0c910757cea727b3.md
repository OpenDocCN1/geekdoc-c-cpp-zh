```
TellGCnemyDestroyed();
```

```
// if this is a boss enemy, tell the game controller
// when we get destroyed so it can end the level
if ( isBoss ) 
{
    TellGCBossDestroyed();
}
// destroy this
{
    Destroy(gameObject);
}
// game controller specifics (which will be overridden by
// different game controller scripts)
/
public virtual void TellGCnemyDestroyed()
{
    GameController_IP.Instance.EnemyDestroyed(myTransform.position, pointsValue, tempINT);
}

public virtual void TellGCBossDestroyed()
{
    GameController_IP.Instance.BossDestroyed();
}
```

# 14.3.4.1 Script Breakdown

The enemy behavior is based on path provided by the BaseAIController.cs script. It derives from the BaseArmedEnemy class, discussed in Chapter 9:

```
public class Enemy_IP : BaseArmedEnemy {
```

The BaseArmedEnemy class adds a data manager and support for the weapon system to our enemy script, but it does not deal with anything more than that. This script starts by adding collision checking and will deduct health from the data manager when hit:

```
public void OnCollisionEnter(Collision collider)
{
```

In this game, the player projectiles are set to use layer 9 (named player_project). When a collision occurs with this enemy, the colliding collider is passed as a parameter and its layer compared. If it matches with the player projectile and this is not respawning, a call to the data manager stored in myDataManager is to reduce health by 1:

```
if( collider.gameObject.layer==9 && isRespawning )
{
    myDataManager.ReduceHealth(1);
}
```