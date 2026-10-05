![](bbox=[0.315, 0.025, 0.715, 0.305])

Figure 14.3 The Standard_Slot Weapon Controller weapons slots with prefabs setup.

weaponController.NextWeaponSlot() tells the controller to move to the next slot:

```
void OnTriggerEnter(Collider other)
{
    if (other.gameObject.layer==12 )
    {
        // tell our sound controller to play a powerup sound
        BaseSoundController.Instance.PlaySoundByIndex( 3,
        myTransform.position );

        // hit a powerup trigger
        Destroy (other.gameObject);

        // advance to the next weapon
        weaponControl.NextWeaponSlot( false);
    }
}
```

LostLife() is called when the player is hit by an enemy projectile:

```
void LostLife()
{}
```

The respawning process takes a little time, so isRespawning is a Boolean to ensure that it does not try to respawn more than once at the same time:

isRespawning=true;

The game controller's PlayerHit() function will make a nice explosion effect at the position of the transform passed into it:

```
// blow us up!
GameController_IP.Instance.PlayerHit ( myTransform );
```