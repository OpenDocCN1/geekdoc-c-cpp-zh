```
// firing isn't in the default spaceship
// (BaseTopSpaceShip.cs) behavior, so we add it here
fire_input= mouse_input.GetFire();
{
    // we're overriding the default input function to add in the
    // ability to fire
    horizontal_input= default_input.GetHorizontal();
    vertical_input= default_input.GetVertical();
}
```

The BaseTopSpaceShip controller script only includes code to move the spaceship around and not to fire, so we need to add some code here to detect the fire button from the default input controller and set the variable fire_input:

```
fire_input= default_input.GetFire();
```

}

The enemy projectiles are on layer 17—named enemy_projectile—which is set by the weapon's mounting point. Whoever the mounting point is set at will be used for its projectiles. Here OnEnter() looks for collisions between the player and the enemy projectiles to see whether or not the player should lose a life:

```
void OnCollisionEnter(Collision collider)
{
```

The collider belonging to the other object involved in a collision is passed by the engine, as a parameter, to this function. The collider's gameObject layer is checked to see whether it matches the enemy projectile layer 17. If the player is not respawning and is not set to be invulnerable, we can go ahead and call the LostLife() function:

```
if(gameObject.layer==17 && !isRespawning &&
nisInvulnerable)
{
    LostLife();
}
```

Power-ups, which upgrade the weapon, gameObjects with box colliders on that are set to be triggers (the IsTrigger property of the collider set to true via the Unity Inspector window). When the player hits the trigger, a sound is played and the power-up is destroyed. To upgrade the weapon, the weapon controller is told to advance to the next weapon slot.

What this means is that the weapon system should be set up so that the lowestpowered weapon is in the first slot, and progressively, more powerful weapons set in each slot up from there. Adding and setting up weapons are simply a case of using the Unity editor Inspector window (with the player gameObject selected) and dragging in the prefabs for each weapon into the array of the Standard_Slot Weapon Controller (see Figure 14.3).