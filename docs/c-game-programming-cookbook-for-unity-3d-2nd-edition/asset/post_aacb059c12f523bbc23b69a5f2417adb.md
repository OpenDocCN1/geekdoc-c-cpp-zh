
array of weapons starts at zero, we deduct 1 to find the last entry). During validation, if the value of slotNum is too high, it will be set to the nearest valid number – that way, the function will not fail in setting the weapon because of a bad value in slotNum:

```
```
// we store this selected slot to use to prevent
duplicate weapon slot setting
lastSelectedWeaponSlot= selectedWeaponSlot;
```
```

Now that selectedWeaponSlot has been set, lastSelectedWeaponSlot needs updating to the latest slot number:

```
```
// enable the newly selected weapon
EnableCurrentWeapon();
}
```
```

A call to EnableCurrentWeapon() will take the value of selectedWeaponSlot and activate the currently selected weapon:

```
```
public virtual void NextWeaponSlot (bool shouldLoop)
{
```
```

The NextWeaponSlot() takes a Boolean parameter to tell the function whether or not to loop around from the last weapon to the first. If the shouldLoop parameter is false and the current weapon is already set to the last available weapon, it will return the same weapon instead of looping around to zero and returning the weapon from the first slot:

```
```
// disable the current weapon
DisableCurrentWeapon();
```
```

First, the current weapon is disabled in anticipation of setting a new one:

```
```
// next slot
selectedWeaponSlot++;

// make sure that the slot isn't higher than the
total number of weapons in our list
if(selectedWeaponSlot==weaponScripts.Count)
{
    if(shouldLoop)
    {
        selectedWeaponSlot= 0;
    } else {
        selectedWeaponSlot=
weaponScripts.Count-1;
    }
}
```
```

selectedWeaponSlot index number is incremented and validated to make sure that it now contains a valid index number (this is where the slot number will be looped back to zero if it goes over the total number of available weapons):

```
```
// we store this selected slot to use to prevent
duplicate weapon slot setting
lastSelectedWeaponSlot=selectedWeaponSlot;
// enable the newly selected weapon
EnableCurrentWeapon();
}
```
```

The lastSelectedWeaponSlot gets updated before the new current weapon is enabled, completing the function:

```
public virtual void PrevWeaponSlot (bool shouldLoop)
{
    // disable the current weapon
    DisableCurrentWeapon();

    // prev slot
    selectedWeaponSlot--;

    // make sure that the slot is a sensible number
    if( selectedWeaponSlot<0 )
    {
        if(shouldLoop)
        {
            selectedWeaponSlot=
            weaponScripts.Count-1;
        } else {
            selectedWeaponSlot= 0;
        }
    }
    // we store this selected slot to use to prevent duplicate weapon slot setting
    lastSelectedWeaponSlot=selectedWeaponSlot;

    // enable the newly selected weapon
    EnableCurrentWeapon();
}
```

PrevWeaponSlot works in almost exactly the same way as NextWeaponSlot(). It has a Boolean parameter to state whether to loop around if the current weapon slot drops below 0 and the most obvious difference is that the selectedWeaponSlot variable is decremented rather than incremented:

```
public virtual void DisableCurrentWeapon ()
{
```

Disabling the current weapon means that it will be both invisible and unable to fire:

```
if(weaponScripts.Count==0)
    return;
```

To disable the weapon, the script will need to talk to the BaseWeaponScript.cs attached to it. Since weaponScripts and weaponSlots Lists were created in the same order, the selectedWeaponSlot can be used as the index for either array.

To make sure that there are scripts in the weaponScripts array, its Count property is checked before going any further:

```
// grab reference to currently selected weapon script
TEMPWeapon = ( BaseWeaponScript )weaponScripts[selectedWeaponSlot];
```

A reference to the currently selected weapon slot's weapon class (BaseWeaponScript) is stored in the variable TEMPWeapon as it is retrieved from the weaponScripts List:

```
// now tell the script to disable itself
TEMPWeapon.Disable();
```

To tell the weapon to disable, it's a call to its Disable() function:

```
disable that, too    // grab reference to the weapon's gameObject and
GameObject _tempGO = (GameObject)_weaponSlots[selectedWeaponSlot];
_tempGO.SetActive(false);
```

As well as disabling the actual weapon script, it now needs to be hidden from view. First, variable _tempGO receives a reference to the weapon's GameObject from the weaponSlots List. The _tempGO is then set to inactive by GameObject.SetActive():

```
public virtual void EnableCurrentWeapon ()
{
    if( weaponScripts.Count==0 )
        return;

    // grab reference to currently selected weapon
    TEMPweapon=
    ( BaseWeaponScript )weaponScripts[selectedWeaponSlot];

    // now tell the script to enable itself
    TEMPweapon.Enable();

    GameObject _tempGO =
    ( GameObject )weaponSlots[selectedWeaponSlot];
    _tempGO.SetActive( true );
}
```

Enabling the currently selected weapon is done by the EnableCurrentWeapon() function, which works almost exactly the same as DisableCurrentWeapon() except that it calls the Enable() function of the BaseWeaponScript instead of Disable():

```
public virtual void Fire ()
{
```

By default, the Fire() function will launch projectiles along the Transform's forward axis, but there is support for firing along a fixed vector by setting the useForceVectorDirection to true.

The function takes no parameters, making it easy to call from any other script:

```
if(weaponScripts==null)
    return;
if(weaponScripts.Count==0)
    return;
```

The weaponScripts List is checked to make sure that it has been properly initialized and that it contains entries (a quick count check):

```
// find the weapon in the currently selected slot
TEMPweapon=
( BaseWeaponScript )weaponScripts[selectedWeaponSlot];
```

TEMPWeapon gets a reference to the currently selected weapon's script from the weaponScripts array:

```
theDir = _TR.forward;
```

By default, the firing direction is along our Transform's forward vector:

```
if( useForceVectorDirection )
    theDir = forceVector;
```

When useForceVectorDirection is set to true, theDir is set to the vector from the variable forceVector, which should be set in the Unity editor Inspector window on the GameObject:

```
// fire the projectile
TEMPWeapon.Fire( theDir, ownerNum );
```

The ownerNum was mentioned earlier in this section, where it is set by the SetOwner() function. When the call to the currently selected weapon's Fire() function goes out, it takes a Vector3, and the owner ID.

## 7.1.2 BaseWeaponScript

The BaseWeaponScript class derives from ExtendedCustomMonoBehaviour:

```
using UnityEngine;
namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Base/Base Weapon Script")]
    public class BaseWeaponScript : ExtendedCustomMonoBehaviour
    {
        public bool canFire;
        public int ammo = 100;
        public int maxAmmo = 100;
        public bool isInfiniteAmmo;
        public GameObject _projectilePrefab;
        public Collider _parentCollider;
        public Transform _spawnPositionTR;
        public float fireDelay = 0.2f;
        public float projectileSpeed = 10f;
        public bool inheritVelocity;

        [System.NonSerialized]
        public Transform _theProjectile;

        private bool isLoaded;

        public virtual void Start()
        {
            Init();
        }

        public virtual void Init()
        {
            _TR = transform;
            Reloaded();
        }

```

Start() calls Init(). Init() begins by grabbing a reference to the Transform. A call to Reloaded() ensures that the weapon will be loaded and ready to go from the start.

```
public virtual void Enable()
{
    canFire=true;
```

```
}
public virtual void Disable()
{
    canFire=false;
}
```

The Enable() or Disable() functions set the Boolean variable canFire to true or false, respectively. This will be checked elsewhere in the code before allowing any projectile firing. Note that the visual representation of the weapon is not hidden here; that task is left to the slot control script to deal with, rather than the weapon itself:

```
public virtual void Reloaded()
{
    // the 'isLoaded' var tells us if this weapon is
    loaded and ready to fire
    isLoaded= true;
}
```

When the weapon is fired, the assumption is made that it will not be loaded for a certain period (otherwise you could in theory fire out thousands of projectiles each second). To keep a track of when the weapon is in a loaded state, this script uses the Boolean variable isLoaded. A timed call to the Reloaded() function, after firing, will reset the weapon state again:

```
public virtual void SetCollider( Collider aCollider )
{
    _parentCollider= aCollider;
}
```

SetCollider() is used to set a collider to be ignored by a projectile. For example, when the script is applied to a player it should ignore the player's collider to prevent the newly created projectile from exploding instantly. It should be set, using the Unity editor Inspector window, to a collider that would likely destroy the projectile as it was spawned. If no parentCollider is set, the script will still work, but the projectile will not ignore any collider:

```
public virtual void Fire( Vector3 aDirection, int ownerID )
{
```

The Fire() function takes two parameters, a Vector3 to represent the direction of fire and an integer providing an ID number for its owner (which gets used primarily by collision code to know how to react):

```
if( !canFire )
    return;

// if the weapon is not loaded, drop out
if( !isLoaded )
    return;
```

The Boolean variable canFire needs to be true (the weapon can fire) and isLoaded needs to be true (the weapon is ready to fire) before the function can progress to check the state of ammunition:

```
// if we're out of ammo and we do not have infinite
ammo, drop out..
if( ammo<=0 && !isInfiniteAmmo )
    return;
```
