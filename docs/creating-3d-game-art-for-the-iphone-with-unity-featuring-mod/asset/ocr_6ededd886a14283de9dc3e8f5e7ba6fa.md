```
~~~csharp
public var radius : float = 5.0;
public var power : float = 10.0;
public var upModifier : float = 1.0;
public var particle : ParticleEmitter;
//private var colliders : Collider[];
private var colliders : Collider[];
private var explosionPos : Vector3;

function Awake() {
    explosionPos = transform.position;
    colliders = Physics.OverlapSphere(explosionPos, radius);
    //Set Rigidbodies to Sleep
    for (var hit : Collider in colliders) {
        if (hit.rigidbody) {
            hit.rigidbody.Sleep();
        }
    }
}

//Follow up target
function Explode () {
    for (var hit : Collider in colliders) {
        if (!hit) {
            continue;
        }

        if (hit.rigidbody) {
            hit.rigidbody.AddExplosionForce(power, explosionPos, radius, upModifier);
            Debug.Log("Adding force to " + hit);
            hit.rigidbody.Sleep();
        }
    }
}
~~~
```

FIG 9.22 These Highlighted Areas Show the Key Areas of the Script for Creating the Explosion

# ## Adding Particles

If we're exploding the target from a gun blast, then we'll have to have some fire and smoke, and Unity's Particle System will be perfect to create this effect as shown in Fig. 9.23.

I simply used the explosion particle Prefab that I got from the Desktop version of Unity iOS and tweaked it to the desired settings and positioned the Emitter at the center of the target. Next, I disabled the Emit parameter and activated One Shot so that particles would only emit once on the Emitter as shown in Fig. 9.24.

![](bbox=[0.33, 0.622, 0.925, 0.848])

FIG 9.23 Unity's Particle System Is Great for Creating Fire and Smoke for Our Explosion Effect