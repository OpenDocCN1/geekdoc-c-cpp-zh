The differences between the Blizzard and Super Spray parameters include dimensions for the Blizzard icon. In the Particle Generation rollout, you'll find values for Tumble and Tumble Rate. Another difference is the Emitter Fit Planar option under the Material Mapping group of the Particle Type rollout. This option sets particles to be mapped at birth, depending on where they appear on the emitter. The other big difference is that the Blizzard particle system has no Bubble Motion rollout, because snowflakes don't make very good bubbles. Finally, you'll find a different set of presets in the Load/Save Presets rollout, including Blizzard, Rain, Mist, and Snowfall.

# Using the PArray Particle System

The PArray particle system is a unique particle system. It emits particles from the surface of a selected object. These particles can be emitted from the object's surface, edges, or vertices. The particles are emitted from an object separate from the emitter icon.

The PArray particle system includes many of the same rollouts as the Super Spray particle system. The PArray particle system's emitter icon is a cube with three tetrahedron objects inside it. This system has some interesting parameter differences, starting with the Basic Parameters rollout, shown in Figure 41.15.

# FIGURE 41.15

The Basic Parameters rollout for the PArray particle system lets you select the location where the particles form.

![](bbox=[0.02, 0.65, 0.24, 0.85])

In the PArray system, you can select separate objects as emitters with the Pick Object button. You also can select the location on the object where the particles are formed. Options include Over Entire Surface, Along Visible Edges, At All Vertices, At Distinct Points, and At Face Centers. For the At Distinct Points option, you can select the number of points to use.

The Use Selected SubObject option forms particles in the locations selected with the Pick Object button, but only within the subobject selection passed up the Stack. This is useful if you want to emit particles only