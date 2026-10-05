You'll also need to set MinX, MinY, MaxX and MaxY to temporary high and low values. You'll reset these constraints when you build a level in Chapter 13, "More 2D."

For now, enter -100 for MinX and MinY then 100 for MaxX and MaxY. Set the Tracking Speed to 2.5 – determines how quickly the camera moves towards its target.

Run the game. Using the Scene view move along with the move tool, move SoyBoy around with the mouse and notice how smoothly the camera follows the sprite. Awesome!

![](bbox=[0.346, 0.296, 0.653, 0.399])

# Adding 2D physics

Right now, your sprites can't interact with the physics engine. They just float in the air. If there were to be a collision, the reaction would make you think you've created a strange alternate universe.

Unity's 2D physics system is similar to the 3D system. The main difference is that you use the versions of each type of component.

These are the physics components that you'll use in 2D games to let objects interact with the physics engine:

+   - Rigidbody2D: Puts a sprite or object under the control of the physics engine. You generally need one for every item that uses a collider.
- BoxCollider2D: Defines an axis-aligned rectangle collision area around an object.
- CircleCollider2D: Creates a circular collision area around an object.
- PolygonCollider2D: Makes an arbitrary polygon-shaped collision area around an object that's defined by vertices set up in different positions. They usually have more edges than other colliders, so they also come at a higher cost. Be careful with these!
- EdgeCollider2D: Represents an arbitrary set of connected edges defined by vertices.