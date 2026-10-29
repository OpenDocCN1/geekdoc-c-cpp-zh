# Part X: Dynamic Animation

7. Drag the Find Target action from the Depot pane, and drop it at the bottom of the Event01 node. This adds a new Find Target icon to the viewports. Select the Find Target icon in the viewports, and move it to the lantern flame’s position. Select Group to Attach, and click the lantern object to add the Find Target icon to the lantern group. This makes the target move with the lantern. Enable the Use Cruise Speed option, and then set the Speed to 1000 with a Variation of 50 and the Accel Limit to 5000 with an Ease % of 50. You also need to enable the Follow Target Animation option.

8. Drag the Material Dynamic from the Depot pane to the Event Display pane, and drop it outside the Event01 node to create a new node called Event02. In the Parameters pane, enable the Assign Material button and click the material button. Select the Flash material from the Material/Map Browser (select the Material Editor option to see the sample slot materials). Then drag a wire from Event01 to Event02.

9. Drag the Age Test action from the Depot pane, and drop it below the Material Dynamic action. Then select Event Age from the drop-down list in the Parameters pane, and set the Test Value to 2.

10. Finally, drag the Delete action from the Depot pane, and drop it away from the other events. Then wire Event02 to the new event node, and select the Selected Particles Only option in the Parameters pane.

Figure 41.21 shows several moths eagerly pursuing the swinging lantern.

# FIGURE 41.21

All the moths in this scene are particles and are following a target linked to the lantern.

![](bbox=[0.08, 0.68, 0.58, 0.88])

# Debugging test actions

Any test action can be made to return a True or False value if you click the left (for True) or right (for False) side of the test action’s icon in the Particle View interface. This lets you debug the particle flow. Tests set to be true show an icon with a green light, and tests set to be false show a red light icon.