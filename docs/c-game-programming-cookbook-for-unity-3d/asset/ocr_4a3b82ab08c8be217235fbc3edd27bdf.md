playerGO2 will hold a reference to the second player when a cooperative game is selected from the main menu and totalPlayers is greater than 1:

```
// if we have a two-player game, let's grab that
// player's gameobject too
if(totalPlayers>1)
    playerGO2=SpawnController.Instance.GetPlayerGO(
```

When a level begins, a game controller prefab is instantiated. Within the child objects of the game controller prefab are several objects to the game, one of which is a camera named GameCamera. Until the game controller prefab is added to the scene, the in-game levels have no camera. As the Init() function runs on the game controller script, it grabs a reference to the camera and positions it at the correct point for starting the level. CameraTransform is used to hold the main reference:

```
// find the game camera
CameraTransform = GameObject.Find("GameCamera").transform;
```

```
// position the camera at the specified position
// (set in the Unity Editor window on this
// component)
tempVec3 = CameraTransform.localPosition;
tempVec3.z = CameraStartPositionZ;
CameraTransform.localPosition = tempVec3;
```

The variableControl holds a reference to the game controller script:

```
// if we don't have a camera script object set by
// the editor, try to find one
cameraControl=
CameraTransform.GetComponent<BaseCameraControl(),
```

As a top-down scrolling shoot 'em up game, the scrolling of the level is continuous until it is stopped. The isStopped Boolean variable will be used to stop scrolling when the player reaches the boss battle:

```
isStopped=false;
```

To able to change game scenes, this script needs to have a reference to the scene manager. It looks for the scene manager in the GetSceneManager() function:

```
// make sure we have a scene manager to talk to
GetSceneManager();
didInit=true;
```

After all of the main updates are done, the camera is moved forward a little more in LateUpdate(). During the game, there are several very important objects parented to the camera that will be moved along with it. These are

+   * BulletDestroyer Large invisible object with a box collider. There are two of these objects, located just off camera, blocking the path across of the play area for projectiles. One is at the top of the play area, one at the bottom. When a projectile hits the collider, it is destroyed. This stops projectiles from firing off into infinity.