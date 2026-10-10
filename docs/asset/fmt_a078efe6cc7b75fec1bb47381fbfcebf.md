
## Unity 游戏制作教程

在代码编辑器中打开 `GunEquipper` 脚本。在其他变量声明下方添加以下内容：

```
[SerializeField]
Ammo ammo;
```

现在来使用这个变量。在 `loadWeapon()` 方法的结束大括号之前添加以下内容：

```
gameUI.SetAmmoText(ammo.GetAmmo(activeGun.tag));
```

这会在玩家切换武器时更新弹药数量。然而，在编辑器中尚未分配弹药。保存你的工作，并切回 Unity。

选择 `Player` 游戏对象（`GameObject`），并将其拖到 `GunEquipper` 组件的 `Ammo` 字段上：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_309_0.png)

在代码编辑器中打开 `Game` 脚本，在类的起始大括号之后添加以下变量：

```
public GameUI gameUI;
public GameObject player;
public int score;
public int waveCountdown;
public bool gameOver;
```

这些是你很快就会用到的引用和计数值。其中一个值得注意的变量是 `gameOver`，它用于跟踪游戏是否结束。稍后我们会编写“游戏结束”场景的代码，但现在添加此标记是有帮助的。

在进一步编辑脚本之前，保存工作并返回 Unity。点击层级（`Hierarchy`）中的 `Game` 游戏对象。

将 `GameUI` 游戏对象拖到 `Game UI` 字段，并将 `Player` 游戏对象拖到 `Player` 字段。

## 第11 章：引入 UI

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_310_0.png)

在代码编辑器中打开 `Game` 脚本。在 `using UnityEngine;` 下方添加此导入项：

```
using System.Collections;
```

此导入将允许你使用协程。在 `SpawnRobot()` 方法的结束大括号下方添加此方法：

```
private IEnumerator updateWaveTimer()
{
    while (!isGameOver)
    {
        yield return new WaitForSeconds(1f);
        waveCountdown--;
        gameUI.SetText(waveCountdown);
    }

    // 生成下一波敌人并重启倒计时
    if (waveCountdown == 0)
    {
        SpawnRobots();
        waveCountdown = 30;
        gameUI.ShowNextWaveText();
    }
}
```

你首先检查 `isGameOver` 标记是否设置。如果没有设置，脚本将暂停一秒，然后递减 `waveCountdown` 并更新 UI。如果倒计时变为 0，你就调用 `spawn-robots` 方法，重置倒计时，然后显示消息告诉玩家新波机器人即将到来！

现在，在你刚刚添加的方法下方立即添加以下内容：

```
public static void RemoveEnemy()
{
    singleton.enemiesLeft--;
    singleton.gameUI.SetEnemyText(singleton.enemiesLeft);

    // 如果在计时器结束前清理了敌人，给玩家奖励
    if (singleton.enemiesLeft == 0)
    {
        singleton.score += 50;
        singleton.gameUI.ShowWaveClearBonus();
    }
}
```

这会在机器人杀死时被调用。它从敌人计数中移除一个机器人并更新 UI。如果没有剩余敌人，它会提醒玩家他们获得了额外分，并在分数中加上“50”。

玩家每次杀死机器人时也应该获得积分。在最后一个方法下方添加以下方法：

```csharp
public void AddRobotKillToScore()
{
    score += 10;
    gameUI.SetScoreText(score);
}
```

这会在玩家杀死机器人时给他们积分。

玩家每存活攻击的每一秒也应该获得一分。在最后一个方法下方添加以下方法：

```csharp
IEnumerator increasesScoreEachSecond()
{
    while (!gameOver)
    yield return new WaitForSeconds(1);
    score += 1;
    gameUI.SetScoreText(score);
}
```

上面是一个协程，它在游戏运行时每秒更新一次分数。

现在，你需要更新 `Start()` 来设置你的新变量。在包含 `singleton = this;` 的行之后添加以下内容：

```c
StartCoroutine("increaseScoreEachSecond");
isGameOver = false;
time.timeScale = 1;
waveCountdown = 30;
enemiesLeft = 0;
StartCoroutine("updateTimer");
```

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_311_0.png)

首先，你启动 `increaseScoreEachSecond`，然后在启动 `updateWaveTimer` 之前将所有变量初始化为起始值。

在 `SpawnRobots()` 中，结束大括号之前添加以下内容：

```
gameUI.SetText(enemiesLeft);
```

这会在生成新机器人后将敌人计数设置为最后一个值。保存你的工作，并在代码编辑器中打开 `Robot.cs`。

在这里，你需要调用刚刚创建的 `RemoveEnemy()` 方法。在调用 `StartCoroutine("DestroyRobot");` 之后立即添加以下内容：

```
Game.RemoveEnemy();
```

这将敌人计数减一并更新 UI。保存你的更改并切回 Unity。

干得好！现在你可以收获劳动的成果并点击 Play 了。到处跑跑，杀死机器人并观察敌人数量的减少。注意当你开火时弹药会减少，并在获得拾品时更新。还要查看通知玩家获得拾品的文本。被机器人击中时，你的血量也会下降。你还会看到新波敌人的警报，以及在波计时器结束前杀死所有敌人获得的奖励。波计时器将每秒倒计时，并在达到 0 时生成新敌人（并重置）。

## 添加主菜单

你几乎完成了游戏；接下来的完善工作将让它大放异彩。首先你将添加一个主菜单。在 `Scenes` 文件夹中，右键点击，选择 `Create Scene` 并命名为 `MainMenu`。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_313_0.png)

双击你想打开的场景。从 `Resources` 文件夹将 `Robot` 预制体（`prefab`）拖到层级（`Hierarchy`）。将其位置设置为 `(15, -61, 53)`，旋转设置为 `(0, 180, 0)`。这个位置在游戏开发时是一个很好的起点。回想你在层级中是如何处理 `UI > Canvas` 的，像以前一样创建一个 `Canvas` 并将其命名为 `MenuUI`。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_313_1.png)

首先我们需要创建一个按钮。在层级中右键点击，`Create UI > Button` 并将其重命名为 `BeginButton`。将锚点设置为底部居中，轴心（`pivot`）设置为 `(0.5, 0.5)`，位置设置为 `(0, 165, 0)`，宽度为 `260`，高度为 `75`。

在 `Image` 组件中，将 `Image` 设置为 `Grey_Texture`。在 `Button` 组件中，将 `Transition` 设置为 `Sprite Swap`。将 `Highlighted Sprite` 设置为 `Pink_Texture`，`Pressed Sprite` 设置为 `Black_Texture`。按钮如下所示：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_310_0.png)

## Unity 教程游戏

## 第 11 章：介绍 UI

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_316_0.png)

这创建了一个 `UnityEvent`，它允许你在点击此按钮时调用另一个函数。将 `MenuUI` 游戏体拖到该字段中以显示下拉菜单。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_316_1.png)

现在，右侧的下拉菜单会显示 `No Function`（无函数）。点击此下拉菜单并选择 `Menu -> StartGame()`。现在，当点击此按钮时，它将调用 `Menu` 脚本中的 `StartGame()`，从而加载场景。

对 `ExitButton` 重复此过程，但将它的回调设置为 `Quit` 方法。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_316_2.png)

点击 `Play` 并点击 `Begin` 按钮加载游戏。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_317_0.png)

## 音乐

如果这个游戏有一个配乐就太棒了 —— 这是你接下来要做的。

在 `MainMenu` 场景中，创建一个空游戏体并命名为 `BackgroundMusic`。创建一个 C 脚本，命名为 `BackgroundMusic` 并在代码编辑器中打开它。删除模板文本并将其替换为以下方法：

```
void Start()
{
    DestroyOnLoad(gameObject);
}
```

这确保了脚本挂载的游戏体在切换场景时不会被删除，因此当你切换到战斗时，音乐将继续播放！当你运行游戏时，会在 `Hierarchy`（层级）中看到这一变化：

保存你的更改。回到 Unity，将此脚本拖到 `BackgroundMusic` 游戏体上。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_317_1.png)

选择 `BackgroundMusic` 游戏体并添加 `Audio Source` 组件。将 `Loop` 勾选为 `Selected`，并将 `AudioClip` 设置为 `music`。现在，点击 `Play` 并点击 `Begin` 按钮。在史诗般的旋律中开始杀死机器人吧！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_318_0.png)

## 游戏结束

这个游戏几乎完成了，但它需要一个 `Game Over` 界面。打开 `Battle` 场景（在 `Scenes` 文件夹中双击）。

首先，在 `Hierarchy` 中右键点击并选择 `UI ▸ Panel` 创建 `Panel`。将其重命名为 `GameOverScreen`。将其 `Anchor Preset`（锚点预设）设置为 `middle-center`，`Position Y` 设置为 `0`，`Width` 为 `400`，`Height` 为 `500`。将 `Image` 组件中的 `SourceImage` 设置为 `Box`，并将 `Alpha` 设置为 `1`（只需点击 `Color` 框并将 A 滑动到右侧）。

`Panel` 只是另一个 UI 控件，可以用它来组织你的控件。所有后续 UI 控件将成为 `GameOverScreen` 的子物体。
