To keep everything tidy, all of the physics functionality is called from FixedUpdate(),
but it actually resides in the Update() function:

```
public void FixedUpdate()
{
    UpdatePhysics();
}
```

Changing the pitch of the engine AudioSource object makes a convincing motor
sound. As it may be possible for mySpeed to be negative, Mathf.Abs is used,
as well as an arbitrary multiplier to bring the number down to something that changes the
pitch in a satisfactory manner. There's no science here! The number was decided by trial
and error, just adjusting its value until the motor sounded right:

```
public virtual void UpdateEngineAudio()
{
    // this is just a 'made up' multiplier value applied to
    // mySpeed.
    engineAudioSource.pitch=0.5f + (Mathf.Abs(mySpeed)*0.005f);
}
```

The real guts of the script may be found in the UpdatePhysics() function. CheckLock()
is called first, which takes care of holding the vehicle in place when the lock is on (the vari-
able is Locked set to true):

```
public virtual void UpdatePhysics()
{
    CheckLock();
}
```

velo is a variable holding the car's rigidbody:

```
// grab the velocity of the rigidbody and convert it into
// flat velocity (remove the Y)
velo=body.angularVelocity;
```

The next task is to find the velocity in the local coordinate space, remove its y-axis,
and use its value along the z-axis to put it in the variable: mySpeed:

```
// convert the velocity to local space we can see how fast we're
// moving forward (along the z axis)
velo=transform.InverseTransformDirection(body.velocity);
flatVelocity.x=velo.x;
flatVelocity.y=0;
flatVelocity.z=velo.z;
```

mySpeed is then checked to see whether its value is less than 2. When the speed is
slow and the brake key is held down, brakeTorque is no longer applied to the wheels;
instead, a reverse amount of the maximum amount of torque (brakeMax) is
applied to make the vehicle move backwards. Note that brakeMax is both the maxi-
m amount of torque applied into the brakeTorque property of the WheelCollectors