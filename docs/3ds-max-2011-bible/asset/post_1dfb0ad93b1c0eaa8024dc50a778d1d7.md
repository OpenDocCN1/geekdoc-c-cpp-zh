
In the Particle Motion group, the Speed value determines the initial speed and direction of particles. The Variation value alters this initial speed as a percentage of the Speed value. A high Variation value results in particles with all sorts of different speeds.

### Note

Be sure to use the Variation values liberally to get more realistic particle behavior. ■

In the Particle Timing group, you can set when the emitting process starts and stops. Using the Display Until value, you also can cause the particles to continue displaying after the emitting has stopped. The Life value is how long particles stay around, which can vary based on another Variation setting.

When an emitter is animated (such as moving back and forth), the particles can clump together where the system changes direction. This clumping effect is called puffing. The Subframe Sampling options help reduce this effect. The three options are Creation Time (which controls emitting particles over time), Emitter Translation (which controls emitting particles as the emitter is moved), and Emitter Rotation (which controls emitting particles as the emitter is rotated). All three options can be enabled, but each one that is enabled adds the computation time required to the render.

### Note

The Subframe Sampling options increase the rendering time and should be used only if necessary. ■

You can specify the particle size along with a Variation value. You also can cause the particles to grow and fade for a certain number of frames.

The Seed value helps determine the randomness of the particles. Clicking the New button automatically generates a new Seed value.

### Note

If you clone a particle system and each system has the same Seed value, then the two systems will be exactly the same. Two cloned particle systems with different Seed values will be unique. ■

## Particle Type rollout

The Particle Type rollout, shown in Figure 41.6, lets you define the look of the particles. At the top of the rollout are three Particle Type options: Standard Particles, MetaParticles, and Instanced Geometry.

### FIGURE 41.6

The Particle Type rollout (shown in four parts) lets you define how the particles look.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1062_0.png)

## Part X: Dynamic Animation

If you select Standard Particles as the particle type, you can select which geometric shape you want to use from the Standard Particles section. The options are Triangle, Special, Constant, SixPoint, Cube, Facing, Tetra, and Sphere.

The Special type consists of three intersecting planes, which are useful if you apply maps to them. The Facing type is also useful with maps; it creates a simple square face that always faces the viewer. The Constant type maintains the same pixel size, regardless of the distance from the camera or viewer. The Six Point option renders each particle as a 2D six-pointed star. All other types are common geometric objects.

## Tutorial: Creating a fireworks fountain

For an example of the Super Spray particle system, you create a fireworks fountain. Fireworks are essentially just lots of particles with a short life span and a high amount of self-illumination. (Tell yourself that the next time you watch a fireworks display.)

### Cross-Ref

The ready-made material for this example uses the Glow Render effect to make the particles glow. You can learn more about render effects in Chapter 46, “Using Atmospheric and Render Effects.”

To create a fireworks fountain using a particle system, follow these steps:

- 1. Open the Fireworks fountain.max file from the Chap 41 directory on the DVD.
This file includes a simple fountain base and the Gravity space warp to cause the particles to curve back toward the ground.

### Tip

Some of the most amazing special effects are made possible by combining particle systems with Space Warps.

- 2. Select the Create Particles Super Spray menu command, drag in the Top view, and position the system at the top of the cylinder with the direction arrow pointing toward the sky.

- 3. Open the Modify panel, and set the Off Axis Spread to 45 and the Off Plane Spread to 90. In the Particle Generation rollout, set the Total of particles to 2000 with a Speed of 20 and a Variation of 100. Set the Emit Start to 0 and the Emit Stop to 100. Set the Display Until to 100 and the Life to 25 with a Variation of 20. The Size of the particles should be 5.

- 4. Open the Material Editor (by pressing the M key), and select the first sample slot. This slot includes a material named Spark. Drag the material from the Material Editor to the particle system’s icon.

- 5. Select the Super Spray icon, right-click it to open the pop-up menu, and select the Properties menu option. In the Object Properties dialog box, select the Object Motion Blur option.

### Caution

When viewing the animation, maximize a single viewport. If Max tries to update all four viewports at once with this many particle objects, the update is slow. The shortcut to maximize the viewport is Alt+W.

### FIGURE 41.7

The Super Spray particle system is used to create fireworks sparks.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1064_0.png)

## Tutorial: Adding spray to a spray can

The Super Spray particle system is complex enough to warrant another example. What good is a spray can without any spray? In this tutorial, you create a spray can model and then use the Super Spray particle system to create the spray coming from it.

To create a stream of spray for a spray can, follow these steps:

- 1. Open the Spray can.max file from the Chap 41 directory on the DVD. This file includes a simple spray can object created using a cylinder for the can base and the nozzle and a lathed spline for the top of the can.

- 2. Select the Particle Systems subcategory button from the drop-down list, and click the Super Spray button. Drag in the Top viewport to create the Super Spray icon, and position it at the mouth of the nozzle.

- 3. In the Basic Parameters rollout, set the Off Axis Spread to 20 and the Off Plane Spread to 90. In the Particle Generation rollout, set the Emit Rate to 1000, the Speed to 20, and the Life to 30. Set the Size of the particles to 5.

- 4. Open the Material Editor (by pressing M), and select the material named Spray Mist. Then drag this material onto the Super Spray icon to apply this material to the Super Spray particle system.

### FIGURE 41.8

Using a mostly transparent material, you can create a fine mist spray.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1065_0.png)

## Using the MetaParticles option

The MetaParticles option in the Particle Type rollout makes the particle system release Metaball objects. Metaballs are viscous spheres that, like mercury, flow into each other when close. These particles take a little longer to render but are effective for simulating water and liquids. The MetaParticles type is available for the Super Spray, Blizzard, PArray, and PCloud particle systems.

Selecting the MetaParticles option in the Particle Types section enables the MetaParticle Parameters group. In this group are options for controlling how the MetaParticles behave. The Tension value determines how easily objects blend together. MetaParticles with a high tension resist merging with other particles. You can vary the amount of tension with the Variation value. The Tension value can range between 0.1 and 10, and the Variation can range from 0 to 100 percent.

Because MetaParticles can take a long time to render, the Evaluation Coarseness settings enable you to set how computationally intensive the rendering process is. This can be set differently for the viewport and the renderer—the higher the value, the quicker the results. You also can set this to Automatic Coarseness, which automatically controls the coarseness settings based on the speed and ability of the renderer. The One Connected Blob option speeds the rendering process by ignoring all particles that aren’t connected.

## Tutorial: Spilling soda from a can

MetaParticles are a good option to use to create drops of liquid, like those from a soda can.

To create liquid flowing from a can, follow these steps:

- 1. Open the MetaParticles from a soda can.max file from the Chap 41 directory on the DVD. This file includes a soda can model created by Zygote Media positioned so the can is on its side.

- 2. Select the Create Particles Super Spray menu command, and drag the icon in the Front viewport. Position the icon so that its origin is at the opening of the can and the directional vector is pointing outward.
