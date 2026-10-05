```
for ( int i = 0; i < numberRacers; i++)
```

```
Transform tempT= (Transform)playerTransforms[i];
CarController_MVD tempController=
tempT.GetComponent<CarController_MVD>();
```

```
playerList.Add(tempController);
```

```
BaseAIController tempAI=tempController.GetComponent<nBaseAIController>();
```

```
// tell each player where to find the waypoints
tempAI.SetWaypointController(WaypointForAI);
```

```
tempController.Init ();
```

```
// tell the car controller script about the waypoint
// controller so it can pass it onto the
// racecontroller (!);
```

The variable WaypointControllerForAI should serve to reference the waypoint controller
in the main scene (via the Unity editor inspector):

```
tempController.SetWaypointController(WaypointForAI);
```

playerGO1 will store a reference to the main player's gameObject, which is returnedy the spawn controller when we ask for it by index:

```
// grab a ref to the player's gameobject for later use
playerGO1 = SpawnController.Instance.GetPlayerGO( 0 );
```

Once the main player is established, the game controller adds an
AudioListener component to it. By default, Unity adds an audio listener to the main camera of the scene. This is great for a start, but in this case, it makes more sense to have the
listener attached to the player; the user is supposed to be in the car, not in the camera:

```
// add an audio listener to the first car so that the audio
// is from the car rather than from the main camera
playerGO1.AddComponent<AudioListener>();
```

Next, the game controller looks to find the default AudioListener component attached to the camera. If it finds one, the next part of the code uses the Destroy() function
to remove it. Removing the listener from the camera is important, as Unity allows for
single listener per scene, and if there is more than one listener, a warning will be written
to the console:

```
// look at the main camera and see if it has an audio
// listener attached
AudioListener tempListener=
Camera.main.GetComponent<AudioListener>();
```

```
// if we found a listener, let's destroy it
if(tempListener==null)
Destroy(tempListener);
```