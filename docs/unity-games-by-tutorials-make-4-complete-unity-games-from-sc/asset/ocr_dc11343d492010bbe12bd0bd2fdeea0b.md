# Unity Games by Tutorials

This limits the number of aliens you can spawn by the number of spawn points.

Add the following:

```
```aliensPerSpawn = (aliensPerSpawn > totalAliens) ?
aliensPerSpawn = totalAliens : aliensPerSpawn;```
```

This is another chunk of preventive code. If aliensPerSpawn exceeds the maximum, the amount of spawns will reduce. This means a spawning event will never create more aliens than the maximum that you've configured.

Now comes the actual spawning code. Add the following:

```
```for (int i = 0; i < aliensPerSpawn; i++)
{
}
```
```

This loop iterates for each spawned alien. Add the following between the braces:

```
```if (aliensOnScreen < maxAliensOnScreen)
{
aliensOnScreen += 1;
}```
```

This code checks if aliensOnScreen is less than the maximum, and then it increments the total screen amount.

After the aliensOnScreen += 1, add the following:

```
```// 1
int spawnPoint = -1;
// 2
while (spawnPoint == -1)
{
// 3
int randomNumber = Random.Range(0, spawnPoints.Length - 1);
// 4
if (!previousSpawnLocations.Contains(randomNumber))
{
previousSpawnLocations.Add(randomNumber);
spawnPoint = randomNumber;
}
```
```

This code is responsible for finding a spawn point.

+   1. spawnPoint is the generated spawn point number. Because it references an index, it's set to -1 to indicate that a spawn point hasn't been selected yet.

+   2. This loop runs until it finds a spawn point or the spawn point is no longer -1.

![](bbox=[0.118, 0.933, 0.28, 0.953])