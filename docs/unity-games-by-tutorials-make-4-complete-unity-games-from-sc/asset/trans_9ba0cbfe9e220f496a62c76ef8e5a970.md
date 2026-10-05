

```cs
//5
public TowerType type;
//6
public AudioClip shootSound;
//7
public Transform towerPieceToAim;
//8
public Enemy targetEnemy = null;
//9
private float attackCounter;
```

以下是这些变量的含义：

- 1. 塔对敌人造成的伤害量。
- 2. 射击之间的冷却时间。
- 3. 塔开始锁定敌人之前，塔与敌人之间的最小距离。
- 4. 塔的等级，可以通过升级增加。
- 5. 塔的类型。
- 6. 该塔射击时播放的音效。
- 7. 应该对准敌人的 Transform（例如，头部）。
- 8. 当前正在锁定的敌人。
- 9. 这个计数器每帧都会递减。当它变为 0 时，塔可能会射击。

有很多非常有用的变量！接下来是观察和攻击。在变量声明下方添加这些方法：

```cs
private void SmoothlyLookAtTarget(Vector3 target)
{
    towerPieceToAim.localRotation = UtilityMethods.SmoothlyLook(towerPieceToAim, target);
}

protected virtual void AttackEnemy()
{
    GetComponent<AudioSource>().PlayOneShot(shootSound, .15f);
}
```

`SmoothlyLookAtTarget()` 使用 `SmoothlyLook` 工具方法来看向敌人目标。`AttackEnemy()` 仅播放音效。这是因为每个塔将实现自己的攻击方式。注意 `virtual` 关键字。这意味着任何派生自 `Tower` 的类都可以原样使用此方法、在其基础上添加内容，或完全重写它。

## Unity 游戏教程

塔需要一种方法来检测敌人并选择最近的一个作为目标。
添加以下方法：

```cs
//1
public List<Enemy> GetEnemiesInAggroRange()
{
    List<Enemy> enemiesInRange = new List<Enemy>();
    //2
    foreach (Enemy enemy in EnemyManager.Instance)
    {
        if (Vector3.Distance(transform.position, enemy.transform.position) <= aggroRadius)
        {
            enemiesInRange.Add(enemy);
        }
    }
    //3
    return enemiesInRange;
}

//4
public Enemy GetNearestEnemyInRange()
{
    Enemy nearestEnemy = null;
    float smallestDistance = float.PositiveInfinity;
    //5
    foreach (Enemy enemy in GetEnemiesInAggroRange())
    {
        if (Vector3.Distance(transform.position, enemy.transform.position) < smallestDistance)
        {
            smallestDistance = Vector3.Distance(transform.position, enemy.transform.position);
            nearestEnemy = enemy;
        }
    }
    //6
    return nearestEnemy;
}
```

以上代码的逻辑如下：

- 1. `GetEnemiesInAggroRange()` 返回此塔仇恨范围范围内所有敌人的列表。
- 2. 遍历所有敌人，并将处于范围内的敌人添加到 `enemiesInRange` 列表中。
- 3. 返回该列表。
- 4. `GetNearestEnemyInRange()` 返回距离此塔最近的敌人。
- 5. 遍历范围内的所有敌人，并持续存储最近的敌人。当遍历完整个列表后，`nearestEnemy` 将是最近的一个。
- 6. 返回最近的敌人。

`Tower` 中最大且最重要的方法是 `Update()`；它处理旋转、锁定和攻击。将它添加在其他方法下方：

```cs
public virtual void Update()
{
    //1
    attackCounter -= Time.deltaTime;
    //2
    if (targetEnemy == null)
    {
        //3
        if (towerPieceToAim)
        {
            SmoothlyLookAtTarget(towerPieceToAim.transform.position, new Vector3(0, 0, 1));
        }
        //4
        if (GetNearestEnemyInRange() != null
            && Vector3.Distance(transform.position, GetNearestEnemyInRange().transform.position) <= aggroRadius)
            targetEnemy = GetNearestEnemyInRange();
    }
    else
    {
        // 5
        // 6
        if (towerPieceToAim)
        {
            SmoothlyLookAtTarget(targetEnemy.transform.position);
        }
        //7
        if (attackCounter <= 0f)
        {
            // 攻击
            AttackEnemy();
            // 重置攻击计数器
            attackCounter = timeBetweenAttacksInSeconds;
        }
    }
    // 8
    if (Vector3.Distance(transform.position, targetEnemy.transform.position) > aggroRadius)
    {
        targetEnemy = null;
    }
}
```

这段代码为你处理了很多工作：

- 1. 递减 `attackCounter`。
- 2. 检查当前是否没有目标敌人。
- 3. 如果有需要旋转的 Transform，则看向性位置。这是塔的空闲状态。
- 4. 尝试寻找新的目标敌人。
- 5. 检查是否分配了目标敌人。
- 6. 如果有，看向目标敌人。
- 7. 如果 `attackCounter` 等于或低于零，调用 `AttackEnemy()` 并重置计数器。
- 8. 如果目标敌人移出范围，将 `targetEnemy` 设置为空。

快结束了！添加此方法以完成 `Tower` 脚本：

```cs
public void LevelUp()
{
    level++;
    attackPower *= 2;
    timeBetweenAttacksInSeconds *= 0.7f;
    aggroRadius *= 1.2f;
}
```

这会让塔升级：它通过乘法值值增加了塔的攻击力、攻击间隔和仇恨范围。

