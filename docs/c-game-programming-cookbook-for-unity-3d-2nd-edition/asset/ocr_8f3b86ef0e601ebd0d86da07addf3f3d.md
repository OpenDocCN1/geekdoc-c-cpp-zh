```
public override void Init()
{
    base.Init();
    // now get on and chase it!
    SetAIState(AISTates.AIState.chasing_target);
}
```

Above, we override BaseAIController's Start() function with this one. It calls the Init() function to get set up. Init() calls its base class equivalent then sets the AI's state to AI.States.AIState.chasing_target so that our bots will start moving right away.

```
public override void Update()
{
    base.Update();
}
```

We only need the base class to update, so that's all we do here.

```
public void OnCollisionEnter(Collision collider)
{
    if (IsInLayerMask(collider.gameObject.layer, projectileLayerMask))
    {
        ReduceHealth();
        if (GetHealth() <= 0)
        {
            Instantiate(explosionPrefab, _TK.position, _TK.rotation);
            BlasterGameManager.instance.EnemyDestroyed();
            Destroy(gameObject);
        }
    }
}
```

Above, when OnCollisionEnter() gets called by the engine, we check to see if it is a projectile hitting the bot. If it is, health is reduced by 1 and there's a check to see if our enemy health is depleted. If the health is at (or below) 0, explosionPrefab is instantiated at our position. BlasterGameManager's instance gets informed of the enemy demise via EnemyDestroyed() and then we use Unity's Destroy() function to remove the enemy GameObject from the Scene.

# 15.3.4 Weapons and Projectiles

Our EnemyBot prefab uses two Components for its weapons system. Those are; AI Weapon Controller and a Standard Slot Controller. The Standard Slot Controller is the system provided as part of the framework for dealing with weapons – we use the exact same Component on the player. It is the AI Weapon Controller that accesses StandardSlotController to tell it when to fire.

The main weapon (a prefab named Blaster_1) has a cylinder that looks like a weapon with a single Component attached to it – BaseWeaponScript – and it contains a reference to a projectile named Blast that will be instantiated whenever it fires. For more on the weapon system, see Chapter 7.

# 15.3.5 User Interface

The UI script derives from BaseUIDataManager, the standard UI script shown in Chapter 10. The BaseUIDataManager declares several common variables and provides some basic functions to deal with them: