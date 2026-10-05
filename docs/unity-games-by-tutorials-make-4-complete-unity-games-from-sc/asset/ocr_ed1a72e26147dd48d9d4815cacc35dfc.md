+   Player intersection with Hazards enabled: This ensures that the player can interact with touch hazards.

+   Default intersection with Hazards removed: You will be leaving all the level / platform building blocks on the Default layer, so you do not want the hazards to be collision checking against these. Usually the saw blades will be "embedded" or placed behind platform blocks, so disabling collisions here will also save on performance.

In Game scene, select SoyBoy and change the GameObject layer to the new Player physics layer. Click Apply to update the prefab instance.

# Completing the 2D Character Controller

Up until now, Super Soy Boy has only been able to move left and right and face in those directions. You'll need to get the meat of the controller to provide the complete range of platform movement actions.

# A note on 2D raycasting

2D raycasting will be used in your Character Controller to determine when you are touching the ground, jumping, up against a wall and so on.

Raycasting in 2D is done with the Physics2D.Raycast(). This method returns the RaycastHit2D type, which references the first Collider2D object that the ray hit. If the ray does not hit anything then the collider returns null.

![](bbox=[0.153, 0.597, 0.846, 0.823])

In the example above, a raycast is being performed from Super Soy Boy, to his right. The ray hits a Collider2D object. In code, a RaycastHit2D object would be returned, and the collider property on this would contain a reference to the object's BoxCollider2D.