![](bbox=[0.344, 0.085, 0.655, 0.273])

# Tweaks

Now that the game is fully up and running, there are a few tweaks that will make it a bit
more enjoyable. One of these is creating more waves! Currently, there's only one lonely
wave that follow the first path. Time to add some more.

Select Wave Manager in the Hierarchy, collapse Element 0 and set the Size of Enemy
Waves to 5.

Configure the waves as follows:

+   - Element 1: Set Path Index to 1, Start Spawn Time to 30 and Time Between
Spawns to 1.9. Drag a Tanky Enemy prefab to the List Of Enemies from the
Prefabs ▸ Enemy folder.
- Element 2: Set Path Index to 0, Start Spawn Time to 60 and Time Between
Spawns to 1.6. Drag 3 Fast Enemy prefabs into the List of Enemies.
- Element 3: Set Path Index to 1, Start Spawn Time to 110 and Time Between
Spawns to 1.5. Drag 4 Fast Enemy prefabs into the List of Enemies.
- Element 4: Set Path Index to 0, Start Spawn Time to 130 and Time Between
Spawns to 1.4. Drag 4 Tanky Enemy prefabs into the List of Enemies.

That should certainly up the ante. Test the game out with these new settings and see
how you do. Be sure to upgrade your towers as often as you can!