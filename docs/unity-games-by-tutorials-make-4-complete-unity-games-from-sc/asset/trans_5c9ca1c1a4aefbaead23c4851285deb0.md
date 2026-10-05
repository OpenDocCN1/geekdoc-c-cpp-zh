
在 Prefabs > Tower > Weapons 文件夹中选择 StoneProjectile 预制体，并将 Stone 添加进去。你可以先选择该预制体来实现这一点。然后在你的 Inspector（检查器）面板中，点击底部的 Add Component（添加组件）按钮。然后搜索 'Stone' 并选择该脚本：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_540_0.png)

现在，将 StoneProjectile 预制体拖到 StoneTower 脚本的 Stone Prefab 字段中：

| Assets > Prefabs > Tower > Weapons |
| :--- |
| Target Enemy None (Enemy) |
| StoneProjectile StonePrefab None (Game Object) |

现在，在让弹药按预期工作之前，StoneTower 脚本还需要对其进行一点小改动。打开 StoneTower 脚本（Scripts > Game > Tower 文件夹），并添加这些击落它们的代码！并在 `Instantiate` 行下方直接添加这些行：

```
stone.GetComponent<Stone>().enemyToFollow = targetEnemy;
stone.GetComponent<Stone>().damage = attackPower;
```

给石块弹药一个要追踪的敌人以及一个对敌人造成的伤害值。

保存脚本并返回 Unity；StoneTower 已准备就绪。点击 Apply 按钮将更改保存回预制体。

保存场景并准备迎接精彩时刻！在 Hierarchy（层级面板）中多次复制 StoneTower 并移动它们，使用吸附功能（snapping）让它们精确对齐到瓦片的中心。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_540_1.png)

点击 Play 按钮查看塔看向敌人并射击它们！现在，从场景中删除 StoneTower 及其副本并保存场景。

## Tower Manager

TowerManager 负责创建新塔，并持有不同防御塔的价格。

在 Scripts > Game > Tower 文件夹中创建一个名为 TowerManager 的新 C 脚本，并在代码编辑器中打开它。完全移除 Start() 和 Update() 方法，并在其他语句下方添加这些行：

```
using System;
using System.Collections.Generic;
using System.Linq;
```

在 `public class TowerManager : MonoBehaviour :` 正上方添加以下结构体：

```
[Serializable]
public struct TowerCost
{
    public TowerType TowerType;
    public int Cost;
}
```

这将允许脚本使用一个外部的、易编辑的价格列表。

现在，在类内部添加此代码：

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

第 19 章：制作防御塔

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

以下是它的工作原理：

- 1. 这是另一个单例，该脚本的静态引用被存储在 Instance 中。
- 2. 存储了塔预制体的引用，用于生成新的实例。
- 3. 在列表中存储每种类型防御塔的价格。
- 4. 将 Instance 变量设置为此脚本。
- 5. 接受一个塔槽位（slot）和一个塔类型作为参数，并在塔槽位的位置创建所选塔的新副本。它还会禁用该槽位，以便你无法在同一个槽位上放置两个塔。
- 6. 一个 LINQ 工具方法，用于轻松获取某种类型塔的价格。

现在保存脚本并回到 Unity。

在 Hierarchy 中，创建一个空 GameObject。将其命名为 TowerManager 并将其父级设置为 Managers。在 Inspector 面板中使用 Add Component 按钮搜索并将 TowerManager 脚本添加到其上。

raywenderlich.com

543

Unity Games by Tutorials

第 19 章：制作防御塔

| Tower Manager (Script) | |
| :--- | :--- |
| Script | TowerManager |
| Stone Tower Prefab | None (Game Object) |
| Fire Tower Prefab | None (Game Object) |
| Ice Tower Prefab | None (Game Object) |
| Tower Costs | |
| Size | 0 |

从 Prefabs ▸ Tower 文件夹将 StoneTower 预制体拖动到 Stone Tower Prefab 字段上。

| Tower Manager (Script) | |
| :--- | :--- |
| Script | TowerManager |
| Stone Tower Prefab | None (Game Object) |
| Fire Tower Prefab | None (Game Object) |
| Ice Tower Prefab | None (Game Object) |
| Tower Costs | |
| Size | 0 |
| | Add Component |

其他塔还没有准备好，所以暂时忽略另外两个塔字段。将 Tower Costs 的 Size 设置为 3：

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

按如下方式更改列表：

- 保留第一个条目的 Tower Type 为 Stone，并将其 Cost 更改为 100。
- 将第二个 Tower Type 设置为 Fire，并将 Cost 更改为 200。
- 将最后一个 Tower Type 更改为 Ice，并将 Cost 设置为 150。

raywenderlich.com

544

Tower Manager 现在可以使用了！但在你购买新塔之前，Screen Canvas 的子物体 AddTowerWindow 需要一个脚本来将其 UI 与 TowerManager 关联。

## 链接 UI

在 Scripts > Game > UI 文件夹中创建一个名为 AddTowerWindow 的新 C 脚本。打开脚本并在顶部添加内容：

```
using System;
```

现在移除 Start() 和 Update() 方法，并在它们的位置插入以下块：

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

以下是每个注释引的内容：

- 1. 指向应该建造塔的槽位的引用。
- 2. AddTower() 方法接收单个字符串参数：塔的类型。
- 3. 将传递的字符串参数转换为 TowerType 枚举。该方法不直接将 TowerType 作为参数的原因是因为事件触发器（Event Triggers）不支持枚举。
- 4. 检查玩家是否有足够的黄金购买该塔。
- 5. 从玩家的黄金中减去塔的价格。
- 6. 在 TowerManager 上调用 NewTower() 并禁用 AddTowerWindow。

545

Unity Games by Tutorials

AddTowerWindow 脚本已完成。保存它并返回 Unity。

在 Hierarchy 中，选择并启用 AddTowerWindow，它是 Screen Canvas 的子 GameObject。在 Inspector 面板中使用 Add Component 搜索并将 AddTowerWindow 脚本添加到其上，或者从 Project 面拖入。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_545_0.png)

将 Hierarchy 中的 TowerSlot 拖到 Inspector 面板中的 TowerAddToTo 字段中。

是时候链接按钮以允许以后创建塔了。

在 Hierarchy 中，展开 GameObject AddTowerWindow，展开其子 GameObject HorizontalLayout。选择其子 BtnStoneTower，并将 Hierarchy 中的 AddTowerWindow 拖到 On Click () Object 字段中。

点击方法下拉菜单——即当前显示为 No Function 的下拉菜单。在方法下拉菜单中选择 AddTowerWindow.AddTower(string)。在下拉菜单下方的参数字段中，如果没有自动插入，请插入 Stone。

选择 BtnFireTower。像对 stone 执行的那样，但在下拉菜单下方的参数字段中插入 Fire。

最后，选择 BtnIceTower。像对 stone 和 fire 执行的那样，但这次在下拉菜单下方的参数字段中插入 Ice。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_545_1.png)

按钮现在已准备就绪。禁用 AddTowerWindow GameObject 并进入下一部分，这样你就可以真正建造防御塔了！
