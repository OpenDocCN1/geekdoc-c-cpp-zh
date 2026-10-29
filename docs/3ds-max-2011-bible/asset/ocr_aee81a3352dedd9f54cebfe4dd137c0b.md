# Part VIII: Advanced Animation Techniques

opposite of soft body dynamics is **rigid body** dynamics. Think of a statue in the park. When the wind blows, it doesn’t move. The statue is an example of a rigid body. On the other hand, the flag flying over the library moves all over when the wind blows. The flag is an example of a soft body.

# Cross-Ref

> Soft body objects can also be defined and simulated using reactor, which is covered in Chapter 43, “Simulating Physics-Based Motion with reactor.”

Another way to think of soft bodies is to think of things that can flex. Objects such as a clothesline flex under very little stress, but other objects like a CD flex only a little when you apply a significant force. The settings of the Flex modifier make it possible to represent all kinds of soft body objects.

Figure 34.12 shows many of the rollouts available for the Flex modifier.

# FIGURE 34.12.

The Flex modifier rollout lets you control the flex settings.

![](bbox=[0.069, 0.401, 0.568, 0.804])

# Flex subobjects

In the Modifier Stack, the Flex modifier has three subobjects that you can access: Center, Edge Vertices, and Weights and Springs. The Center subobject is a simple box gizmo that marks the center of the flex effect. Portions of the object that are farther from the center have a greater distance. The Edge Vertices subobject can be selected to control the direction and falloff of the flex effect. The Weights and Springs rollout controls the Weights and Springs subobject.