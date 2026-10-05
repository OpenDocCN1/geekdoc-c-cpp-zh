Unity Games by Tutorials

Chapter 18: Making A Tower Defense Game

Here's what these methods do:

+   1. Sets the Instance variable to script itself.

+   2. Add to elapsedTime. Check if a new wave has to be started and update the wave that's active every frame.

+   3. Iterate over the enemyWaves.

+   4. Check that a wave wasn't already started before and the time spent in the level is the start time of that wave.

+   5. If so, make the enemy wave the active. Add it to the list of already activated waves and reset the spawn counter.

+   6. Break out of the list iteration as a suitable wave has been found.

+   7. An empty method up until now. This is filled in the next part.

Now for the actual spawning. Add this code inside UpdateActiveWave():

```
//1
if (activeWave != null)
{
    spawnCounter += Time.deltaTime;
    //2
    if (spawnCounter >= activeWave.timeBetweenSpawnsInSeconds)
        spawnCounter = 0;
    //3
    if (activeWave.listOfEnemies.Count != 0)
        //4
        GameObject enemy = (GameObject)Instantiate(
            activeWave.listOfEnemies[0], WaypointManager.Instance.GetSpawnPosition(activeWave.pathIndex), Quaternion.identity
        );
        //5
        enemy.GetComponent<Enemy>().pathIndex = activeWave.pathIndex;
        //6
        activeWave.listOfEnemies.RemoveAt(0);
}
else
{
    //7
    activeWave = null;
    //8
    if (activatedWaves.Count == enemyWaves.Count)
    {
        // All waves are over
    }
}
```

raywenderlich.com

518