Now that the target is completed, I can create a Prefab of this object so that I can quickly place targets in the level with all the functionality already in place.

# ## Optimizing Physics Using the Time Manager

Earlier, we talked about the physics causing the frame rate to drop. There are additional optimizations that can be done with physics. Rendering happens as fast as it can, and the rendering loop takes place all of the time. Physics needs to be constant, so a separate loop runs at constant speed and is calculated independently of the game's frame rate. Using the Time Manager, you can adjust the Fixed Timestep and Maximum Allowed Timestep as shown in Fig. 9.26.

![](bbox=[0.098, 0.294, 0.497, 0.466])

Essentially, the smaller the Fixed Timestep, expressed in milliseconds, the more accurate the physics will be but at a heavier cost to the CPU. The Maximum Allowed Timestep value, also specified in milliseconds, says that physics calculations won't run longer than the entered value. Basically, if your frame rate drops below this threshold, the physics will slow down in order to let the CPU catch up. Both these values can be used to stop your physics from dropping the frame rate too much, but at the cost of the quality of the physics simulation.

# ## Publishing Your Game

In this section, I want to take a look at the Player Settings for deploying your game in terms of creating Universal Builds. We'll then move on to optimizing your game. Over these next two sections, we will focus mainly on the Basic License version of Unity iOS as it's an affordable option for getting into game development. The Advanced License gives you a bit more control such as being able to optimize the Player Size as well as using Umbra Occlusion Culling.

# ## Player Settings

There are several important settings in the Player Settings. In Fig. 9.27, you can see the Player Settings. The Player Settings is where you set your Bundle Identifier, SDK version, Target IOS Version as well as application icons, splash images, and the default orientation.

![](bbox=[0.098, 0.481, 0.497, 0.95])