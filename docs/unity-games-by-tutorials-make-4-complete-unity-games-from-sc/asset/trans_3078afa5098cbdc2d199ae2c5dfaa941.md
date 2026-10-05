

# UI Manager

对于 UI Manager，在 `Scripts > UI` 文件夹下创建一个名为 `UIManager` 的新 C# 脚本，并在编辑器中打开它，删除 `Start()` 方法。

在文件顶部的 `using` 语句下方添加以下内容：

```csharp
using UnityEngine.UI;
```

在类声明下添加这些变量：

```csharp
//1
public static UIManager Instance;
//2
public GameObject addTowerWindow;
//3
public Text txtGold;
public Text txtWave;
public Text txtEscapedemies;
```

每个变量的作用如下：

- 1. UIManager 的静态引用。
- 2. AddTowerWindow 组件的引用。
- 3. 栏中 Text 组件的引用。

在变量声明下方添加以下方法：

```csharp
//1
void Awake()
{
    Instance = this;
}

//2
private void UpdateToolbar()
{
    txtGold.text = GameManager.instance.gold.ToString();
    txtWave.text = "Wave " + GameManager.instance.waveNumber + " / " +
    WaveManager.instance.enemyWaves.Count;
    txtEscapedemies.text = "Escaped Enemies " +
    GameManager.instance.escapedemies + " / " + GameManager.instance.maxAllowedEnemies;
}
```

```csharp
//3
public void ShowTowerWindow(gameObject towerSlot)
{
    addTowerWindow.SetActive(true);
    addTowerWindow.GetComponent<AddTower>().towerSlot = towerSlot;
}
```

```csharp
UtilityMethods.MoveUiElementToPosition(addTowerWindow,
    GetComponent<RectTransform>(), towerSlot.position);
```

上述代码的作用是：

- 1. 设置 UIImage 脚本。
- 2. 更新金币、波次和逃逸敌人值。
- 3. 将 Tower Slot 作为参数，将其传递给 AddTower 字段，并使用 `MoveUiElementToPosition` 方法显示。

最后，在 `Update()` 方法中调用此方法：

```csharp
UpdateToolbar();
```

这每帧更新 TopBar 中的文本。保存脚本并返回 Unity 连接各个部分。

在层级（Hierarchy）中，添加一个新的空游戏对象并命名为 `UIImage`，将其父级设置为 Managers。通过 Inspector 面板中的 Add Component 按钮或从 Project 面板为其添加 `UIManager` 脚本。将 `addTowerWindow` 拖入 AddTower 字段。然后对 Screen Canvas > TopBar 的子物体 `txtGold`、`txtWave` 和 `txtEscapedemies` 分别执行同样的操作。(img/fd5c2ca20ea33da762b612547_0.png)

现在，处理点击塔位时购买塔的功能。在层级中选择 `TowerSlot`，将 `UIImage` 拖到它的 `OnClick` 事件，并从下拉菜单选择 `UIImage > ShowTowerWindow(GameObject)`。最后，将 `TowerSlot` 拖入参数字段以传递自身。

# 第19 章：制作防御塔

点击 Apply 按钮保存你对 `TowerSlot` 制品的修改。

选择 GameManager 并将 Gold 的数量设置为 400。这将是初始金币，让玩家从开始就能购买塔。如果从零开始，这个游戏将毫无意义！

点击 Play 按钮并测试塔位。点击它时，AddTower 窗口应该出现，点击石头塔图标时，该处应该建造一座塔！(img/fd5c2ca20ea33da762b612548_0.png)

该功能运行后，最好的想法是制作所有的塔位并进行整理。在层级中，创建一个命名为 `TowerSlots` 的空游戏对象。重置其 Transform并将 `TowerSlot` 拖入 `TowerSlots` 成为其子物体。

现在，按住 Ctrl 复制 `TowerSlot` 并移动复制品，直到覆盖所有这些位置：(img/fd5c2ca20ea33da762b612548_1.png)

你可以使用 Y 轴半格对齐来到达地图右上角的区域。现在保存场景，再次运行并购买一些石头塔来消灭所有敌人。当你清理了一波敌人时，你应该听到“胜利”的音效。

# 塔信息窗口与升级

**塔信息窗口**允许玩家检查塔的等级，并在负担得起时对其升级。(img/fd5c2ca20ea33da762b612549_0.png)

你可以在场景的 Screen Canvases 子物体中找到该窗口；目前它只是一个没有任何功能的窗口。要添加该功能，在 `Scripts > Game > UI` 文件夹创建一个名为 `TowerInfoWindow` 的新 C# 脚本并在编辑器中打开它。

```csharp
using UnityEngine.UI;
```

在类声明下添加这些变量：

```csharp
public Tower tower;
public Text txtInfo;
public Text txtCost;
private int upgradePrice;
private GameObject btnUpgrade;
```

每个变量的作用如下：

- 1. 可升级塔的引用。
- 2. 显示信息的 Text 组件。
- 3. 升级塔的成本。
- 4. 升级按钮的引用。

在变量声明下方添加以下方法：

```csharp
void Awake()
{
    // 不需要
}

void OnEnable()
{
    UpdateInfo();
}

private void UpdateInfo()
{
    txtInfo.text = tower.type + " Lv " + tower.level;
    upgradePrice = Mathf.CeilToInt(tower.GetPrice() * tower.level);
    if (tower.level < 3)
    {
        btnUpgrade.SetActive(true);
        txtCost.text = "Upgrade\n" + upgradePrice + " Gold";
    }
    else
    {
        btnUpgrade.SetActive(false);
    }
}

public void UpgradeTower()
{
    if (GameManager.Instance.gold >= upgradePrice)
    {
        GameManager.Instance.gold -= upgradePrice;
        tower.LevelUp();
        gameObject.SetActive(false);
    }
}
```

```csharp
public void ShowTowerWindow(Tower tower)
{
    GetComponent<TowerInfoWindow>().tower = tower;
    gameObject.SetActive(true);

    UtilityMethods.MoveUiElementToTowerPosition(gameObject,
        GetComponent<RectTransform>(), transform.position);
}
```

```csharp
public void ShowTowerInfo()
{
    UIManager.Instance.ShowTowerWindow(this);
}
```

升级系统最后一个需要编辑的脚本是 Tower 脚本。在编辑器中打开它，并在 LevelUp() 下方添加此方法：

