# THE GAMELOADING STATE

The GameLoading state, as shown in Figure 17.1, is the first state the game enters.

![](bbox=[0.102, 0.153, 0.574, 0.513])

**Figure 17.1**
Game Loading.
© 2014 Timothy Wright.

This state loads all the game resources using the thread pool method demonstrated in Chapter 12, “Threads.” The items loaded are:

+   - Background image
+   - High score file
+   - Asteroid models and sprites
+   - Ship model and sprites
+   - Thruster, explosions, and missile sounds

The updateObjects() method checks the progress of all the resource loading and updates the load percentage. The render() method draws the loading progress. When all the game resources are loaded, the state transitions to the PressSpaceToPlay state. Remember, for the ambient sound, there are differences depending on which version of java you are using.