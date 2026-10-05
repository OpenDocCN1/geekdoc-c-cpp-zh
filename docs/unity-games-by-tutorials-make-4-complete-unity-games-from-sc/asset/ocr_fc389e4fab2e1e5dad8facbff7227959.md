# Unity Games by Tutorials

Now comes the fun part — actually shooting back. There are two things you need to do:\Deal damage to the robots but also implement zooming (otherwise known as iron sights).

Open Gun and add the following variables:

```
public float zoomFactor;
public int range;
public int damage;

private float zoomFOV;
private float zoomSpeed = 6;
```

zoomFactor controls the zoom level when the player hits the right mouse button.
FOV is the field of view based on the zoom factor. range is how far the gun can effectively hit its target. The shotgun has the shortest range and the pistol has the longest. damage is how much damage the gun causes.

Save your work and switch to Unity.

Click the 1Pistol GameObject and set its Zoom Factor to 1.3, Range to 60 and its Damage to 3.

Click the 2AssaultRifle GameObject and set its Zoom Factor to 1.4, Range to 30 and its Damage to 1.

Click the 3Shotgun GameObject and set its Zoom Factor to 1.1, Range to 10 and its Damage to 10.

Open the Gun script and update Start() to the following:

```
void Start()
{
  zoomFOV = Constants.CameraDefaultZoom / zoomFactor;
  lastFrameTime = Time.time - 10;
}
```

This initializes the zoom factor.

Modify Update() to the following:

```
protected virtual void Update()
{
  // Right Click (Zoom)
  if (Input.GetMouseButton(1))
{
    Camera.main.fieldOfView = Math.Lerp(Camera.main.fieldOfView, zoomFOV, zoomSpeed * Time.deltaTime);
  }
  else
{
    Camera.main.fieldOfView = Constants.CameraDefaultZoom;
}
```