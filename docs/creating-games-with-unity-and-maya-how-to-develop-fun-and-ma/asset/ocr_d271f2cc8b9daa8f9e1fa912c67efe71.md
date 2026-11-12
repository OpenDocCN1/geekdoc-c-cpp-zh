# Final Test

+   - **Step 49:** Make sure the Scene-Hallway is set up appropriately (Hallway_BakedGroup deactivated, Hallway_UnBaked activated, etc.).
+   - **Step 50:** Open Scene-Opening.
+   - **Step 51:** Play the game. Be sure to die and see if Scene-ClosingFail indeed pops up. Also, get a bit damaged and make sure that the health state transfers from level to level.
+   - **Step 52:** Celebrate! The game is done; or at least started.

# Conclusion

So there’s the game. There is still one vital step before we can share it—we need to “build” it, or more accurately, “create a build.” This will produce the actual product that others can launch. Additionally, we’ll need to create a build to make sure that the game does indeed quit. In the next chapter we’ll wrap up with a brief discussion of builds.

But the basic functionality is complete. This, of course is just the beginning. Be sure to be thinking about how the game might be expanded, and while these assets are still familiar to you, add new challenges to it. There are lots of doors unopened, and lots of mini-games that could still be implemented.

# Homework and Challenges

+   - **Challenge 1:** The EndgameTriggerScript gets the job done, but can this be polished some more? Maybe a fade (Hint: Consider a GUITexture (all black) with an animated iTween.FadeTo attached to it)? Or an additional camera with some animation to ease us out of the scene? How could these be integrated into the EndgameTriggerScript? Can this be expanded to allow for smoother transitions into Scene-Closing?
+   - **Challenge 2:** The camera countdown works, but it could let the player know better the consequences of not taking out the cameras. Create a mechanism that alerts the player that if he doesn’t destroy the camera that's seen him, the authorities will descend and catch him.
+   - **Challenge 3:** At this point the game can be ended by losing (either by the cameras catching you or by the health hitting 0). However, what if the player wants to quit? On a Mac, Command-Q will stop the game, and on a PC, Alt+F4 will do the same thing, but this isn’t something that most PC users instinctively know. The first impulse is to press the Esc key. Create a new script that listens for the key input of the Esc key (Hint: Keycode.Escape), and then quits the application (Application.Quit). Where should this script be housed?
+   - **Challenge 4:** The steam emitters use a tool that constantly checks for the distance between fpcAegis and the emitter (and turns the steam emitter on if he is within a certain range). Unfortunately, this is very expensive to have a bunch of objects checking every single frame what their distance is to another object. How could this be instigated in a more efficient way (hint: think collider triggers….).