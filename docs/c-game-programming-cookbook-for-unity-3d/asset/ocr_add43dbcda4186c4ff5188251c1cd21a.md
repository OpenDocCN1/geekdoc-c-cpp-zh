To access the user's controller script quickly, the game controller stores a reference to it in the variable focusPlayerScript, named because it is the player on which the game controller will focus:

```
focusPlayerScript = ( CarController_MVD )
playerGO1.GetComponent<CarController_MVD>();
```

The user's player script is given an ID number of 0, and user input is allowed with a call to UseInput():

```
// assign this player the id of 0
focusPlayerScript.SetID( 0 );
```

```
// set player control
focusPlayerScript.SetInput( true );
```

For the camera to follow the player during the game, the camera control script needs to know about its target. This script uses the SetTarget() function to do that, passing in the transform from playerGO1:

```
// tell the camera script to target this new player
cameraScript.SetTarget( playerGO1.transform );
```

UpdateLapCounter is used to set the counter to be displayed by the UI code. Its default value of 1 gets set so that the display is correct when the game starts:

```
// do initial lap counter
UpdateLapCounter( 1 );
```

Players need to be held in place until the 3-2-1 countdown at the start of the race has finished. The function SetPlayerLocks will loop through all of the players in the game and tell them whether or not they should be locked in place:

```
// lock all the players on the spot we're ready to go
SetPlayerLocks( true );
```

The 3-2-1 countdown is to begin. It takes 4 seconds to go through StartRace 4 times using the Invoke function:

```
// start the game in 3 seconds from now
Invoke( "StartRace", 4 );
```

There is no need for the user interface to update every frame or every step. It would be an unnecessary load on the CPU to update positions like that, so instead, the game controller schedules a repeating call to the InvokeRepeating function takes three parameters: the name of the function to call, the time from the call to the first function call, and the time between each function call after that and ongoing until this script instance is destroyed or CancelInvoke is called to stop the continuing calls:

```
// update positions throughout the race, but we don't need
// to do this every frame, so just do it every half a second
// instead
InvokeRepeating( "UpdatePositions", 0.5f, 0.5f );
```