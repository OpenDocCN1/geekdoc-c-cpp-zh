```
 // fire if we need to
if( default_input.GetFire() && canFire)
{
    // tell weapon controller to deal with firing
    weaponControl.Fire();
}
}
```

When the respawn happens, a call to resetRespawn() resets the state of canRespawn to allow future respawning:

```
void resetRespawn()
{
    canRespawn=true;
}
```

GetAIInput() is called when a car is AI controlled. The AI vehicles get their inputs from the AI controller script; steering and motor inputs come from the AIController object instead of the input object:

```
public void GetAIInput()
{
    // calculate steering amount
    steer= Mathf.Clamp( AIController.GetHorizontal(), -1, 1);

    // how much accelerator?
    motor= Mathf.Clamp( AIController.GetVertical() , 0, 1);
}
```

When the race is over, FinishedRace() will be called to stop control of the vehicle and to tell the race (raceControl) that this player is done:

```
public void FinishedRace()
{
    // stop allowing control for the vehicle
    canControl = false;
    brake = 1;
    motor = 0;

    // set a flag so it's easy to tell when we are done
    raceControl.RaceFinished();
}
```

SetAIInput() is used to tell this script whether the player should be controlled by AI or not:

```
public void SetAIInput(bool aiFlag)
{
    isAIControlled = aiFlag;
}
```

When the function IsFinished() is called, it looks to the race controller (Boolean)
return result: