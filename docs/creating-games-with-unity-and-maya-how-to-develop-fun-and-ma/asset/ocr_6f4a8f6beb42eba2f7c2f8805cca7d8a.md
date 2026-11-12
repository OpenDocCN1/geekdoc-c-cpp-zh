Preferences. Go to the Time Slider section and change the Playback Speed option to real time.

# Conclusion

Lots left to do. This is a seven-step tutorial that will probably take you a couple of hours to complete. Just animating a game character is worth an entire book on its own, so if you haven't a lot of animation experience, don't sweat it. Get a bit of animation in there and call it good; or feel free to use the AegisChung-SingleMesh-Animated.mb file to use for the next tutorial.

# Tutorial 10.4: Getting Animated Characters to Unity

In previous chapters I've argued passionately for manually exporting assets from Maya for consumption in Unity. Because the topic's been beaten pretty hard, I'll avoid pontificating too much in this chapter; however, it's important to note that for game characters manual export carries some real benefits.

The most important benefit has to do with how IK is calculated. In our current rig and animation, the rotation of all the leg joints has been done via IK chains, and specifically with the translate keyframes of the foot handles. These calculations are dynamic within Maya, meaning that each frame isn't just seen as an incremental rotation difference, as it is in the upper body, but a much more complex calculation of incremental difference in translation of the IK handle, and then another calculation of how to rotate the involved joints to solve for this IK handle location. If you've used different 3D applications, you know that IK can work differently and have different personalities across different programming solutions. It's no different in the Maya/Unity marriage; and IK might solve great in Maya and not solve quite so nicely in Unity. Especially if using things like pole vectors, Unity doesn't always see the IK the same way Maya does.

To help alleviate this, we'll look at baking our animation into all joint rotation procedures. The IK will then not actually be calculated by Unity at all—Unity will simply see joint rotation keyframes.

+   1. **Save a backup version of the file.** Save as `Aegis_Chung-Animated.mb`.

# Why?

We are about to bake the animation. Once the animation is baked, it is very difficult to do any sort of meaningful editing. It's always good to have a nonbaked version of the file. You may never need to go back to this unbaked version, but if you need it and don't have it, the animation practically needs to be started over.

+   2. **Bake the animation.** In the Outliner select AC_Root. Then choose Edit>Keys>Bake Simulation (Options). In the Bake Simulation Options