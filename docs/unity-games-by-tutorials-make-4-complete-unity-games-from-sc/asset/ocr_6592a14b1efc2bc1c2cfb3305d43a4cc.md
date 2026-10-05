Add the following beneath the previous variables:

```
public int maxAliensOnScreen;
public int totalAliens;
public float minSpawnTime;
public float maxSpawnTime;
public int aliensPerSpawn;
```

These are variables that you will use for gameplay for BobbleHeads Wars:

+   - maxAliensOnScreen: Will determine how many aliens appear on the screen at once.
- totalAliens: Will represent the total number of aliens the player must vanish to claim victory.
- minSpawnTime and maxSpawnTime: Will control the rate at which aliens appear.
- aliensPerSpawn: Will determine how many aliens appear during a spawning event.

Next, you need to add a few private variables that the GameManager will need for recordkeeping. Place the following underneath the public variables:

```
private int aliensOnScreen = 0;
private float generatedSpawnTime = 0;
private float currentSpawnTime = 0;
```

Here's what these will manage:

+   - aliensOnScreen: Will track the total number of aliens currently displayed. You'll tell it to the GameManager whether to spawn or wait.
- generatedSpawnTime: Will track the time between spawn events. You'll randomize this to keep the player on his toes. That way, the player won't be able to track when the aliens spawn, making the game harder to predict.
- currentSpawnTime: Will track the milliseconds since the last spawn.

With that done, the aliens are next.

# Spawning the aliens

Next up is writing the spawning code. With the GameManager script still open, add the following to Update():

```
currentSpawnTime += Time.deltaTime;
```

currentSpawnTime accumulates the amount of time that's passed between each frame update.