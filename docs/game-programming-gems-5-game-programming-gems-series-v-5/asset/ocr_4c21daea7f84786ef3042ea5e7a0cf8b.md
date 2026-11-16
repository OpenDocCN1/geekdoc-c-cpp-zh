In Figure 3.6.2, we see that an AI player has discovered an enemy city with some tanks around it. In this example, we have a player massing troops on the western slope. The AI has a corresponding detachment of units on the eastern slope. The AI would like to attempt an invasion of the belligerent city. Should it use the most direct route (A) or the alternate (B–C) route?

Ideally, the AI can react with a degree of prescience. At the strategic level, we assume that the AI already *knows* it needs to take the city. To accomplish this, the AI would need to evaluate the available routes and form a plan.

Here are three possible plans:

+   **Plan A:** March forces through the mountain pass.

+   **Plan B:** March forces to the port city and then transport them around to the southern flank.

+   **Plan C:** March part of the forces through the mountain pass to occupy the enemy while the main force executes plan B.

These plans all have similar components; let's look at the components that go into plan C, as it encompasses components of both plans A and B:

+   **Update the influence map:** In this specific instance, the AI needs to know if its forces can be mobilized *through* the choke point before his forces would be engaged. This will require an up-to-date influence map.

+   **Generate unit paths:** We need paths for units that are going to enter the mountain pass and for the units that are moving via route B–C.

+   **Provide Transportation:** Tasks to either build transports at the city or route transports to help in moving the units.

+   **Provide Attack Formations:** This will direct the units once they reach the western slope of the mountain range.

+   **Assess Diplomatic Constraints:** Ascertain what type of political fallout will occur if the AI attacks the city on the western slope.

Just by deciding how the AI should attack, we've generated several potential tasks. In addition to these new tasks, we may have high-level, behind-the-scenes, strategic plans and tasks in process. Some tasks will be quick and easy to compute (usually on the local processor); others will be bulky and require assignment to other PEs. As we shall see, the size or granularity of the task will dictate how each task needs to be scheduled.

# Granularity

Each task is assigned a *granularity*, which helps determine its scheduling position inside the task manager. A task's granularity is a reflection of the following:

+   - The size of the task
+   - The amount of computational effort required to accomplish the task
+   - The bandwidth that will be required to facilitate a solution