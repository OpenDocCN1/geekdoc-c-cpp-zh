toppling over in games, but it comes at cost. If the car were to roll and flip over, it will roll in an unrealistic way because of the center of mass will affect its movement. Look to the stabilizer bar simulation for a more realistic solution, but for now, this is as far as we go:

```
// with this simple vehicle code, we set the center of the mass
// low to try to keep the car from toppling over
myBody.centerOfMass= new Vector3(0,-4f,0);
```

If no engine sound has been set up in the Vehicle Inspector of the Unity editor, the script tries to find it a call with GameObject.GetComponent(). The sound source will be stored in engineSoundSource and used solely for engine sound effects:

```
// see if we can find an engine sound source, if we need to
{
    engineSoundSource=null

    engineSoundSource=myGO.GetComponent<AudioSource>();
}

```

As all of the movement controllers, UserInput sets a flag to decide whether or not inputs should be used to drive the vehicle:

```
public void SetUserInput(bool setInput)
{
    canControl= setInput;
}
```

Unlike movement controllers from this book so far, this introduces a lock state. The lock state is for holding the vehicle in place without affecting its y-axis. This differs from disabling user input as it adds physics constraints to the physics object to hold it still (purpose being to hold the vehicle during the counting in the start of a race or other similar scenario):

```
public void SetLock(bool lockState)
{
    isLocked = lockState;
}
```

LateUpdate() starts by checking for input via the GetInput() function, when canControl is set to true. Next, UpdateEngineAudio() is called to update the pitch of the engine sound based on the engine speed:

```
public virtual void LateUpdate()
{
    // check for input in LateUpdate because Unity recommends
    // this
    if (canControl)
        GetInput();

    // update the audio
        UpdateEngineAudio();
}
```