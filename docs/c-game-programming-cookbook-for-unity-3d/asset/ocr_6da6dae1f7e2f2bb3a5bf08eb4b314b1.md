# 6.1.2.1 Script Breakdown

The BaseWeaponScript class derives from MonoBehavior:

using UnityEngine;
using System.Collections.

```
public class BaseWeaponScript : MonoBehaviour
{
    public virtual void Start()
    {
        Init();
    }
}
```

Init() begins grabbing a reference to the transform and the layer at which this gameObject with this script attached to is set. This will be used to disable collisions between the layer of the weapon and the actual projectile so that the projectile does not explode as soon as it is instantiated: Init()

```
public virtual void Init()
{
    // cache the transform
    myTransform= transform;

    // cache the layer (we'll set all projectiles to avoid
    // layer in collisions so that things don't
    // themselves!)
    myLayer= gameObject.layer;

    // load the weapon
    Reloaded();
}
```

The Enable() and Disable() functions set the Boolean variable canFire to true and false, respectively. This will be checked elsewhere in the code before allowing any projectile firing. Note that the visual representation of the weapon is not hidden here; that task is left to the slot control script to deal with rather than the weapon itself:

```
public virtual void Enable()
{
    canFire=true;
}

public virtual void Disable()
{
    canFire=false;
}
```

When the weapon is fired, the assumption is made that it will not be loaded for a certain period of time (otherwise, you could, in theory, fire thousands of projectiles each second). To keep track of when the weapon is in a loaded state, this script uses the