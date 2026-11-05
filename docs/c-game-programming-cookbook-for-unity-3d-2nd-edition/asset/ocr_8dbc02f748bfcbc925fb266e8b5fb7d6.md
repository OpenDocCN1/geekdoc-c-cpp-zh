# # 8 Waypoints Manager

# ## 8.1 Waypoint System

Waypoints can be used for more than just guiding AI objects or players around the game world. We can use them to guide a camera for cut scenes or a guided camera system, track who is winning a race, use them to make sure that the player is going in the right direction along a path, to reposition players in a safe location, for counting laps during a race and quite probably a whole other number of uses that don't immediately spring to mind. Waypoints are really useful for game developers.

For an example of this script in action, check out the racing game example in Chapter 14.

Our waypoints manager needs to be flexible enough to provide the functionality for all of these uses and then some, without going against the componentized methodology we are employing for this book. The functions it should provide are:

+   1. Produce a visual representation of the path we want our AI cars to take, to make manipulation of our waypoints in the editor a little easier
+   2. Provide an interface that can allow other scripts to search for the nearest waypoint to a given point in 3d space
+   3. Provide an interface that allows other scripts to get waypoint information from an index number: as our cars go around the track, they have a waypoint counter which could potentially be used with this function to establish where the current, next, or previous waypoints are.