
The Min and Max Fragment Size values set the minimum and maximum number of faces caused by the explosion.

The Gravity value determines the strength of gravity and can be positive or negative. Gravity always points toward the world's Z-axis. The Chaos value can range between 0 and 10 to add variety to the explosion. The Detonation value is the number of the frame where the explosion should take place, and the Seed value alters the randomness of the event. Figure 42.16 shows a frame of an explosion produced by the Bomb Space Warp.

## FIGURE 42.16

The Bomb Space Warp causes an object to explode.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1102_0.png)

## Note

The Bomb Space Warp is seen over time. At frame 0, the object shows no effect.

## Tutorial: Blowing a dandelion puff

You can use Space Warps with other types of objects besides particle systems. The Scatter object, for example, can quickly create many unique objects that can be controlled by a Space Warp. In this tutorial, you create a simple dandelion puff that can blow away in the wind.

To create and blow away a dandelion puff, follow these steps:

- 1. Open the Dandelion puff.max file from the Chap 42 directory on the DVD.
- This file includes a sphere covered with a Scatter compound object representing the seeds of a dandelion.

## Cross-Ref

For details on the Bend, Noise, Skew, Taper, Twist, and Stretch modifiers and their parameters, see Chapter 11, “Introducing Modifiers and Using the Modifier Stack.” ■

## FIGURE 42.18

The Modifier-Based Space Warps: Bend, Noise, Skew, Taper, Twist, and Stretch

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1104_0.png)

These Space Warps include a Gizmo Parameters rollout with values for the Length, Width, and Height of the gizmo. You can also specify the deformation decay. The Decay value causes the Space Warp’s effect to diminish with distance from the bound object.

You can reposition the Modifier-Based Space Warp’s gizmo as a separate object, but the normal modifiers require that you select the gizmo subobject to reposition it. Unlike modifiers, Space Warps don’t have any subobjects.

## Combining Particle Systems with Space Warps

To conclude this chapter, you’ll look at some examples that use Space Warps along with particle systems. With all these Space Warps and their various parameters combined with particle systems, the possibilities are endless. These examples are only a small representation of what is possible.

## Tutorial: Shattering glass

When glass shatters, it is very chaotic, sending pieces in every direction. For this tutorial, you shatter a glass mirror on a wall. The wall keeps the pieces from flying off, and most pieces fall straight to the floor.

To shatter glass, follow these steps:

- 1. Open the Shattering glass.max file from the Chap 42 directory on the DVD.
- This file includes a simple mirror created from patch grid objects. The file also includes a simple sphere that is animated striking the mirror.

- 2. Select the Create ⇨ Particles ⇨ PArray menu command. Then drag in the Front viewport to create the PArray icon. In the Basic Parameters rollout, click the Pick Object button and select the first patch object. In the Viewport Display section, select the Mesh option. In the Particle Generation rollout, set the Speed and Divergence to 0. Also set the Emit Start to 30 and the Life value to 100, so it matches the last frame. In the Particle Type rollout, select the Object Fragments option, and
set the Thickness to 1.0. Then in the Object Fragment Controls section, select the Number of Chunks option with a Minimum value of 30. In the Rotation and Collision rollout, set the Spin Time to 100 and the Variation to 50.
These settings cause the patch to emit 30 object fragments with a slow, gradual rotation.

- 3. Select the Space Warps category button, and choose the Forces subcategory from the drop-down list. Click the PBomb button, and create a PBomb Space Warp in the Top view; then center it above the Mirror patch. In the Modify panel, set the Blast Symmetry option to Spherical with a Chaos value of 50 percent. Set the Start Time to 30 with a Strength value of 0.2. Then click the Bind to Space Warp button, and drag from the PBomb Space Warp to the PArray icon.

- 4. Select the Create Space Warps Forces Gravity menu command, and drag in the Front viewport to create a Gravity Space Warp. Position the Gravity Space Warp so that the icon arrow is pointing down in the Front viewport. In the Modify panel, set the Strength value to 0.1. Then bind this Space Warp to the PArray icon.

- 5. Select the Create Space Warps Deflectors PDynaFlect menu command. Drag this Space Warp in the Top view, and make it wide enough to be completely under the mirror object. Rotate the PDynaFlect Space Warp so that a single large arrow is pointing up at the mirror. Position it so that it lies in the same plane as the plane object that makes up the floor. In the Modify panel, set the Reflects value to 100 percent and the Bounce value to 0. Bind this Space Warp to the PArray as well; this keeps the pieces from falling through the floor. Press Play to see the results.

Figure 42.19 shows the mirror immediately after being struck by a ball.

## FIGURE 42.19

A shattering mirror

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1105_0.png)

## Summary

Space Warps are useful for adding forces and effects to objects in the scene. Max has several different types of Space Warps, and most of them can be applied only to certain object types. In this chapter, you learned the following:

- How to create Space Warps
- How to bind Space Warps to objects
- How to use all the various Space Warps in several subcategories
- How to combine Space Warps with particle systems to shatter glass and explode a planet

You can have Max dynamically compute all the animation frames in a scene using the physics-based reactor engine, which is covered in the next chapter.

## Simulating Physics-Based Motion with reactor

When you speak of reactor in Max, you really are speaking of physics. Physics is one of the coolest arms of science because it deals with the science of matter and energy and includes laws that govern the motions and interactions between objects. For animators, this is great news because what you are trying to do is to animate the motions and interactions between objects.

So, should all animators study physics? The answer is absolutely. Understanding these laws through study and experience will sharpen your animating skills. But you can also take advantage of the work that other animators have done in understanding the laws of physics and turning them into a product that ships with Max. The other animators are a group called Havok, and the product is reactor.

The Havok physics engine included in Max is the same engine commonly used in games to simulate game-world physics such as the reactions in Valve’s Half Life 2.

Using reactor, you can simulate many physical properties and automatically capture keyframes as the objects interact. It’s like getting a physics degree for free.

The reactor menu includes everything you need to access the reactor physics simulation engine. With reactor, you can define objects as rigid bodies like chairs or bowling balls or as soft bodies like stuffed animals. You can also define specialized objects, including cloth and rope.

After physical properties are defined, you can define physical forces to act on these objects and simulate the resulting animation. Not only does reactor make difficult physical motions realistic, but it also is fun to play with.

## Understanding Dynamics

Dynamics is a branch of physics that deals with forces and the motions they cause, and regardless of your experience in school, physics is your friend—especially in the world of 3D. Dynamics in Max can automate the creation of animation keys by calculating the position, rotation, and collisions between objects based on physics equations.

## IN THIS CHAPTER

- Exploring the reactor utility
- Learning to use collections
- Applying reactor modifiers
- Assigning object properties
- Working with reactor objects
- Previewing animations
