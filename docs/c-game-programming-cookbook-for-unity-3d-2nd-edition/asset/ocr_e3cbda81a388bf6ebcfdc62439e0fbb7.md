```
```csharp
public void OnCollisionEnter(Collision collider)
{
    if (IsInLayerMask(collider.gameObject.layer,
projectileLayerMask) && !_controller.isRespawning)
    {
```
```

Unity’s collision system will automatically call the OnCollisionEnter() function above, where we can identify what it was that collided with the player and react to it. To do this, we start out by comparing the layer of the Collider that hit the player to the projectileLayerMask. This will tell us if the player has been hit by a projectile from an enemy.

BasePlayerStatsController, the class this class derives from, in turn derives from ExtendedCustomMonoBehaviour. ExtendedCustomMonoBehaviour provides a function named IsInLayerMask(), which can be used to find out if a specified layer fall within a LayerMask (which is a collection of layers). To use IsInLayerMask, we pass in the layer you want to check as the first parameter and the LayerMask as the second. Above, we pass in the Collider’s GameObject’s layer to look for and the projectileLayerMask LayerMask as the LayerMask to look at.

When the player dies, before respawning the player object is hidden but it still exists in the game world and can still receive collision events. It is for this reason that we make sure the player is not respawning by checking against _controller.isRespawning.

```
```csharp
ReduceHealth(1);

if (GetHealth() <= 0)
{
    Instantiate(explosionPrefab, _TR.position,
_TR.rotation);

    // need to respawn, or reload the current
level here... life lost!
    PlayerDestroyed();
}
}
}
```
```

If we know the Collider that hit the player is a projectile and we are not respawning, we go ahead and reduce the player’s health stat by 1. Below that, we take a look at GetHealth() to see if it is less or equal to 0. Since the player only has one health in this game, one hit has the effect of killing the player instantly. If you want to make the player have more than one chance before getting destroyed by a projectile, you could change the SetHealth() statement in the Init() function near the top of the class.

If GetHealth() says the health level is less or equal to 0, Instantiate creates an explosion effect in the Scene, courtesy of the explosionPrefab prefab and positioned at the player’s Transform position and rotation. We then call the PlayerDestroyed() function to deal with the next steps:

```
```csharp
void PlayerDestroyed()
{
    _controller.isRespawning = true;

    // hide the avatar / visual representation of a
player!
```
```