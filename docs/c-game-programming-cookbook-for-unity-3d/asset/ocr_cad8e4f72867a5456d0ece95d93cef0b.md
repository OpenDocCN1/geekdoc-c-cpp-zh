OK, so there's no actual launching of anything, just prefab instantiating. It may not be as exciting as its name sounds, but the LaunchWave() function is at the core of the game:

```
public void LaunchWave()
{
}
```

We make a quick call to CancelInvoke just in case there been any duplicate calls to LaunchWave(). If more than one attack wave was spawned into the same level, our spawner would have trouble tracking how many enemies are left before the next wave and the system wouldn't work. If there are any previous Invoke calls to LaunchWave() queued up, they will be cancelled out by CancelInvoke:

```
CancelInvoke("LaunchWave");
```

The spawner may work in two different ways. One is to pick random items from the spawnPrefabObjects array and spawn them; the other is to progressively go through the array starting at zero and loop back to zero until the list is exhausted. If the Boolean randomSpawning is true, the currentToObject is set to a number between 0 and the total number of objects in the spawnPrefabObjects array using Random.Range. If randomSpawning is false, currentToObject incremented and a check is made to ensure that it loops to zero when it is incremented higher than the total number of objects in the array:

```
if(randomSpawning )
{
    currentToObjectNum= Random.Range ( 0, totalSpawnObjects-1 );
} else {
    currentToObjectNum++;

    // loop back to 0 when we reach the end of the
    // 'run' of things to spawn
    if(currentToObjectNum > totalSpawnObjects-1)
    {
        currentToObjectNum=0;
        // you could also implement something to tell
        // game control that all waves have finished if
        // you were making a game that only lasted until
        // that happens
    }
}
```

The next step is to instantiate the attack wave prefab. For this, an instance of the spawn controller (outlined in full back in Chapter 4, Section 4.3.1) is used and its SpawnGO (spawn game object) function. The parameters for SpawnGO are the prefab to be spawned, position and a Quaternion rotation:

```
// create an object
GameObject tempObj=
SpawnController.Instance.SpawnGO( spawnObjectPrefabs[currentToObjectNum], Vector3.zero, Quaternion.identity );
```

264 11. Dish: Lazer Blast Survival