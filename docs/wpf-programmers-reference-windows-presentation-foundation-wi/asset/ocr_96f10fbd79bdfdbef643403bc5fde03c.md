The CameraTypes example program shown in Figure 23-6 displays images of the same scene with both kinds of cameras.

![](bbox=[0.147, 0.147, 0.621, 0.355])

FIGURE 23-6

> > ORTHOGRAPHIC ILLUSIONS

Because your brain expects far objects to look smaller than closer objects, orthographic projections can sometimes cause an optical illusion. When you look at the right side of Figure 23-6, your brain may tell you that the box in the back is bigger than those in front because it does not appear smaller as it should.

The following code shows how the CameraType parameter defines its perspective camera. The FieldOfView parameter determines the camera's field of view in degrees. A larger value makes the camera see more to the sides so the camera must shrink its results to fit in its available area.

```
<PerspectiveCamera
Position="0, 0, 8"
LookDirection="0,0,-8"
FieldOfView="60">
```

Available for download on Wrox.com.

CameraTypes

The following code shows how the CameraTypes program defines its orthographic camera. The Width parameter determines the width of the camera sees in the scene's coordinate system. This parameter is roughly the orthographic equivalent of the perspective camera's FieldOfView parameter.

```
<OrthographicCamera
Position="0, 0, 8"
LookDirection="0, 0,-8"
UpDirection="0, 1, 0"
Width="8">
```

Available for download on Wrox.com.

CameraTypes