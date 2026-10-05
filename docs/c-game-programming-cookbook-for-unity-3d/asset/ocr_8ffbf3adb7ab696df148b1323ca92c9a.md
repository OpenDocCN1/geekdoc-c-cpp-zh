# RaycastHit;

The raycast starts at the position of the waypoint (from tempEC) with 300 units added up to it, to ensure that the raycast starts below the ground. The ray direction is -Vector3.up (straight down), but in this call to Physics.Raycast, there is no distance-set, and the ray should detect everything below it no matter how far away:

```
if (Physics.Raycast(tempV + (Vector3.up * 300),
    -Vector3.up, out hit))
{
    tempVEC.y=hit.point.y-15;
}
```

myTransform is ready to be set up to its new position and rotation:

```
// reposition the player at tempVEC (the waypoint position)
// with a corrected y value via raycast and also we set the
// player rotation to the waypoint's rotation so that we are
// facing in the right direction after respawning
myTransform.rotation=tempTR.rotation;
myTransform.position=tempVEC;
```

After the respawn, the player is made invulnerable (by a call to MakeInvulnerable function). Invoke() is used to schedule a call to MakeInvulnerable in 3 s time, limiting the player invulnerability time:

```
// we need to be invulnerable for a little while
MakeInvulnerable();
```

```
Invoke ("MakeVulnerable", 3);
```

Whenever a respawn happens, the weapon is reset to its default setting of using the first slot:

```
// revert to the first weapon
if (weaponControl==null)
    weaponControl.SetWeaponSlot(0);
```

The MakeInvulnerable() and MakeVulnerable() functions just set the isInvulnerable Boolean variable to true or false, respectively. WhenInvulnerable is true, the collision function (OnCollisionEnter()) from earlier in this script will ignore collisions with the projectiles' layer:

```
void MakeInvulnerable()
{
    isInvulnerable=true;
}

void MakeVulnerable()
{
    isInvulnerable=false;
}
```