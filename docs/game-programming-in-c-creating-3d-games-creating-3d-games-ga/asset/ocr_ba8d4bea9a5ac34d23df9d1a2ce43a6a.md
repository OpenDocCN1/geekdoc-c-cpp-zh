Click here to view code image

```
// Location of camera
Vector3 eye = mCameraActor->GetPosition();
// Point 10 units in front of camera
Vector3 target = mCameraActor->GetPosition() +
mCameraActor->GetForward() * 10.0f;
Matrix4 view = Matrix4::CreateLookAt(eye, target, Vec
```

# Projection Matrix

The **projection matrix** determines how the 3D world flattens into the 2D world drawn onscreen. Two types of projection matrices are common in 3D games: orthographic and perspective.

In an **orthographic projection**, objects farther away from the camera are the same size as objects closer to the camera. This means that players will not be able to perceive whether objects are closer or farther away from the camera. Most 2D games use an orthographic projection. Figure 6.3 illustrates a scene rendered with an orthographic projection.