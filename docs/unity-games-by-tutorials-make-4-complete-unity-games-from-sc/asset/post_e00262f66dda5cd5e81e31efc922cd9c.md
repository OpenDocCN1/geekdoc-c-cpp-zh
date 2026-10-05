
Select the StoneProjectile prefab in the Prefabs > Tower > Weapons folder and add the Stone to it. You can do that by first selecting the prefab. Then in your Inspector panel, click the Add Component button at the bottom. Then search for 'Stone' and select the script:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_540_0.png)

Now, drag the StoneProjectile prefab to StoneTower's Stone Prefab field:

| Assets > Prefabs > Tower > Weapons |
| :--- |
| Target Enemy None (Enemy) |
| StoneProjectile StonePrefab None (Game Object) |

Now the StoneTower script needs a little addition before the projectile will work as it should. Open up the StoneTower script (Scripts > Game > Tower folder) and add these shooting them down! and add these lines right under the Instantiate line:

```
stone.GetComponent<Stone>().enemyToFollow = targetEnemy;
stone.GetComponent<Stone>().damage = attackPower;
```

Give the stone projectile an enemy to follow and an amount of damage to deal to enemies.

Save the script and return to Unity; StoneTower is ready to go. Press the Apply button to save the changes back into the prefab.

Save the scene and prepare for awomeness! Duplicate the StoneTower in the Hierarchy a few times and move them around, using snapping to get them right on the center of the tiles.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_540_1.png)

Press the Play button to see the towers looking at enemies and shooting them! Now, delete the StoneTower and its duplicates from the scene and save the scene.

## Tower Manager

The TowerManager handles creating new towers and holds the prices for the different towers.

Create a new C Script named TowerManager inside the Scripts > Game > Tower folder and open it in a code editor. Completely remove the Start() and Update() methods and add these lines under the other statements:

```
using System;
using System.Collections.Generic;
using System.Linq;
```

Add the following struct right above public class TowerManager : MonoBehaviour :

```
[Serializable]
public struct TowerCost
{
    public TowerType TowerType;
    public int Cost;
}
```

This will let the script use an external, easily editable list of prices.

Now, inside the class, add this code:

```
//1
public static TowerManager Instance;

//2
public GameObject stoneTowerPrefab;
public GameObject fireTowerPrefab;
public GameObject iceTowerPrefab;

//3
public List<TowerCost> TowerCosts = new List<TowerCost>();

//4
void Awake()
{
    Instance = this;
}

//5
public void CreateNewTower(GameObject slotToFill, TowerType towerType)
{
    switch (towerType)
    {
        case TowerType.Stone:
            Instantiate(stoneTowerPrefab, slotToFill.transform.position, Quaternion.identity);
            slotToFill.gameObject.SetActive(false);
            break;
```

Unity Games by Tutorials

Chapter 19: Making Towers

```
case TowerType.Fire:
    Instantiate(fireTowerPrefab, slotToFill.transform.position,
    Quaternion.identity);
    slotToFill.gameObject.SetActive(false);
    break;
case TowerType.Ice:
    Instantiate(iceTowerPrefab, slotToFill.transform.position,
    Quaternion.identity);
    slotToFill.gameObject.SetActive(false);
    break;
}
// //
public int GetTowerPrice(TowerType towerType)
{
    return (from towerCost in TowerCosts
            where towerCost.TowerType
            == towerType
            select towerCost.Cost).FirstOrDefault();
}
```

Here’s how it works:

- 1. As this is another singleton, a static reference to this script is stored away in Instance.
- 2. References to the tower prefabs, needed to spawn new instances.
- 3. Store the cost of each type of tower in a list.
- 4. Sets the Instance variable to this script.
- 5. Accepts a tower slot and a type of tower as parameters, and create a new copy of the chosen tower at the position of the tower slot. It also disables the tower slot so you can’t place two towers on one slot.
- 6. A LINQ utility method to easily get the price of a tower type.

Now save the script and hop back into Unity.

In the Hierarchy, create a new empty GameObject. Name it TowerManager and parent it to Managers. Add the TowerManager script to it using the Add Component button in the Inspector panel and searching for it.

raywenderlich.com

543

Unity Games by Tutorials

Chapter 19: Making Towers

| Tower Manager (Script) | |
| :--- | :--- |
| Script | TowerManager |
| Stone Tower Prefab | None (Game Object) |
| Fire Tower Prefab | None (Game Object) |
| Ice Tower Prefab | None (Game Object) |
| Tower Costs | |
| Size | 0 |

Drag the StoneTower prefab from the Prefabs ▸ Tower folder onto the Stone Tower Prefab field.

| Tower Manager (Script) | |
| :--- | :--- |
| Script | TowerManager |
| Stone Tower Prefab | None (Game Object) |
| Fire Tower Prefab | None (Game Object) |
| Ice Tower Prefab | None (Game Object) |
| Tower Costs | |
| Size | 0 |
| | Add Component |

The other towers aren't ready yet, so ignore the two other tower fields for now. Set the Tower Costs Size to 3:

| Tower Costs | |
| :--- | :--- |
| Size | 3 |
| Element 0 | |
| Tower Type | Stone |
| Cost | 0 |
| Element 1 | |
| Tower Type | Stone |
| Cost | 0 |
| Element 2 | |
| Tower Type | Stone |
| Cost | 0 |

Change the list as follows:

- Leave the first entry's Tower Type set to Stone and change its Cost to 100.
- Set the second Tower Type to Fire and change its Cost to 200.
- Change the last Tower Type to Ice and set the Cost to 150.

raywenderlich.com

544

The Tower Manager is now ready for use! Before you can buy new towers though,
Screen Canvas' child AddTowerWindow needs a script to link its UI to
TowerManager.

## Linking the UI

Create a new C Script named AddTowerWindow inside the Scripts > Game > UI folder. Open the script and add this to the top:

```
using System;
```

Now remove the Start() and Update() methods and insert the following block in their place:

```
//1
public GameObject towerSlotToAddTo;
//2
public void AddTower(string towerAsString)
{
//3
    TowerType type = (TowerType)Enum.Parse(typeof(TowerType), towerAsString);
//4
    if (TowerManager.Instance.GetTowerPrice(type) <= GameManager.Instance.gold)
//5
    GameManager.Instance.gold -= TowerManager.Instance.GetTowerPrice(type);
//6
    TowerManager.Instance.NewTower(towerSlotToAddTo, type);
    gameObject.SetActive(false);
}
```

Here's what each comment references:

- 1. The reference to the tower slot where the tower should be built.
- 2. The AddTower() method takes a single string parameter: The tower's type.
- 3. Convert the string parameter that was passed into the TowerType enum. The reason why the method doesn't simply the TowerType as a parameter because enums are not supported for Event Triggers.
- 4. Check that the player has enough gold to afford the tower.
- 5. Subtract the tower's price from the player's gold.
- 6. CreateNewTower() on the TowerManager and disable the AddTowerWindow.

545

Unity Games by Tutorials

That's it for the AddTowerWindow script. Save it and return to Unity.

In the Hierarchy, select and enable AddTowerWindow, which is a child GameObject under Screen Canvas. Add the AddTowerWindow script to it using the Add Component in the Inspector panel and searching for it or dragging it from the Project panel.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_545_0.png)

Drag TowerSlot from the Hierarchy to the TowerAddToTo field in the Inspector panel.

Time to link up the buttons to allow the creation of towers in the future.

In the Hierarchy, expand the GameObject AddTowerWindow, expand its child GameObject HorizontalLayout. Select its child BtnStoneTower and drag the AddTowerWindow GameObject from the Hierarchy to the On Click () Object field.

Click the method drop-down — that is, the drop-down where No Function is currently selected. Select AddTowerWindow.AddTower(string) in the method dropdown. In the parameter field under the drop-down, insert Stone if it isn't inserted automatically.

Select BtnFireTower. Do the same as you did for stone, but insert Fire in the parameter field under the drop-down.

Finally, select BtnIceTower. Do the same as you did for stone and fire, but this time insert Ice in the parameter field under the drop-down.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_545_1.png)

The buttons are all set to go now. Disable the AddTowerWindow GameObject and move on to the next part so you can actually build some towers!
