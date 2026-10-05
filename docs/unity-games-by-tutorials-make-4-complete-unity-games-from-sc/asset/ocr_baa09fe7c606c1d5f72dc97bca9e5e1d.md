```
{
// 3
if (camTarget != null) {\n// 4
  var newPos = Vector2.Lerp(transform.position,
    camTarget.position,
    Time.deltaTime * trackingSpeed);
  var camPosition = new Vector3(newPos.x, newPos.y, -10f);
  var v3 = camPosition;
  var clampX = Math.Clamp(v3.x, minX, maxX);
  var clampY = Math.Clamp(v3.y, minY, maxY);
  transform.position = new Vector3(clampX, clampY, -10f);
}
}
```

+   1. These public variable fields let you set the target the camera will track, tracking speed and the camera's bounds.
2. FixedUpdate() is called with every fixed-frerate frame — it's the best method when dealing with a Rigidbody component of any kind. The result is the camera will track the player, who will have a Rigid2D attached to it.
3. This null check ensures that a Transform component was assigned to the camTarget field in the editor.

4. Vector2.Lerp() performs linear interpolation between two vectors by the third parameter's value (a value between 0 and 1). Normally, you'd usually use this to move between positions over time, but here actually tracking as you near the camera's target (Soy Boy). The rest of the Lerp method ensures that the position calculated is clamped (constrained) to the MinX, MinY, MaxX, and MaxY points.

Save the script and return Unity.
Drag the CameraLerpToUnity script to the Main Camera GameObject in the Hierarchy.

Select the Main Camera in the Hierarchy. Drag SoyBoy Object onto the Cam Target field on the CameraLerpToTransform script, which is now attached to Main Camera.

![](bbox=[0.115, 0.775, 0.875, 0.855])

raywenderlich.com