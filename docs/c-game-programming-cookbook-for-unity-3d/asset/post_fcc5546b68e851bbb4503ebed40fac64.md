
```cs
// if we are moving slow, apply some extra force to turn the
// car quickly so we can do donuts (!) - note that since
// there is no 'ground detect' it will apply it in the air,
// too (bad!)
if(mySpeed < TurnTorqueHelperSpeed) {
    myBody.AddTorque(new Vector3(0, steer * myBody.mass * turnTorqueHelper * motor, 0));
}
```

The global race manager tracks the race state and whether the race is running, but it will also communicate it to each player's race controller. LateUpdate() starts by getting the state of the race from raceControl.raceRunning and storing it into a variable named `isRaceRunning`:

```csharp
public override void LateUpdate() {
    // get the state of the race from the race controller
    isRaceRunning = raceControl.raceRunning;
}
```

If the race is running, this function will go on to do all the things we need to during the race:

```csharp
if(isRaceRunning) {
```

We regularly call Check_If_Car_Flipped() to check to see whether the car's rotation is irregular, to see whether it has flipped and needs respawning:

```csharp
// check to see if we've crashed and are upside down
Check_If_Car_Flipped();
```

Whenever the race is running on AI, `canControl` should be able to fire, so `canControl` is set to true:

```csharp
if(isAIControlled) {
    // make sure that canControl has been told it can fire
    canControl = true;
}
```

When this is updating an AI player, inputs to drive the vehicle come from the GetAIInput() function. Otherwise, GetInput() will provide inputs from the default object:

```csharp
if(isAIControlled) {
    GetAIInput();
} else {
    GetInput();
}
```

When the Boolean variable `isRaceRunning` is false, the race is over for this player, the LateUpdate() function needs to ignore input. Instead of getting inputs for the vehicle, this code just disables the `canControl` script so that nobody can fire after the game ends:

```csharp
if (isAIControlled) {
    // since the race is not running, we'll tell canControl not to fire yet
    canControl = false;
}
```

The race controller always needs to track waypoints for position tracking and lap counting, regardless of whether the race is still running. raceControl does not keep own update function so the next part of LateUpdate() calls UpdateWaypoints() to keep updating:

```csharp
// tell the race controller to update
UpdateWaypoints();
```

The code continues by calling CheckLock() to see whether or not the vehicle is held in place, and then there is a call out to raceControl to CheckWrongWay():

```csharp
// see if our car is supposed to be in place
CheckLock();
// tell race control to see if we're going the wrong way
CheckWrongWay();
```

When raceControl detects the vehicle is traveling around the track the wrong way, assumption is made that non-AI-controlled player will be the user. The code below tells the game controller to update its wrong-way status with a call to GameController.Instance.UpdateWrongWay():

```csharp
// check to see if we're going the wrong way and act on it
if(raceControl.goingWrongWay) {
    if (isAIControlled)
        GameController.Instance.UpdateWrongWay(true);
}
```

When raceControl first detects the vehicle is heading in the wrong direction, this `timeWayStarted` variable acts like a timestamp as it is set to the value of the system `Time.time`. This code checks `raceControl.timeWayStarted` and `Time.time` to see whether the vehicle has been going in the wrong way for longer than the time set by `resetTime`:

```csharp
// if going the wrong way, compare time since it started to see if we need to respawn
if(raceControl.timeWayStarted != -1)
    timedIf = Time.time - raceControl.timeWayStarted;
if(timedIf > resetTime)

If the vehicle has been going the wrong way for too long, the function Respawn() is called to put it back on the track facing the right direction:

```csharp
// it's been x resetTime seconds in the wrong way, let's respawn this thing:
Respawn();
} else if (isAIControlled) {
```

When this condition is met, the car is not going the wrong way and it is not an AI-controlled vehicle so a call is made to the game controller to UpdateWrongWay(), telling that we are not going the wrong way so that the UI may be updated accordingly:

```csharp
GameController.Instance.UpdateWrongWay(false);
}
```

In racing games, one common method for keeping the game interesting is to employ something rubber banding. It gets its name from the type of effect that happens when the top speed of racers is increased when they fall too far behind and decreased when they get too far ahead—the players rubber band in front and behind the main player.

Done with some subtlety, rubber banding can help to provide an exciting race each time. When it is not handled well, the effect can be frustrating as the AI players gain the lead time the player starts ahead, so use it with caution! This really is one of those unseen parts of the game that needs to be carefully balanced but, despite having such a strong impact on gameplay, most players will not even notice.

To tell it is time for an AI player to go faster and when it is for that player to go slower, the code here uses RacePosition to see where this player stands. If myRacePosition is greater than 3—meaning that this player is in fourth place or worse—then the maximum acceleration rate of the vehicle, in the variable `accelMax`, is set to catchUpAccelMax to make it faster. If the position of this player is first (myRacePosition < 2), then `accelMax` is set to the original acceleration rate held by `originalAccelMax` multiplied by 0.25, slowing down the vehicle:

```cs
accelMax = originalAccelMax;

// catch up if this car is falling behind in the race
if(isRaceRunning && isAIControlled) {
    if(myRacePosition > 3) {
        // speed up
        accelMax = catchUpAccelMax;
    } else {
        accelMax = originalAccelMax;
    }
}

// first place, let's slow you down!
if(myRacePosition < 2) {
    accelMax = originalAccelMax * 0.25f;
}
```

The last part of the function will update the pitch of the engine audio based on the current speed of the vehicle. This happens in the UpdateEngineAudio() function, which is called here:

```cs
// update the audio
UpdateEngineAudio();
```

The GetInput() function overrides the original one found in BaseVehicle script. This works almost the same, with additions of respawning functionality and weapon support

```cs
public override void GetInput() {
    // calculate steering
    steer = Math.Clamp(default_input.GetHorizontal(), -1, 1);

    // how much accelerator?
    motor = Math.Clamp(default_input.GetVertical(), 0, 1);

    // how much brake?
    brakes = -1 * Math.Clamp(default_input.GetVertical(), -1, 0);
}
```

The default_input object is of type Keyboard_Input, which has support for respawn. Finding out whether the user is hitting the respawn key is a call to default_input.GetRespawn(), which will return true or false. If the user hits the respawn key, the vehicle is not respawning already and `canRespawn` is true, the Respawn() function is called to reset the cache, and the variables `isRespawning` and `canRespawn` are set to disable any further respawning. They will be reset when the call to resetRespawn is made, scheduled by an Invoke() function for 2 s time:

```cs
if(default_input.GetRespawn() && !isRespawning && canRespawn) {
    isRespawning = true;
    Respawn();
    canRespawn = false;
    Invoke("resetRespawn", 2);
}
```

To keep the flexibility of still being able to work without a weapon controller, the firing input code starts with a null check on `weaponControl`. If default_input.Fire() is true and `canFire` is true, weaponControl.Fire() is called to make the current weapon do its thing:

```cs
// first, we make sure that a weapon controller exists
// (otherwise no need to fire!)
if(weaponControl != null)
```
