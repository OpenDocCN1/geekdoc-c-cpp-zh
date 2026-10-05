# What do these numbers mean?

By default, Unity considers one point to be equal to one meter, but you don't have to follow this logic. For instance, you may be making a game about planets, and that scale would be too small. For the purposes of simplicity in this book, we have sized our models to follow Unity's default of one point per meter.

Now that you've altered the location, you have to apply it to the SpaceMarine GameObject. Add the following after the previous line:

```
transform.position = pos;
```

This updates the SpaceMarine GameObject's position with the new position.
Save the script and switch back to Unity. You may be tempted to run your game, but there's a slight problem. The camera is not positioned correctly.

In the Hierarchy, select the Main Camera, and in the Inspector, set Position to (-9.7, 53.6, -56.1) and Rotation to (30, 0, 0). I determined these values by moving the camera around manually and looking at the Camera preview in the lower right until I was happy with the result.

In the Camera component, set Field of View to 31. This effectively "zooms" in the view a bit.

![](bbox=[0.284, 0.545, 0.715, 0.883])