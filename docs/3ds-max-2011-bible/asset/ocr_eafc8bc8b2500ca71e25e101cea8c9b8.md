# # Animating with Constraints and Simple Controllers

When you first begin animating and working with keys, having Max figure out all the frames between the start and end keys seems amazing, especially if you've ever animated in 2D by drawing every frame. But soon you realize that animating with keys can be time-consuming for complex realistic motions, and again, Max comes to the rescue. You can use animation constraints and controllers to automate the creation of keys for certain types of motions.

Constraints and controllers store and manage the key values for all animations in Max. When you animate an object using the Auto Key button, the default controller is automatically assigned. You can change the assigned controller or alter its parameters using the Motion panel or the Track View.

This chapter explains how to work with constraints and some simple controllers. For example, you can use the Noise controller to add random motion to a flag blowing in the wind or use the Surface constraint to keep a bumper car moving over the surface.

# ## Restricting Movement with Constraints

The trick of animating an object is to make it go where you want it to go. Animating objects deals not only with controlling the motion of the object but also with controlling its lack of motion. Constraints are a type of animation controller that you can use to restrict the motion of an object.

Using these constraints, you can force objects to stay attached to another object or follow a path. For example, the Attachment constraint can be used to make a robot's feet stay connected to a ground plane as it moves. The purpose of these constraints is to make animating your objects easier.

![](bbox=[0.762, 0.026, 0.961, 0.148])

**IN THIS CHAPTER**

- Using constraints
- Attaching an object to the surface of an object
- Making an object travel along a path with the Path constraint
- Controlling the weighted position and orientation of objects
- Shifting between two controlling objects using the Link constraint
- Following objects with the LookAt constraint
- Understanding the controller types
- Assigning controllers using the Motion panel and the Track View
- Setting default controllers