# FIGURE 44.3

The Object Properties dialog box lets you define the properties of cloth and collision objects.

![](bbox=[0.03, 0.23, 0.48, 0.68])

After all the objects involved in the simulation are included and defined, you can set the simulation range in the Simulation Parameters rollout. The initial state for the object to be draped may be set using the Set Initial State button, which is located in the Object rollout. The Cloth Forces button, in the Object rollout, opens a simple dialog box where you can select to add additional forces to the simulation. Gravity is added by default, but you can change its value in the Simulation Parameters rollout.

# Creating a cloth simulation

After completing the initial setup, clicking the Simulate button starts the simulation process. The objects are updated in the viewport as each frame is calculated. After every frame is calculated, you can see the entire dynamic simulation by dragging the Time Slider or clicking the Play Animation button. If you want to drape the cloth without running it over several frames, you can use the Simulate Local button. The Simulate Local (damped) button causes the simulation to run local with a large amount of damping, which is useful if the cloth tends to drape too fast. If you want to remove the current simulation because some properties have changed, click the Erase Simulation button, or you can remove all frames after the current simulation frame with the Truncate Simulation button.