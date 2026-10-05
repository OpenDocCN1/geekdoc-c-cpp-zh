3. This line produces a random number as a possible spawn point.

4. Next, it checks the previousSpawnLocations array to see if that random number is an active spawn point. If there's no match, then you have the spawn point. The number is added to the array and the spawnPoint is set, breaking the loop. If it finds a match, the loop iterates with a new random number.

Now that you have the spawn point index, you need to get the actual SpawnGameObject. Hang in there for a few more steps! You're close to unlocking an achievement.

Add the following after the closing brace of the while statement:

```
GameObject spawnLocation = spawnPoints[spawnPoint];
```

Since there are already assigned spawn points in the Inspector, this grabs the spawn point based on the index that you generated in the last code.

Now, to spawn the actual alien. Add the following:

```
GameObject newAlien = Instantiate(alien) as GameObject;
```

Instantiate() will create an instance of your prefab passed into it. It will create an object that is the type object, you must cast it into a GameObject. Now add the following:

```
newAlien.transform.position = spawnLocation.transform.position;
```

This positions the alien at the spawn point. Save your code and switch back to Unity.

Select the GameManager and go to the Inspector. The Max Aliens on Screen to 10, Total Aliens to 10, Min Spawn Time to 0, Max Spawn Time to 3, and Aliens Per Spawn to 1.

![](bbox=[0.311, 0.663, 0.693, 0.831])

Play your game and watch the Scene view. Glorious! Look at all those creepy critters. Achievement unlocked!