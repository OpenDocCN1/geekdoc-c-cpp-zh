# Tutorial: Firing at a fleeing spaceship

Well, it is about time for a space scene, and we all know that lots of particles float around out in space—stars, asteroids, comets, and so forth. It's all great stuff to animate. For this scene, you use the Particle Flow feature to fire laser blasts on a fleeing spaceship.

To use Particle Flow to fire on a fleeing spaceship, follow these steps:

+   1. Open the Fleeing spaceship.max file from the Chap 41 directory on the DVD.
+   This file includes a spaceship model created by Viewpoint Datalabs that has been animated as if it were fleeing
+   2. Select Create→ Particles→ Particle Flow Source, and drag in the Front viewport to create the emitter. With the Select and Move (W) button selected, move the emitter until it is aligned with the end of the laser gun. Then click the Select and Link button, and drag from the emitter to the gun object to bind the emitter to the gun.
+   The emitter now moves with the animated laser gun.
+   3. With the Particle Flow Source icon selected, open the Modify panel and click the Particle View button in the Setup rollout (or press the 6 key) to open the Particle View interface.
+   4. In the Event01 node, select the Birth 03 event; in the Parameters panel, set the Emit Stop to 100 and the Amount to 50. This produces a laser blast every two frames. Click the blue dot in the lower-right corner of the Event node, and select a red color from the Color Selector that appears.
+   5. Select Create→ Standard Primitives→ Cylinder, and drag in the Front viewport to create a Cylinder object. In the Hierarchy panel, select the Affect Pivot Only button and rotate the Cylinder's Pivot Point until its Y-axis points at the spaceship. Then in the Particle View window, drag the Shape Instance event from the depot and drop it on top of the Shape event in the Event 01 node. This replaces the Shape event with a Shape Instance event. In the Parameters rollout, click the Particle Geometry Object button and select the Cylinder object. Select the Rotation event, and delete it with the Delete key.
+   6. Select Create→ Space Warps→ Deflectors→ SOmniFlect, and drag in the Top viewport to create a spherical deflector that encompasses the spaceship. Click the Select and Non-Uniform Scale button, and scale the X- and Z-axes until the deflector just fits around the spaceship. Then link the deflector Space Warp to the spaceship.
+   7. In the Particle View window, drag the Collision event from the depot to the bottom of the Event 01 node. In the rollout, below the Deflectors list, click the Add button and select the SOmniFlect01 object surrounding the spaceship.
+   8. Drag a Spawn event from the depot to the event display, and then connect the Collision event by dragging from its output to the input of the new Spawn event. Then click the color for the new event particles, and change it to orange. Select the Spawn 01 event, enable the Delete Parent option, and set the Offspring to 200 and the Variation % to 20. Then set the Inherited % to 50 with a Variation of 30.
+   9. Drag the Delete event to the bottom of the Event 02 node, select the By Particle Age option, and set the Life Span to 20 and the Variation to 30. Drag a Shape event to the Event 02 node, and set the Shape to Sphere and the Size to 0.5.
+   10. Finally, click the Play button to see the resulting animation.

Figure 41.22 shows the final Particle View flow, and Figure 41.23 shows a frame of the animation in the viewport. You can still do several things to improve this animation, such as adding a Glow Render Effect to the laser blasts and using the Particle Age material with some transparency to improve the explosion's look.