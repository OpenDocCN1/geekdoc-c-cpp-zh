
## Part X: Dynamic Animation

Consider the motion of a simple yo-yo. Animating this motion with keys is fairly simple: Set rotation and position keys halfway through the animation and again at the end, and you're finished.

Now think of the forces controlling the yo-yo. Gravity causes the yo-yo to accelerate toward the ground, causing the string to unwind, which makes the yo-yo spin about its axis. When it reaches the end of the string, the rotation reverses and the yo-yo rises. Using Gravity and Motor Space Warps, you can simulate this motion, but setting the keys manually is probably easier for these few objects.

But before you write off dynamics, think of the motion of popcorn popping. With all the pieces involved, setting all the position and rotation keys would take a long time. For this system, using dynamics makes sense.

Dynamic tools let you specify objects to include in a simulation, the forces they interact with, and the objects to be involved in collisions. After the system is defined, the Dynamics utility automatically calculates the movement and collisions of these objects according to the forces involved, and then it sets the keys for you.

### Note

Max includes several different dynamic tools, including dynamic objects such as a spring and damper, dynamic material properties found in the Material Editor, specialized dynamic Space Warps, and the Dynamics utility. Before investing too much time in the Dynamics utility, please realize that for dynamic simulations, the reactor features are more robust and easier to set up. The Dynamics utility still exists only for backwards compatibility.

### Using reactor

The reactor plug-in was developed by a company named Havok. reactor is a complex piece of software with a huge assortment of features that enable you to define physical properties and forces and have the scene automatically generate the resulting animation keys as the objects interact while following the laws of physics.

### Note

Be aware that the reactor plug-in is different from the Reaction controller, discussed in Chapter 22, “Animating with Constraints and Simple Controllers.”

The reactor plug-in interface exists in the Utilities panel and is one of the default utilities, but you can also access it from the reactor menu and the reactor toolbar, shown in Figure 43.1. The reactor menu and the reactor toolbar provide a quick and easy way to access the various reactor elements. For example, clicking the Rope Collection button opens the Helper category in the Command Panel, selects the reactor subcategory, and selects the RP Collection button.

### FIGURE 43.1

Use the reactor toolbar to define physical object properties.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1109_0.png)

### The reactor process

Before getting into the details of reactor, I want to briefly explain the process involved in using reactor. reactor works with geometry that is defined with certain physical properties. After these properties are defined, the reactor engine can take over and determine how all the various objects interact with one another. In the reactor utility, you can select to use the reactor version 1 engine (Havok 1) or the reactor version 3 engine (Havok 3). Version 3 of the reactor engine is much more accurate and considerably faster than version 1, but if your simulation includes cloth, rope, or soft body objects, then you need to stick with version 1.

Within the Utilities panel are several rollouts of options for controlling the simulation. In the Preview & Animation rollout, you can set the simulation range, number of frames, and substeps per key. In the Havok 1 World rollout, you can set the global gravity values, the World Scale, and Collision Tolerance. The Add Deactivator option lets you remove objects from the simulation that are considered at rest. This keeps them from wiggling around, which happens when they are still part of the simulation. The Short and Long Frequency values help determine when an object is at rest.

If the Havok 3 option is selected, then you can choose to compute the object's motion on a Continuous basis or on a Discrete basis, which only checks the object motion at the beginning and end of each step and interpolates between these two states. You also can set a Maximum Linear Velocity for objects and a Stiffness value.

The Collisions rollout lets you specify how collisions are stored. By storing collisions, you can trigger an event to make particles show sparks, but enabling the storing of collisions can slow down a simulation. A window for Defining Collisions lets you ensure that certain objects won't collide and others will.

The Display panel lets you specify a camera, clipping planes, lights, and textures to use in the Preview window for displaying the simulated objects.

The Utils panel includes an Analyze World button that you can use before starting a simulation. There are also controls for reducing the total number of keys and for testing the convexity of objects.

Defining geometry with physical properties happens in several different ways. Objects can be added to a collection. A collection is a type of reactor object that has several inherited physical properties, such as a Rigid Body collection. Objects can also be linked with reactor objects such as a Spring or Motor. These objects are affected by forces that are preset for the different reactor objects. Finally, you can set properties using the Object Property rollout, which lets you define properties such as mass, friction, and elasticity. After all the objects are defined and attached to the correct reaction collection or object, you can open a Preview window that lets you see how the object will react under the current forces. You can also interactively play with the various objects in the Preview window.

When you're comfortable with the animation, the Animation reactor Create Animation menu command creates all the keys for the animation sequence.

### Tutorial: Filling a glass bowl

Imagine trying to animate a bunch of marbles falling into a glass bowl. If you were using keyframes, determining whether an object overlaps another would be difficult, but with this quick example you see the power of reactor.

To animate marbles falling into a glass bowl, follow these steps:

- 1. Open the Glass bowl of marbles.max file from the Chap 43 directory on the DVD.
  This file includes a glass bowl and several marbles positioned above its opening.

- 2. Select Animation reactor Create Objects Rigid Body Collection, and click in the Front viewport to create the icon. In the RB Collection Properties rollout, click the Add button to open the Select Objects dialog box.

- 3. In the Select Objects dialog box, click the Select All button and then the Select button to select and make all objects in the scene rigid body objects. Then right-click to exit Rigid Body Collector mode.

- 4. Select the Box and sphere objects that make up the floor and bowl, select Animation → reactor → Open Property Editor, and enable the Unyielding option. This prevents these two objects from moving. Then select the sphere bowl object, and enable the Concave Mesh option.

- 5. Select all the marble objects in the scene, and set the Mass value to 5.0.

- 6. Then select Animation → reactor → Preview Animation to open the Preview window, and press the P key to start the simulation.

- 7. If the animation looks fine, select Animation → reactor → Create Animation to have reactor compute all the keys.

Figure 43.2 shows the bowl full of marbles positioned using reactor.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1111_0.png)

reactor can compute all the collisions between all these marbles.

### Using reactor Collections

One of the first steps in creating with a simulation is defining the object properties. For example, a simple sphere object in Max could represent a bowling ball, an orange, or a tennis ball. Each of these objects responds very differently when being animated to drop on the floor.
