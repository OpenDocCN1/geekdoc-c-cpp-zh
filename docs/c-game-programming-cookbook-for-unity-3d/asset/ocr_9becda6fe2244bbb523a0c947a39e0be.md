# 4.5.1 Script Breakdown

The script derives from MonoBehavior to tap into the Start() and FixedUpdate() system calls:

```
public class PretendFriction : MonoBehavior
{
    void Start ()
    {
        // cache some references to our rigidbody, mass and
        // transform
        myBody=rigidbody;
        myMass=myBody.mass;
        myTransform=transform;
    }\}
```

The Start() function caches the rigidbody, the amount of mass on the rigidbody and on the transform:

The FixedUpdate() function will calculate how much an object is sliding—to do this, it finds how much sideways the object is making (to the right relative to the transform's rotation)—to find out how much slip is happening:

```
void FixedUpdate ()\{
    // grab the values we need to calculate grip
    myRight=myTransform.right;

    // calculate flat velocity
    velo=myBody.velocity;
    flatVelo.x=velo.x;
    flatVelo.y=0;
    flatVelo.z=velo.z;

    // calculate how much we are sliding
    slideSpeed=Vector3.Dot(myRight,flatVelo);

    // build a new Vector to compensate for the sliding
    TEMPvec3 c=myRight * (-slideSpeed) * myMass * theGrip;

    // apply the correctional force to the rigidbody
    myBody.AddForce(TEMPvec3 * Time.deltaTime);
}
```

# 4.6 Cameras

There are just two camera scripts for the example games in this book. Those are a third-person camera (a camera that sits behind and orbits the player) and a top-down camera (a camera that sits above the player, looking down). They use a simple interface for other scripts to be able to communicate with them, and both cameras should provide a good starting point for camera systems in your own games.