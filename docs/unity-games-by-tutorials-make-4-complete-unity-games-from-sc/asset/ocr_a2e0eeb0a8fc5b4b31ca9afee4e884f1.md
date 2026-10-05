```
pickupShotgunAmmo();
break;
default:
    Debug.LogError("Bad pickup type passed" + pickupType);
    break;
}
}
```

Going over what you've added:

PickupItem() takes an item that represents the type of item being picked up. Now that the Player script can process picking up an item, it's time to create the pickup prefabs.

The Constants file references the IDs of all pickups. These IDs correspond to the five types of pickups. The ID passed into the PickupItem() will be one of these values.

Save your work and switch back to Unity. Create a C# script, name it Pickup and add the following inside the class:

```
public int type;
```

This represents the type of the pickup. Now add the following:

```
void OnTriggerEnter(Collider collider)
{
    if (collider.gameObject.GetComponent<Player>() != null
    && collider.gameObject.tag == "Player")
    {
        collider.gameObject.GetComponent<Player>().PickupItem(type);
        Destroy(gameObject);
    }
}
```

This listens for a collision with the Player GameObject, calls PickupItem() on it, passes along its item type, and then destroys itself. You will add the respawn mechanics shortly.

Save your work and switch back to Unity.

In the Resources folder, select the PickupAmmoAssaultRifle, PickupAmmoPistol, PickupAmmoShotgun, PickupHealth and PickupArmor prefabs. With all of those selected, click the Add Component from the scripts gallery and select the Pickup script.

Next, add a Rigidbody. Check the Is Kinematic box. Finally, add a Box Collider. Check the Is Trigger checkbox and set the Size to (1.5, 1.5, 1.5).