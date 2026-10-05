# Unity Games by Tutorials

# Chapter 4: Physics

degrees in either way. To make it bounce a proper bobble head, set Bounciness to 1— that’s the max value.

Keep the rest of the values as they are, but take note of Break Force and Break Torque. You’d use these if you wanted the head to snap under a certain threshold, e.g., create the effect of a door being blown off its hinges.

Here’s the configured joint:

![](bbox=[0.287, 0.243, 0.712, 0.603])

The hinge needs a collider to work. Click the Add Component button, and from the Physics category, select Sphere Collider. Set Center to (0.41, 2.7, -0.21) and Radius to 2.36. This closely matches the width of the head.

The last thing this needs is some force to make the head bob.

Open PlayerController.cs in your code editor. You need a reference to the connected head Rigid, so add the following instance variable:

```
public Rigidbody head;
```

You might ask why you’re using a Rigidbody instead of a GameObject.

Remember, a Rigidbody deals with physics. You’re adding the head to apply force to it, and there’s no way to apply force to a regular GameObject. Hence, you need a Rigidbody.

raywenderlich.com

117