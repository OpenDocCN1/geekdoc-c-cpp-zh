```
SetupPlayers();

// do initial lap counter display
UpdateLapCounter(1);

// start the game in 3 seconds from now
Invoke("StartRace", 4);
```

The code above first calls out to SetupPlayers() to get our player prefabs into the Scene, then sets the lap counter to 1 through the UpdateLapCounter() function.

The 3,2,1 count in is about to begin. It will take 4 seconds to go through it, so the Game Manager uses Unity's Invoke function to schedule a call to StartRace in 4 seconds' time.

```
InvokeRepeating( "UpdatePositions", 0.5f, 0.5f );
```

There is no need for the user interface to update every frame or every step. It would be unnecessary load on the CPU to update positions like that, so instead the Game Manager schedules a repeating call to the UI updating function UpdatePositions() every half second. The InvokeRepeating function takes three parameters; the name of the function to call, the time from the call to the first function call and the last one is the time between each function call after that and ongoing until either this script instance is destroyed or CancelInvoke is called to stop the continuing calls.

```
// hide our count in numbers
HideCount();
```

All three of the 3,2,1 count in numbers should be hidden at the start of the game (otherwise we'll just have a big blob of all three numbers on the screen at the same time!). A call to the game controller's HideCount() function takes care of that.

```
// schedule count in messages
Invoke( "ShowCount3", 1 );
Invoke( "ShowCount2", 2 );
Invoke( "ShowCount1", 3 );
Invoke( "HideCount", 4 );
```

The code to make the 3,2,1 count in happen is made simple by Unity's Invoke function. The functions our Game Manager uses to display each number will hide each previously displayed number, so all that needs to be done is some staggered calling to each one followed by a final call to HideCount() to hide the final number at the end of the count in sequence.

```
// hide final position text
_uiManager.HideFinalMessage();
```

When the race is over, a message tells the user what their final race position was. At the start of the race, this should be hidden. We call HideFinalMessage() on the _uiManager (an instance of RaceUIManager in the Scene) to hide it.

```
// start by hiding our wrong way message
wrongWaySign.SetActive( false );
```