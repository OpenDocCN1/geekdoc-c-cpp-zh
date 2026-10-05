Here's the play-by-play:

+   1. Just like the WaypointManager, this class also uses the singleton pattern to make itself everywhere using this variable.

+   2. The list of enemy waves that'll be spawned by this class.

+   3. This keeps track of how much time has passed since the level started in seconds.

+   4. The wave that's currently spawning enemies.

+   5. This keeps track of when the last wave spawned. It gets reset to 0 with every spawn, and is incremented in every frame while a wave is spawning.

+   6. A list of waves that were already started. Any waves in here won't start again.

Under the variable declarations you just added, add these methods:

```
//1
void Awake()
{
    Instance = this;
}
//2
void Update()
{
    elapsedTime += Time.deltaTime;

    SearchForWave();
    UpdateActiveWave();
}
private void SearchForWave()
{
    //3
    foreach (EnemyWave enemyWave in enemyWaves)
    {
        //4
        if (!activatedWaves.Contains(enemyWave))
            && enemyWave.startSpawnTimeInSeconds <= elapsedTime
        {
            //5
            activeWave = enemyWave;
            activatedWaves.Add(enemyWave);
            spawnCounter = 0f;
            //6
            break;
        }
    }
}
//7
private void UpdateActiveWave()
{
}
```