```
_engineSoundSource = _GO.GetComponent<AudioSource>();
}
```

Above, if no engine sound source has been set up via the Inspector window of the Unity editor, the script tries to find it with a call to GameObject.GetComponent(). The sound source will be stored in engineSoundSource and used solely for engine sound effects.

As with all the movement controllers, SetUserInput (next) sets a flag to decide whether inputs should be used to drive the vehicle:

```
public void SetUserInput( bool setInput )
{
    canControl= setInput;
}
```

Unlike other movement controllers from this book, this one introduces a lock state:

```
public void SetLock(bool lockState)
{
    isLocked = lockState;
}
```

The lock state is for holding the vehicle in place without affecting its y-axis. This differs from just disabling user input as it adds physical constraints to the physics object to hold it still (its purpose being to hold the vehicle during the counting in at the start of a race or other similar scenario).

```
public virtual void LateUpdate()
{
    if(canControl)
        GetInput();
    UpdateEngineAudio();
}
```

Above, LateUpdate() starts by checking for input via the GetInput() function, when canControl is set to true. Next, UpdateEngineAudio() is called to update the pitch of the engine sound based on the engine speed.

```
public virtual void FixedUpdate()
{
    UpdatePhysics();
    DoFakeBrake();
    CheckGround();
}
```

All of the physics code is called, above, from a call to UpdatePhysics() in FixedUpdate(). We call out to a braking function DoFakeBrake() and CheckGround() to check to see if the vehicle is on the ground.

```
public virtual void UpdatePhysics()
{
    CheckLock();
}
```

CheckLock() is called first, which holds the vehicle in place when the lock is on (when isLocked is true) – ideal for holding vehicles in place at the start of a race!