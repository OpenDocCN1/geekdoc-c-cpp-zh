
## 11.7.1 Script Breakdown

The EnemyBot_LBS class derives from BaseArmedEnemy, as described in Chapter 4 of this book:

```csharp
public class EnemyBot_LBS : BaseArmedEnemy
{
    public void Start ()
    {
        base.Start ();

        // let's find our AI controller
        BaseAIController aController = (BaseAIController) gameObject.GetComponent<BaseAIController>();

        // and tell to chase our player around the screen (we get)
        // the player transform from game controller
        aController.SetChaseTarget( GameController_LBS.Instance.GetMainPlayerTransform() );

        // now get on and chase it!
        aController.SetAIState(AIStates.AIState.chasing_target);

        // we also need to add this to the radar, so we will
        // tell game controller about it and
        // some code in game controller will do this for us
        GameController_LBS.Instance.AddEnemyToRadar(myTransform);
    }

    // game controller specifics (overridden for our laser blast)
    // survival game controller
    public override void TellGCENemyDestroyed()
    {
        // tell the game controller we have been destroyed
        GameController_LBS.Instance.EnemyDestroyed(myTransform);

        // remove this enemy from the radar
        GameController_LBS.Instance.RemoveEnemyFromRadar(myTransform);
    }

    public override void TellGCBossDestroyed()
    {
        // tell the game controller we have been destroyed (and that
        // we are a boss!)
        GameController_LBS.Instance.BossDestroyed();

        // remove this enemy from the radar
        GameController_LBS.Instance.RemoveEnemyFromRadar(myTransform);
    }
}
```

All of the games have different custom game controller scripts, it is not possible for all of the player scripts to try call their game controllers in the same way. Instead, some functions need to be designed to talk to a specific game controller. The enemy needs to tell the game controller when it is destroyed by its EnemyDestroyed() or BossDestroyed() function when the enemy is set to a boss. When an enemy is destroyed, it also needs to tell the game controller to remove its transform from the list of transforms that are being tracked by the radar.

## 11.8 Wave Spawning and Control

Here is the Wave_Spawner.cs script in full:

```csharp
using UnityEngine;
using System.Collections;

public class Wave_Spawner : MonoBehaviour
{
    public bool randomSpawning;
    public float timeBeforeFirstSpawn = 1f;
    public GameObject[] spawnObjectPrefabs;
    private int totalSpawnObjects;
    private int currentObjectNum;
    public int currentWave;

    void Start()
    {
        // count how many objects we have lined up in the spawn
        // object list
        foreach (GameObject go in spawnObjectPrefabs)
        {
            totalSpawnObjects++;
        }

        Debug.Log("Wave_Spawner.cs " + totalSpawnObjects + " objects to choose.");

        // schedule first wave
        Invoke("LaunchWave", timeBeforeFirstSpawn);
    }

    public void LaunchWave()
    {
        // in case there been any duplicate calls to Invoke
        CancelInvoke("LaunchWave");

        if (randomSpawning)
        {
            currentObjectNum = Random.Range(0, totalSpawnObjects - 1);
        }
        else
        {
            currentObjectNum++;
            // loop back to 0 when we reach the end
            if (currentObjectNum >= totalSpawnObjects)
            {
                currentObjectNum = 0;
            }
        }

        // logic for spawning the wave
        GameObject tempObj = SpawnController.Instance.SpawnGO(spawnObjectPrefabs[currentObjectNum], Vector3.zero, Quaternion.identity);
        
        // schedule next wave
        Invoke("LaunchWave", timeBeforeFirstSpawn);
    }
}
```
