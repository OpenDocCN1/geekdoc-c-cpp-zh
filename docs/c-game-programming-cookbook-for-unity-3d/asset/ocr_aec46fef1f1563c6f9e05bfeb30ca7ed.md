MakeInvulnerable() and MakeVulnerable() set the setIsInvulnerable Boolean accordingly or show or hide the shield mesh referenced in shieldMesh, using GameObject.SetActive:

```
void MakeInvulnerable()
{
    isInvulnerable=true;
    shieldMesh.SetActive(true);
}

void MakeVulnerable()
{
    isInvulnerable=false;
    shieldMesh.SetActive(false);
}
```

The only thing left to do when this player has run out of lives (health) is to tell the game controller script about it. That way, the game controller can decide whether or not to end the game completely:

```
public void PlayerFinished()
{
    // tell the player controller that we have finished
    GameController_IP.Instance.PlayerDied(ownerID);
}
```

# 14.3.4 Enemies

The Enemy_IP.cs script:

```
using UnityEngine;
using System.Collections;

public class Enemy_IP : BaseArmedEnemy
{
    private bool isRespawning;
```

```
// here we add collision and respawning to the base armed enemy
// behavior
public void OnCollisionEnter(Collision collider)
{
    // when something collides with us, we check its layer to
    // see if it is on 9 which is our projectiles
    // (Note: remember when you add projectiles, set the layer
    // of the weapon parent correctly!)
    if (collider.layer==2 && isRespawning)
{
        myDataManager.ReduceHealth(1);
        if (myDataManager.GetHealth()==0)
        {
            tempINT=int.Parse(collider.gameObject.name);
        }
        // tell game controller to make an explosion at our
        // position and to award the player points for
        // hitting us
    }
}
```