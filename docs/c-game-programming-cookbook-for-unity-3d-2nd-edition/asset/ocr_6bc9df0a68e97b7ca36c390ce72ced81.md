```
```csharp
        playerAvatarParent.SetActive(false);

        // reduce this player's lives by 1
        ReduceLives(1);

        // tell game manager that the player was destroyed
        BlasterGameManager.instance.PlayerDestroyed();

    }

}
```
```

Above, when PlayerDestroyed() is called we first set a flag _controller.isRespawning to avoid registering any more projectile hits/health losses and/or duplicate respawn calls. playerAvatarParent is a variable containing the GameObject above our player's avatar in the Hierarchy, and here we call SetActive() on it to make it inactive in the Scene. This will hide the parent GameObject and any child objects, too, so the entire player should become invisible to the player. As the player has been destroyed, we call ReduceLives() (all stats functions like this are in that BasePlayerStatsController class, by the way!) and finally call out to the BlasterGameManager instance to register the player destruction with it. BlasterGameManager will then take care of reloading the Scene to reset the game state and restart the level.

# ### 15.3.3 Enemy Bots and the BlasterEnemyBot Class

When it comes to inheritance, there is a three class chain leading up to BlasterEnemyBot:

BlasterEnemyBot>BaseEnemyStatsController>BaseAIController>ExtendedCustomMonoBehaviour.

BaseAIController is a class full of utility functions for dealing with AI, such as waypoint management, and movement. On its own, it does not do anything until we tell it what to do. BaseEnemyStatsController is the equivalent of BasePlayerStatsController only for enemies. It holds information about the enemy's health, score, and name and can be expanded to hold any information you like. BlasterEnemyBot.cs brings BaseEnemyStatsController and BaseAIController together, to form the AI for our enemy bot.

The inherited classes means that BlasterEnemyBot is a relatively small script which derives from AIBotController, as described in Chapter 10, Section 10.4, of this book.

```
```csharp
using UnityEngine;
using GPC;

public class BlasterEnemyBot : AIBotController
{
    [Header("Game specific")]
    public bool isRespawning;
    public bool isBoss;

    [Header("Weapons and hits")]
    public BaseEnemyWeaponController _weaponController;
    public LayerMask projectileLayerMask;
    public Transform _explosionPrefab;

    public override void Start()
    {
        Init();
    }
}
```
```