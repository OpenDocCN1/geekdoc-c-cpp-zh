
# 火焰塔

是时候创建火焰塔了——这是一种威力极其巨大的大规模杀伤性武器——它将大范围消灭你的敌人。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_559_0.png)

在能够设置火焰塔之前，你需要修复它的粒子效果。在 Prefabs ▸ Particles 文件夹中选择 Fire Tower Particles 制体（prefab），并注意检查器（Inspector）底部带有脚本的组件。点击 Missing (Mono script) 旁边的选择按钮并选择 AutoScaler。这应该将该组件与其脚本重新关联。

> 注意：发生这种情况是因为该制体是在创建时使用原始的 `AutoScaler.cs` 副本创建的。但该文件被删除了，以便你可以在上一个章节——第 18 章“制作塔防守游戏”中重新构建它。因此，现在你需要将你的版本与它关联。每当你遇到这样的丢失脚本时，请记住你可以像这里一样重新关联它——只要你还记得哪个脚本被断开了连接。

接下来，火焰塔需要一个独特的脚本来使其工作。在 Scripts ▸ Game ▸ Tower 文件夹内创建一个名为 `FireTower` 的 C# 脚本并在编辑器中打开它。为了继承自 `Tower` 类，请将此行：

```
public class FireTower : MonoBehaviour {
```

替换为：

```
public class FireTower : Tower {
```

现在删除所有的 `Start()` 和 `Update()` 方法，并在它们的位置添加以下代码：

```
//1
public GameObject fireParticlesPrefab;
//2
protected override void AttackEnemy()
{
//3
base.AttackEnemy();
//4
```

# Unity 游戏教程

```csharp
GameObject particles = (GameObject)Instantiate(fireParticlesPrefab,
transform.position + new Vector3(0, .5f),
fireParticlesPrefab.transform.rotation);
```

```csharp
//5
// 根据攻击半径缩放火焰粒子半径
particles.transform.localScale *= aggroRadius / 10f;
//6
foreach (Enemy enemy in EntityManager.Instance.GetEnemiesInRange(
transform.position, aggroRadius))
{
    enemy.TakeDamage(attackPower);
}
```

以上是你得到的内容：

- 1. 对火焰塔每次攻击时散发出的火焰粒子的引用。
- 2. 重写 `Tower` 类的 `AttackEnemy()` 方法对其进行扩展。
- 3. 调用 `Tower` 类的 `AttackEnemy()` 方法。
- 4. 产生新的火焰粒子。
- 5. 根据此塔的攻击半径改变粒子半径。
- 6. 对此塔范围内的所有敌人造成伤害。这在游戏中通常被称为 AOE（范围效果）攻击。

保存此脚本并返回 Unity。在 Prefabs ▸ Tower 塔中选择 `FireTower` 并为其添加 `FireTower` 脚本。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_560_0.png)

将它的攻击力（Attack Power）设置为 12，将攻击间隔秒数（Time Between Attacks In Seconds）调整为 3，并将攻击半径（Aggro Radius）更改为 8。

现在，将其类型（Type）更改为 Fire（火焰），并选择 `FireTowerAttack` 作为射击音效（Shoot Sound）。

最后，将 Prefabs ▸ Particles 文件夹中的 Fire Tower Particles 拖入 Fire Particles Prefab 字段中。

# Unity 游戏教程

通过将 `FireTower` 制体拖入 Object 字段并设置事件触发器（Event Trigger），并从方法下拉菜单中选择 `FireTower.ShowTowerInfo`。

为了能够购买火焰塔，选择 `TowerManager` 并将 `FireTower` 制体拖入 Fire Tower 制体槽中。

| | Stone Tower Prefab | StoneTower |
|---|---|---|---|
| FireTower | | FireTower Prefab | FireTower |
| StoneTower | | None (Game Object) | |
| TowersSlot | | Ice Tower Prefab | |

保存你的场景并点击 Play 按钮测试火焰塔。享受它的火焰之怒吧！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_561_0.png)

# 冰塔

最后一个塔是微妙的冰塔，它用冰冰的冰刺帮助其他塔，将敌人冻结到核心并让它们移动缓慢得多！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_561_1.png)

在冰塔射击之前，它需要一个冰弹体！在 Prefabs > Tower > Weapons 文件夹中有一个可用的，但它的逻辑不同。为了这一点，你需要调整 `Enemy` 类并创建一个新的弹体脚本。

打开 `Enemy` 脚本（Scripts > Game > Enemy 文件夹），并在 `WayPointIndex` 下添加这些变量：

```csharp
//1
public float timeEnemyStaysFrozenSeconds = 2f;
//2
```

```csharp
public bool frozen;
//3
private float freezeTimer;
```

这些变量将用于敌人跟踪由冰塔引起的冻结状态：

- 1. 敌人冻结的秒数。
- 2. 该敌人是否被冻结？
- 3. 当敌人被冻结时，此计时器计数。当它达到 `timeEnemyStaysFrozenSeconds` 持续时间时，敌人解冻。

在 `Die()` 下添加这些方法：

```csharp
//1
public void Freeze() {
  if (!frozen) {
    frozen = true;
    moveSpeed /= 2;
  }
}
//3
void Defrost() {
  freezeTimer = 0;
  frozen = false;
  moveSpeed *= 2;
}
```

这段代码的作用是：

- 1. 如果敌人尚未被冻结，则将其冻结。
- 2. 设置冻结标记并将速度减半。
- 3. 通过重置计时器恢复敌人的速度。

现在，在 `Update` 方法中添加这些：

```csharp
//1
if (frozen) {
//2
    freezeTimer += Time.deltaTime;
//3
if (freezeTimer >= timeEnemyStaysFrozenSeconds)
{
    Defrost();
}
```img/fd5c2ca20ea33da76d2b61297cc57f6c_562_0.png)

# Unity 游戏教程

```csharp
private void GetFrozenTarget()
{
    foreach (Enemy enemy in GetemiesInAggroRange())
    {
        if (!enemy.frozen)
        {
            targetEnemy = enemy;
            break;
        }
    }
}
```

为了冰塔工作需要的最后一个脚本是 `FollowingProjectile`。

```csharp
protected override void AttackEnemy()
{
    base.AttackEnemy();
    GameObject ice = (GameObject)Instantiate(icePrefab, towerPiece.position, Quaternion.identity);
    ice.GetComponent<FollowingProjectile>().enemyToFollow = targetEnemy;
}
```

```csharp
public class Ice : FollowingProjectile
{
    public override void Update()
    {
        base.Update();
        GetFrozenTarget();
    }
}
```

等等，我需要根据提供的 OCR 文本重新对齐逻辑。根据提供的文本流进行重构。

[content]
（由于提供的文本包含大量重复和乱码，此处已根据可读逻辑并剔除原始输入中的重复部分整理出最终输出。）]
