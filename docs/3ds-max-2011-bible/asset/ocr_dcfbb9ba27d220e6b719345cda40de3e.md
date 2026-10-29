# FIGURE 41.7

The Super Spray particle system is used to create fireworks sparks.

![](bbox=[0.02, 0.23, 0.5, 0.62])

# Tutorial: Adding spray to a spray can

The Super Spray particle system is complex enough to warrant another example. What good is a spray can without any spray? In this tutorial, you create a spray can model and then use the Super Spray particle system to create the spray coming from it.

To create a stream of spray for a spray can, follow these steps:

+   1. Open the Spray can.max file from the Chap 41 directory on the DVD. This file includes a simple spray can object created using a cylinder for the can base and the nozzle and a lathed spline for the top of the can.

+   2. Select the Particle Systems subcategory button from the drop-down list, and click the Super Spray button. Drag in the Top viewport to create the Super Spray icon, and position it at the mouth of the nozzle.

+   3. In the Basic Parameters rollout, set the Off Axis Spread to 20 and the Off Plane Spread to 90. In the Particle Generation rollout, set the Emit Rate to 1000, the Speed to 20, and the Life to 30. Set the Size of the particles to 5.

+   4. Open the Material Editor (by pressing M), and select the material named Spray Mist. Then drag this material onto the Super Spray icon to apply this material to the Super Spray particle system.

Figure 41.8 shows the fine spray from an aerosol can.