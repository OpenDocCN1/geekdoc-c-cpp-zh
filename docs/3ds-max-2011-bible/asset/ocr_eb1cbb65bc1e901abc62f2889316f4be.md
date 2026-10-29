# FIGURE 44.2

Using precomputed hair can save you a bundle of time when rendering.

![](bbox=[0.06, 0.19, 0.82, 0.6])

# Simulating Cloth Dynamics

Hair isn't the only system that has the benefit of dynamic motion. Cloth also can benefit from dynamic simulations. The steps for setting up a dynamic cloth simulation are similar to those for hair. First, apply the cloth modifier and define the cloth properties and the environmental forces acting on the cloth. Then run the simulation.

# Defining cloth properties and forces

To add objects (both cloth and collision objects) to the simulation, click the Object Properties button in the Object rollout. This opens the Object Properties dialog box, shown in Figure 44.3. Clicking the Add Objects button lets you select scene objects to add to the simulation. Only objects added to the scene are included in the simulation. If an object isn't added, it's ignored. All objects added to the simulation are added to the list at the left. Selected objects in the list can be specified as Inactive, Cloth, or Collision Object. For Cloth and Collision Objects, you can set properties. You can also load and save cloth presets. Cloth presets are saved using the .sti extension.

# Tip

If the cloth tends to pass through objects, then you can increase the Offset value for the collision object.