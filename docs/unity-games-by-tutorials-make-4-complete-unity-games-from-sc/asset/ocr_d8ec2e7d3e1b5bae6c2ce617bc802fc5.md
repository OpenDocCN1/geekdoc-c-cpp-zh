This will be the starting point of the second path, which has to look like this:

![](bbox=[0.269, 0.122, 0.73, 0.327])

Notice the slopes at the top right. These need extra waypoints at the start and end of them to make sure enemies ascend and descend them properly. Without them, they would either appear to be floating or moving through the ground.

![](bbox=[0.311, 0.403, 0.688, 0.513])

Add the necessary waypoints to make this path by duplicating Waypoint (1) and moving the copies around the map. Here's the list of positions to check after you're done:

+   * Waypoint (1): (-25, 0, 13)
* Waypoint (2): (3.5, 0, 13)
* Waypoint (3): (6.5, 1.5, 13)
* Waypoint (4): (11, 1.5, 13)
* Waypoint (5): (11, 1.5, 8.5)
* Waypoint (6): (11, 0, 5.5)
* Waypoint (7): (11, 0, -6.5)

Now, increase the size of Paths in the WaypointManager to 2. Set the size of Way Points to 0 and drag in your new waypoints like you did before. Now, disable EnemyPaths. You don't need the visualization of the path to progress.