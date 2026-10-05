In the Hierarchy, check BobbleArena and check if you see the following in the Animator window:

![](bbox=[0.198, 0.143, 0.801, 0.393])

You'll see that the Walls animation is already present in the controller. Any new animation clips are added to the current animator controller automatically.

Each rectangle indicates an animation state:

+   - The green rectangle is the entry point of the animator.
- The orange rectangle indicates the default state; it's always played first.
- The arrows indicate transitions between states.

By scrolling your mouse wheel up, you can zoom in on the states. Likewise, scrolling down zooms out. Pressing and holding the middle mouse wheel allows you pan over the states. These shortcuts are useful when you have a lot of states onscreen at once.

Play your game and move the hero until you can see the lowered walls. The animation loops endlessly.

![](bbox=[0.343, 0.725, 0.656, 0.897])