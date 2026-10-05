# Unity Games by Tutorials

This bit of code simply gets the current position of the GameObject — in this case, the space marine since that is what this script is attached to — stores it in a variable named pos. In Unity, a Vector3 encapsulates the x, y and z of a GameObject, i.e., the object's position in 3D space.

Now comes the tricky part. Add the following after the previous line:

```
pos.x += moveSpeed * Input.GetAxis("Horizontal") * Time.deltaTime;
pos.z += moveSpeed * Input.GetAxis("Vertical") * Time.deltaTime;
```

When you move it, it'll be on z- and x-axes which represents up and down. Because there are two different input sources ("Horizontal" for left and right, and "Vertical" for up and down), you need to calculate values for each axis separately.

Input.GetAxis("Horizontal") retrieves a value from the Horizontal component of the Input Manager. The value returned is either 1 or -1, with 1 indicating that a positive button in the Input Manager is being pressed. According to the settings you saw earlier, this is the right arrow or d keys. Similarly, a value of -1 indicates that a negative button is being pressed, meaning it was the left arrow or a key.

![](bbox=[0.345, 0.458, 0.654, 0.566])

Whatever the returned value may be, it's multiplied by the moveSpeed and added to the current x position of the GameObject, effectively moving it in the desired direction.

The same thing happens with Input.GetAxis("Vertical"), except it retrieves a value from the vertical component of the Input Manager (indicating with the s, down, w or up keys), multiplies this (1 or -1) by the moveSpeed and adds it to the z position of the GameObject.

So what? with Time.deltaTime? That value indicates how much time has passed since the last Update(). Remember, Update() is called with every frame, so that time difference must be taken into account or the space marine would move too fast to see.

TL/DR: Time.deltaTime ensures movement is in sync with the frame rate.