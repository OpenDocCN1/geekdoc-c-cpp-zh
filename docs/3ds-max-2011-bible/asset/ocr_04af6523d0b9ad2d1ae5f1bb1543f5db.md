# TABLE 43.4

# reactor Constraints

| Toolbar Button | Name | Description |
|---|---|---|
|  | Constraint Solver | Contains all active constraints used in the scene |
|  | Rag Doll Constraint | Causes a model to act as a human figure |
|  | Hinge Constraint | Allows angular rotation like a hinge |
|  | Point-Point Constraint | Links two points together; good for rope ends |
|  | Prismatic Constraint | Used to constrain the motion of two rigid bodies to a single axis with no rotation |
|  | Car-Wheel Constraint | Causes a car to move linearly as a wheel object is rotated |
|  | Point-Path Constraint | Limits a point to move only along a path |

When a constraint's Child is first selected, the Constraint's icon is positioned at the pivot point of the child object. If you look in the Modifier Stack for the Constraint object, you'll find subobject modes for Child Space and Parent Space. If you select these subobject modes, you can change the position of the constraint's child and parent objects.

# Using a Constraint Solver

In order to use most constraints, you need to add a Constraint Solver to the scene. Then you can use the Modify panel to add Constraints to the list to be solved. The Constraint Solver needs to know about any Rigid Body Collections that are attached to any Constraints in the scene. To identify all the Constraints that are part of the Constraint Solver, click the Highlight button.

# Tip

If the simulation includes any constraints that the Constraint Solver doesn't know about, the Constraint Solver icon appears red in the viewports.

# Rag Doll constraint

The Rag Doll constraint defines all the joint limits common in a human figure. It can be used to animate a lifeless body colliding with various rigid body objects. Using the Rag Doll constraint, you can manually define how the body joints can twist, rotate, and move.

These joints are fairly common for human bodies. Autodesk has created a script to create a human body proxy that creates a rag doll with the correct constraints already defined. The script is named rctRagdollScript.ms. It can be found in the scripts directory where 3ds Max is installed.