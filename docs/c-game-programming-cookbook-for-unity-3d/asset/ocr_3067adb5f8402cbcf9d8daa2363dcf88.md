Init() is responsible for setting up the references required to make the core of this class
work. Those are the transform of the gameObject script is attached to and the trans-
belonging to the main camera in the scene (found using Unity's camera.main):

```
void Init() {
    // cache ref to our transform
    myTransform = transform;

    // cache ref to the camera
    Camera mainCam = Camera.main;
```

Camera.main finds the first camera tagged with the MainCamera tag (see the tag
dropdown in the Unity editor Inspector window). If there are no cameras in the scene
tag with this, the main part of this function will not work. For that reason, main-
Cam is null, it drops out of Init():

```
if (mainCam==null) {
    return;
}
```

The camera transform is stored in cameraTransform, which will be used to trigger
spawning when distanceBasedSpawnStart is true:
cameraTransform = mainCam.transform;
This has its own shouldReversePath Boolean variable, as the waypoint
controller owning. This line takes the value of the Boolean variable shouldReversePath
uses it to override the existing reserve value held by the waypoint controller
any spawned objects will use. It does this by calling waypointControl.SetReverseMode():

```
// tell waypoint controller if we want to reverse the path
// or not
waypointControl.SetReverseMode(shouldReversePath);
```

Keep a total on how many objects are in the spawnObjectPrefabs array:
totalSpawnObjects = spawnObjectPrefabs.Length;

If AutoStartSpawningOnLoad is true, the first spawning kicks off right away.
TheWave() function takes two parameters: how many enemies it should spawn and
what the time between spawns will be here on. StartWave() will schedule future
enemy spawning:

```
if (shouldStartSpawningOnLoad) {
    StartWave(totalAmountToSpawn, timeBetweenSpawns);
}
```

TheOnDrawGizmosSelected() function draws helper graphics in the Unity editor
whenever this gameObject is selected:

```
public void OnDrawGizmosSelected() {
}
```