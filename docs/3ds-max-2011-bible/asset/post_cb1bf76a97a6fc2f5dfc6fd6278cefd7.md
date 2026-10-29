
## Part IX: Working with Characters

+   2. With the arm skin selected, choose the Modifiers > Animation > Skin Morph menu command to apply the Skin Morph modifier on top of the Skin modifier.
+   3. In the Parameters rollout, click the Add Bone button and select the forearm bone object.
+   The bone object is added to the Skin Morph list in the Parameters rollout.
+   4. Select and rotate the forearm bone to the location where the deformation is at its maximum. Then select the bone object from the list in the Parameters rollout, and click the Create Morph button in the Local Properties rollout. In the Morph Name window name the morph Bulging bicep.

### Tip

The forearm bone can be hard to see under the skin, but you can always select the bone using the Select by Name dialog box, which is opened by pressing H.

+   5. In the Local Properties rollout, click the Edit button. This enables the Points subobject mode. Then enable the Edge Limit option in the Selection rollout, so the vertices on the forearm aren't accidentally selected. Drag over the points on the front of the bicep muscle in the Left viewport, and enable the Use Soft Selection option in the Selection rollout. Set the Radius value to 0.5, and scale the points to the right in the Left viewport to form a bulge. Click the Edit button again to exit Edit mode.
+   6. Select and rotate the forearm bone to see the bulging bicep muscle.
+   Figure 40.10 shows the arm muscle as it bulges along with the rotating forearm.

### FIGURE 40.10

Using the Skin Morph, you can set a muscle to bulge as the forearm is rotated.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1051_0.png)

## Using Character Animation Techniques

When it comes to character animation, several techniques can really help. Keeping these points in mind as you animate characters can make a difference:

+   - Use Biped: Manual rigging is useful for those cases where Biped won’t work, but the tools and features found in Biped make it silly to look elsewhere for human characters.
+   - Use dynamics: Dynamic packages like reactor can provide incredibly realistic motion based on physical properties. Learning to use this powerful tool for even the most basic animation sequences is worth the effort.
+   - Learn by example: If you’re working on a cartoon character, then by all means, watch cartoons. Traditional cartoons understand and invented the language of cartoon motion, including squash and stretch, exaggerated motion, or scaling eyes large to indicate surprise. If your character motion is more realistic, find the motion, videotape it, and watch it over and over to catch the subtle secondary motion.
+   - Use background animations: The Viewport Background can load animation clips, which can make positioning characters to match real motion easy. This is a poor man’s motion capture system.
+   - Include secondary motion: The primary motion of a character is often the main focus, but you can enhance the animation by looking for secondary motion. For example, when a person walks, you see his legs take the steps and his arms moving opposite the legs’ motion, but secondary motion includes his hair swishing back and forth and shoelaces flopping about.
+   - Use the Flex modifier: The Flex modifier gives soft bodies, such as tails, hair, ears, and clothing, the realistic secondary motion needed to make them believable.
+   - Use the Morph modifier: The Morph modifier can be used to morph a character between two poses or to morph its face between the different phonemes as the character talks.
+   - Use IK: The next chapter covers this in detail, but here’s a quick tip: Having a character move by positioning its foot or hand is often much easier than pushing it into position.
+   - Use the Spring Controller: Another good way to get secondary motion is to use the Spring Controller. This controller works well with limbs.
+   - Add randomness with the Noise Controller: Often, perfect animation sequences don’t look realistic, and using the Noise Controller can help to make a sequence look more realistic, whether the Noise Controller is applied to a walking sequence or to the subtle movement of the eyes.
+   - Use manipulators: Manipulators can be created and wired to give you control over the animation values of a single motion, such as opening and closing the character’s eyes.

## Summary

Characters are becoming more and more important in the Max world and can be saved as separate files just like Max scene files. Combining a detailed skin mesh with a skeletal biped lets you take advantage of Character Studio’s unique animation features. This chapter covered the following topics:

+   - Designing your character before building
+   - Working with the Skin modifier
+   - Reusing animations with Skin Wrap
+   - Bulging muscles with Skin Morph

In Part X, "Dynamic Animation," you’ll examine the dynamic animation features, starting with particle systems.

## Part X

## Dynamic Animation

### IN THIS PART

+   - **Chapter 41**
+     Creating Particles and Particle Flow
+   - **Chapter 42**
+     Using Space Warps
+   - **Chapter 43**
+     Simulating Physics-Based Motion with reactor
+   - **Chapter 44**
+     Animating Hair and Cloth

## Creating Particles and Particle Flow

Every object that you add to the scene slows down Max to a small degree because Max needs to keep track of every object. If you add thousands of objects to a scene, not only does Max slow down noticeably, but also the objects become difficult to identify. For example, if you had to create thousands of simple snowflakes for a snowstorm scene, the system would become unwieldy, and the number wouldn’t get very high before you ran out of memory.

Particle systems are specialized groups of objects that are managed as a single entity. By grouping all the particle objects into a single controllable system, you can easily make modifications to all the objects with a single parameter. This chapter discusses using these special systems to produce rain and snow effects, fireworks sparks, sparkling butterfly wings, and even fire-breathing dragons.

## Understanding the Various Particle Systems

A particle is a small, simple object that is duplicated en masse, like snow, rain, or dust. Just as in real life, Max includes many different types of particles that can vary in size, shape, texture, color, and motion. These different particle types are included in various particle systems.

When a particle system is created, all you can see in the viewport is a single gizmo known as an emitter icon. An emitter icon is the object (typically a gizmo, but it can be a scene object) where the particles originate. Selecting a particle system gizmo makes the parameters for the particle system appear in the Modify panel.

Max includes the following particle systems:

+   - **Particle Flow Source:** Particles that can be defined using the Particle Flow window and controlled using actions and events.
+   - **Spray:** Simulates drops of water. These drops can be Drops, Dots, or Ticks. The particles travel in a straight line from the emitter’s surface after they are created.

| In This Chapter |
|---|
| Understanding the various particle systems |
| Creating a particle system |
| Using the Spray and Snow particle systems |
| Using the Super Spray and Blizzard particle systems |
| Working with MetaParticles |
| Using an object as an emitter |
| Using particle system maps |
| Using the Particle Flow interface |

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1056_0.png)

## Part X: Dynamic Animation

+   - Snow: Similar to the Spray system, with the addition of some fields to make the particles Tumble as they fall. You also can render the particles as Six Pointed shapes that look like snowflakes.
+   - Blizzard: An advanced version of the Snow system that can use the same mesh object types as the Super Spray system. Binding the system to the Wind Space Warp can create storms.
+   - PArray: Can use a separate distribution object as the source for the particles. For this system, you can set the particle type to Fragment and bind it to the PBomb Space Warp to create explosions.
+   - PCloud: Confines all generated particles to a certain volume. A good use of this system is to reproduce bubbles in a glass or cars on the road.
+   - Super Spray: An advanced version of the Spray system that can use different mesh objects, closely packed particles called MetaParticles, or an instanced object as its particles. Super Spray is useful for rain and fountains. Binding it to the Path Follow Space Warp can create waterfalls.

## Creating a Particle System

You can find all the various particle systems under the Create panel and also in the Create menu. To access these systems, click the Geometry category and select the Particle Systems subcategory from the drop-down list. All the particle systems then appear as buttons. Or you can select the Create→Particles menu.

With the Particle Systems subcategory selected, click the button for the type of particle system that you want to use, and then click in a viewport to create the particle system emitter icon. The emitter icon is a gizmo that looks like a plane or a sphere and that defines the location in the system where the particles all originate. Attached to the icon is a single line that indicates the direction in which the particles move when generated. This line points by default toward the construction grid’s negative Z-axis when first created. Figure 41.1 shows the emitter icons for each particle system type including, from left to right, Particle Flow Source; Super Spray; Spray, Snow, and Blizzard (which all have the same emitter icon); PArray; and PCloud.

### FIGURE 41.1

The emitter icons for each particle system type

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1057_0.png)

You can transform these icons using the standard transform buttons on the main toolbar. Rotating an emitter changes the direction in which the particles initially move.

After an icon is created, you can set the number, shape, and size of the particles and define their motion in the Parameter rollouts. To apply a material to the particles, simply apply the material to the system’s icon. This material is applied to all particles included in the system.

### Note

Be aware that the particles are displayed as simple objects such as ticks or dots in the viewports. To see the actual resulting particles, you need to render the scene file.

You can set the parameters for the Max particle systems in the Create panel when they are first created or in the Modify panel at any time. The simpler systems, Spray and Snow, have a single Parameters rollout, but
