
car would float above its resting place against the ground until the race started when it would drop down some as gravity is applied:

```csharp
public void CheckLock()
{
    if (isLocked)
    {
        // control is locked out and we should be stopped
        steer = 0;
        brake = 0;
        motor = 0;
        // hold our rigidity in place (but allow the Y to
        move the car may drop to the ground if it is not
        // exactly matched to the terrain)
        Vector3 tempVEC = myBody.velocity;
        tempVEC.x = 0;
        tempVEC.z = 0;
        myBody.velocity = tempVEC;
    }
}
```

steer, motor and brake are float variables used for moving the vehicle around. GetInput() uses Math.Clamp to keep them to reasonable values as they are set by the default input:

```csharp
public virtual void GetInput()
{
    // calculate steering amount
    steer= Math.Clamp(default_input.GetHorizontal() , -1, 1);

    // how much accelerator?
    motor= Math.Clamp(default_input.GetVertical() , 0, 1);

    // how much brake?
    brake= -1 * Math.Clamp(default_input.GetVertical() , -1, 0);
}
```

## 5.3.2 Wheel Alignment

WheelColliders do a great job of acting like wheels, but if we want to see wheels, there is still more work to be done; each wheel mesh needs to be positioned to match that of its WheelCollider counterpart.
The script in full looks like this:

> // based on work done in this forum post:
// http://forum.unity3d.com/threads/50643-How-to-make-a-physically-real-
// stable-car-with-WheelColliders
// by Edy.

```csharp
using UnityEngine;
using System.Collections;
```

```csharp
public class BaseWheelAlignment : MonoBehaviour
{

// Define the variables used in the script, the Corresponding
// collider the wheel collider at the position of
// the visible wheel slide, the slip prefab is the prefab instantiated
// when the wheels slide, the rotation value is the
// value used to rotate the wheel around its axle.
public WheelCollider CorrespondingCollider;
public GameObject slipPrefab;
public float slipAmountForTireSmoke = 50f;
```

```csharp
private float RotationValue = 0.0f;
private Transform myTransform;
private Quaternion zeroRotation;
private Transform colliderTransform;
private float slipSuspensionDistance;
```

```csharp
void Start () {
    // cache some commonly used things...
    myTransform = transform;
    zeroRotation = Quaternion.identity;
    colliderTransform = CorrespondingCollider.transform;
}
```

```csharp
void Update () {
    // define a hit point for the raycast collision
    RaycastHit hit;
// Find the collider's center point, you need to do this
// because the center of the collider might not actually be
// the real position if the transform's off.
Vector3 ColliderCenterPoint = colliderTransform.TransformPoint(CorrespondingCollider.center);
// now cast a ray from the wheel collider's center the
// distance of the suspension, if it hit something, then use
// the "hit" variable's data to find where the
// wheel hit, if it didn't, then set the wheel
// to be fully extended along the suspension.
    if (Physics.Raycast(ColliderCenterPoint, colliderTransform.up, hit, CorrespondingCollider.suspensionDistance + CorrespondingCollider.radius)) {
        myTransform.position = hit.point + (colliderTransform.up * CorrespondingCollider.radius);
    }
    else {
        myTransform.position = ColliderCenterPoint -
        (colliderTransform.up * CorrespondingCollider.suspensionDistance);
    }

// now set the wheel rotation to the rotation of the
// collider combined with a new rotation value. This new value
// is the rotation around the axle, and the rotation from
// steering input.

myTransform.rotation= colliderTransform.rotation *
Quaternion.Euler( RotationAngle, CorrespondingCollider.steerAngle, 0 );

// increase the value by the rotation speed (in
// degrees per second)
RotationValue+= CorrespondingCollider.rpm * ( 360 / 60 ) *
Time.deltaTime;

// define a wheelhit object, this stores all of the data
from the wheel collider and will allow us to determine
slip of the tire.
WheelHit correspondingGroundHit= new WheelHit();
CorrespondingCollider.GetGroundHit(out correspondingGroundHit );

// if the slip of the tire is greater than 2.0f, and the
// slip prefab exists, create an instance of it on the ground at
// a zero rotation.
if ( Math.Abs(correspondingGroundHit.sidewaysSlip) > slipAmountForTireSmoke ) {
    if ( slipPrefab ) {
      SpawnController.Instance.Spawn( slipPrefab,
correspondingGroundHit.point, zeroRotation );
    }
}
```

## 5.3.3 Script Breakdown

The BaseWheelAlignment.cs script may be used to align the wheel meshes to the wheel colliders, as well as provide a little extra functionality in spawning tire smoke as we is slipping. The smoke is optional, of course, but it is here in case you need it.

Each wheel should have a BaseWheelAlignment script attached to it (i.e., the wheel mesh not the WheelCollider) and then a reference to the WheelCollider component provided to this script via the Unity editor inspector, to the variable named CorrespondingCollider. The wheels should be independent of the WheelColliders for them to move correctly; do not parent the wheel meshes to the colliders.

In the example Metal Vehicle Doom, the vehicle looks like this in the hierarchy

- Car
- Body
- Colliders (body)
- WheelColliders
- Wheel_FL
- Wheel_FR
- Wheel_RL
- Wheel_RR
- WheelMeshes
- Wheel_FL
- Wheel_FR
- Wheel_RL
- Wheel_RR

The script derives from MonoBehaviour so that it can tap into the engine's Update() function:

```csharp
using UnityEngine;
using System.Collections;

public class BaseWheelAlignment : MonoBehaviour
{
```
