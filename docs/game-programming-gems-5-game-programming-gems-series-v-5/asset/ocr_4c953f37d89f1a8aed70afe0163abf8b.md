motion. To compensate, the prediction about the actual position of the followed object is born 0.7 seconds earlier. Therefore, the sample buffer holding the extrapolated positions needs to store samples from the last 0.7 seconds, which is easy to solve in case of a constant frame rate. However, the frame rate of a computer game is always changing depending on the complexity of the rendered scene. As a result, we must use a variable length sample buffer for extrapolated positions.

# Programming Issues

This gem was implemented in C++ language using OpenGL and GLUT graphics support in the Win32 environment. In this section, we will present our virtual camera model and other helper data structures, which are applicable to OpenGL easily.

# Camera in OpenGL

First of all, let us see how we can define a perspective view in OpenGL using GLUT. We used two functions to define a view. The first is

```
gluPerspective(fov, width/height, nearDist, farDist);
```

The fov (field of view) is the vertical viewing angle of a camera in degrees. This can be a small value when using a telephoto lens and can be large in the case of a wide-angle lens. If you want to simulate zooming, you have to change this variable from time to time. The value width/height defines the aspect ratio of the rendered view, which should be the same as the screen to avoid distortion. The last two parameters, nearDist and farDist, define the distance of the camera's eye from the near and far clipping planes. The scene appears between these two planes.

The basic function for the camera definition is as follows:

```
gluLookAt(eye.X(), eye.Y(), eye.Z(),
 target.X(), target.Y(), target.Z(),
 up.X(), up.Y(), up.Z());
```

With this call, we can define the actual position of the camera's eye, the target point, and the camera's up vector. In a computer game, the scene is always changing. If the camera is changing too, we need to recalculate these variables frame by frame in both functions.

# Changeable Field of View, Auto-Zoom

Our camera model has an auto-zoom feature. Our camera can take into account the size of the followed object and its distance from the camera, allowing it to calculate the fov at every time step:

```
fov = 2.0 *
 atan((targetSize / 2.0) / (target - eye).Length()) *
 180.0 / M_PI;
```