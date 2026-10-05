
# Unity Games by Tutorials

This limits the number of aliens you can spawn by the number of spawn points.

Add the following:

```csharp
aliensPerSpawn = (aliensPerSpawn > totalAliens) ?
aliensPerSpawn = totalAliens : aliensPerSpawn;
```

This is another chunk of preventive code. If aliensPerRow exceeds the maximum, the amount of spawns will reduce. This means a spawning event will never create more aliens than the maximum that you've configured.

Now comes the actual spawning code. Add the following:

```csharp
for (int i = 0; i < aliensPerSpawn; i++)
{
}
```

This loop iterates for each spawned alien. Add the following between the braces:

```csharp
if (aliensOnScreen < maxAliensOnScreen)
{
    aliensOnScreen += 1;
}
```

This code checks if aliensOnScreen is less than the maximum, and then it increments the total screen amount.

After the aliensOnScreen += 1, add the following:

```csharp
// 1
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
}
```

This code is responsible for finding a spawn point.

- 1. spawnPoint is the generated spawn point number. Because it references an index, it's set to -1 to indicate that a spawn point hasn't been selected yet.
- 2. This loop runs until it finds a spawn point or the spawn point is no longer -1.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_132_0.png)

3. This line produces a random number as a possible spawn point.

4. Next, it checks the previousSpawnLocations array to see if that random number is an active spawn point. If there's no match, then you have the spawn point. The number is added to the array and the spawnPoint is set, breaking the loop. If it finds a match, the loop iterates with a new random number.

Now that you have the spawn point index, you need to get the actual SpawnGameObject. Hang in there for a few more steps! You're close to unlocking an achievement.

Add the following after the closing brace of the while statement:

```csharp
GameObject spawnLocation = spawnPoints[spawnPoint];
```

Since there are already assigned spawn points in the Inspector, this grabs the spawn point based on the index that you generated in the last code.

Now, to spawn the actual alien. Add the following:

```csharp
GameObject newAlien = Instantiate(alien) as GameObject;
```

Instantiate() will create an instance of your prefab passed into it. It will create an object that is the type object, you must cast it into a GameObject. Now add the following:

```csharp
newAlien.transform.position = spawnLocation.transform.position;
```

This positions the alien at the spawn point. Save your code and switch back to Unity.

Select the GameManager and go to the Inspector. The Max Aliens on Screen to 10, Total Aliens to 10, Min Spawn Time to 0, Max Spawn Time to 3, and Aliens Per Spawn to 1.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_133_0.png)

Play your game and watch the Scene view. Glorious! Look at all those creepy critters. Achievement unlocked!

# Unity Games by Tutorials

# Chapter 5: Managers and Pathfinding

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_134_0.png)

- Alien
- Alien(Clone)
- Directional Light
- SpaceMarine
- Columns
- SpawnPoints
- Spawn
- Spawn
- Spawn
- Spawn
- Spawn
- Spawn
- Spawn
- Spawn
- Alien
- Alien
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)

| Max on Play | Mute audio | Stats | Gizmos |
| --- | --- | --- | --- |

# # Pathfinding in Unity

The aliens have arrived, but they're little more than decorations at this point. They need to get moving!

Seems like an easy enough task, yes? You could set a target for the aliens, and in each frame move them towards the target. Problem solved. End of chapter!

Of course, it's not that easy. First, you'd have to rotate the alien constantly so it faces the space marine. Second, a real problem occurs when an alien runs into a column.

The aliens will keep walking into the column until something causes them to move in a different direction. It's pretty ridiculous when a single column can block an entire mobile.

Perhaps you could get away with this behavior 20 years ago, but modern gamers expect better than this.

So what do you do?

Your first inclination may be to write the pathfinding code. For instance, you could write code that makes the aliens turn and move until they are free of the column, then redirect them towards the hero.

It's not that it wouldn't work, but you'd be treating a fundamental problem like an edge case. What would happen if you added another floor to the mix? You'd have to apply similar fixes, and then your code becomes an unreadable pile of spaghetti.

Thankfully, there's a better way.

# Unity's navigation system

It turns out Unity has pathfinding solutions you can use out of the box through its navigation system. Four objects comprise the navigation system:

- 1. Mesh: Represents walkable areas. This works on flat and dimensional terrain, such as stairs.
- 2. Agent: The actor or agent using the Mesh. You give it a goal and it will find its way using the NavMesh.
- 3. Mesh Link: A shortcut that can't be represented on the map, such as a gap that characters can actually cross.
- 4. Obstacle: Obstacles that the agent should avoid. Your agents will use pathfinding to figure a way around them.

To chase the hero, you first need a NavMesh over the entire floor to designate it as a walkable area. To start, click Window\Navigation. Unity will display the Navigation window (it appears in the right panel where the Inspector is usually by default). Take note of the tabs:

- Agents: Defines various agent sizes.
- Areas: Defines an area mask, like a physics layer.
- Bake: Configures the NavMesh's properties.
- Object: Lists the GameObjects you've added to the NavMesh.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_135_0.png)

# Unity Games by Tutorials

Select the Object tab and, in it, select the Renderers icon to apply a filter to the Hierarchy. Now, it'll only display GameObjects that have renderers attached to them. You can see it in the search field:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_136_0.png)

You can filter the Hierarchy by other types. To remove the filter, you can simply click the clear button (but don't do that right).

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_136_1.png)

Press Control on PC or Command on Mac and select Floor_Piece, Floor_Piece_001, Floor_Piece_002, Floor_Piece_003, Glass_Floor.

Some options will appear in the Navigation window. Check the Navigation Static checkbox to tell your selected meshes not to move.

Leave Generate Mesh Links unchecked. Otherwise, you'll get links between selected GameObjects.

Finally, you'll see a Navigation option — this is the navigation mesh you're currently building. Right now, you're working on the Walkable mask but can switch to Not Walkable or Jump. Your custom masks also appear in this drop-down as you create them in the Areas tab.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_136_2.png)

Click the Bake tab and then the Bake button at the bottom of the view. This saves the mesh.

# Unity Games by Tutorials

# Chapter 5: Managers and Pathfinding

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_137_0.png)

Now you have a place for allies to walk! After clicking the Bake button, the arena will turn a lighter blue. This indicates you've got a walkable NavMesh.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_137_1.png)

If you don't see the blue navigation mesh, check the Show NavMesh checkbox in the Scene view.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_137_2.png)

If you selected a different navigation area, such as Jump, then the color would have been orange.

# Unity Games by Tutorials

Click the Areas to see all the areas and colors that are available to you:

| Agents | Areas | Bake | Object | Name Cost |
| --- | --- | --- | --- | --- |
| Built-in 0 | Walkable | | | 1 |
| Built-in 1 | Not Walkable | | | 1 |
| Built-in 2 | Jump | | | 2 |
| User 3 | | | | 1 |
| User 4 | | | | 1 |
| User 5 | | | | 1 |
| User 6 | | | | 1 |
| User 7 | | | | 1 |

The pretty colors will "vanish" when you switch from the Navigation window, and you'll learn about the Bake tab in just a bit.

Clear the search in the Hierarchy at this point, and you are done with it.

# Creating agents

You have the mesh, so you need agents. Select the Alien in the Hierarchy (you should clear the Hierarchy filter to easily find this), and in the Inspector tab, click the Apply button at the top. As previously mentioned, this is how you push changes to the GameObject back up to the corresponding prefab.

Select the Alien prefab in the Prefabs folder. Click Add Component then click NavMeshAgent in the Navigation category. You have many options here:

| Nav Mesh Agent | |
| --- | --- |
| Agent Type | Humanoid |
| Base Offset | 0 |
| Steering | |
| Speed | 3.5 |
| Angular Speed | 120 |
| Acceleration | 8 |
| Stopping Distance | 0 |
| Auto Braking | [x | |
| Obstacle Avoidance | |
| Radius | 0.5 |
| Height | 2 |
| Quality | High Quality |
| Priority | 50 |
| Path Finding | |
| Auto Traverse Off | [x | |
| Auto Repath | [x] |
| Area Mask | Mixed ... |

raywenderlich.com

139
