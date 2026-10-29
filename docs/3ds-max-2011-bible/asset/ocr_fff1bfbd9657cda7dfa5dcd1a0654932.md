# Part VIII: Advanced Animation Techniques

# SplineIK Control modifier

The SplineIK Control modifier can be applied only to spline objects. In the Spline IK Control Parameters rollout, you can click the Create Helpers button, which adds a dummy object to every vertex on the spline. These dummy objects make it much easier to control the spline without having to enter vertex subobject mode. You can also specify how the dummy objects are linked and how they are displayed.

# Attribute Holder modifier

The Attribute Holder modifier displays all custom defined attributes in their own rollout. Creating custom attributes and wiring attributes is discussed in Chapter 35, “Animating with the Expression Controller and Wiring Parameters.”

# Examining Complex Controllers

Now that you are somewhat familiar with controllers and how they work, let’s look at some more complex controllers. Max includes a vast assortment of controllers, and you can add more controllers as plug-ins.

# Transform controllers

Multi-track transform controllers work with the Position, Rotation, and Scale tracks all at the same time. You access them by selecting the Transform track in the Motion panel and then clicking the Assign Controller button or by choosing the Animation ▸ Transform Controllers menu command.

# Note

Each of the available constraints is listed again in the appropriate controller submenu. ■

![](bbox=[0.09, 0.583, 0.13, 0.61])

# Position/Rotation/Scale Transform controller

The Position/Rotation/Scale Transform controller is the default controller for all transforms. This controller includes a Bézier controller for the Position and Scale tracks and a Euler XYZ controller for the Rotation track.

The PRS Parameters rollout, shown in Figure 34.17, lets you create and delete keys for Position, Rotation, and Scale parameters. The Position, Rotation, and Scale buttons control the fields that appear in the Key Info rollouts positioned below the PRS Parameters rollout.

![](bbox=[0.09, 0.711, 0.13, 0.737])

# Script controller

The Script controller is similar to the Expression controller, except that it can work with the MAXScript lines of code for controlling the scene. Right-clicking a track with the Script controller assigned and selecting Properties opens the Script Controller dialog box. Script controllers are available for all transform tracks including Transform, Position, Rotation, and Scale. The flexibility of the Script controller is quite robust. The Script controller is covered in more detail at the end of this chapter, as is the Expression controller.

# Cross-Ref

For more information on MAXScript, see Chapter 49, “Automating with MAXScript.” ■

# XRef controller

If you have a defined motion used by an object in another file that you want to access, you can use the XRef controller. This controller can be assigned only to the Transform track. When this controller is assigned, a file dialog box opens where you can select the XRef file; then in the Merge Object dialog box, you can select a specific object that has the controller and motion you want to use.