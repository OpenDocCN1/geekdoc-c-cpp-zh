```
Vector3 cameraPos = target + mOffset;

Matrix4x4 view = Matrix4x4::CreateLookAt(cameraPos, t

SetViewMatrix(view);
}
```

For the look-at matrix, the target position of the camera is simply the owner's position, the camera position is the owner's position plus the offset, and the up is the camera up. This yields the final orbited camera. Figure 9.5 demonstrates the orbit camera with the car as the target.

![](bbox=[0.172, 0.433, 0.722, 0.763])

Figure 9.5 Orbit camera focused on the car

# SPLINE CAMERA

A spline is a mathematical representation of a curve