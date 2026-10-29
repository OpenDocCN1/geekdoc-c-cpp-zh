# FIGURE 43.10

Animating these falling donuts, simulated as soft body objects, was easy with reactor.

![](bbox=[0.07, 0.19, 0.85, 0.6])

# Constraining Objects

Constraints are ways to limit the amount of motion that an object can do. Using constraints can help control objects in the scene as they interact with other objects. Perhaps the simplest constraint isn't a constraint at all. If you enable the Unyielding option in the Property Editor, the rigid body is set so that it won't move and is a good option for the ground plane. It also allows hand-keyed animated objects to interact with rigid body objects instead of relying on the dynamics engine.

Other constraints are found in the Animation reactor Create Objects menu and consist of Constraint Solver, Rag Doll Constraint, Hinge Constraint, Point-Point Constraint, Prismatic Constraint, Car-Wheel Constraint, and Point-Path Constraint, as listed in Table 43.4.

After a Constraint object is added to the scene, you can select the objects that will be included as child and parent objects using the buttons in the Properties rollout. The Properties rollout also includes buttons to align the constraint to the Child Body, Parent Body, Child Space, or Parent Space. For each constraint, you can set the Strength and Tau of the connection. This determines how strong the link is and how easily broken. In addition to the Strength and Tau values, you can set Limits and allow the hinge to be Breakable under a defined Linear or Angular force value. The Threshold value defines the breakability of the constraint. Higher Threshold values make it less likely to break. The Threshold value works only with reactor version 3.