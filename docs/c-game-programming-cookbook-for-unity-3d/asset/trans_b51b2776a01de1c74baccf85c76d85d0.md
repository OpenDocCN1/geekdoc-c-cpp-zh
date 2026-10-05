

weaponControl=myGO.GetComponent<Standard_SlotController>();

该类提供了此选项，仅当指定的渲染器（renderer）位于屏幕上时发射武器。其意图是使用主要的敌人网格渲染器，这样只有当敌人出现在屏幕上时才会发射武器。如果 `Renderer` 类型的变量 `renderToTestAgainst` 没有在 Unity 编辑器检查器（Inspector）中设置，代码将使用 `GameObject.GetComponentInChildren()` 尝试寻找一个可用的渲染器：

```
if (renderToTestAgainst==null)
{
    // 我们需要一个渲染器来判断我们是否
    // 在屏幕上，所以如果我们还没有在编辑器中
    // 设置它，就尝试在子物体中寻找一个
    renderToTestAgainst=myGO.GetComponentInChildren<Renderer>();
}
```

该敌人的玩家管理器将用于处理该敌人的血量。该敌人在技术上并不是玩家，但它共享了一些脚本和行为，两种类型之间的某些模糊行和某些脚本是可以互换的。由于它将要发射射物，它很可能会受到这些射物的击中，`BaseArmedEnemy.cs` 脚本本身不处理健康值，但在第 14 章中，我们将看到一个派自此脚本的脚本为健康和击中添加完整支持。

`myPlayerManager` 持有 `BasePlayerManager` 脚本的引用，如果它在 Unity 检查器窗口未设置（导致其值为 null），则在此代码中进行填充：

```
// 如果编辑器中没有设置玩家管理器，让我们尝试
// 寻找一个
if (myPlayerManager==null)
{
    myPlayerManager=myGO.AddComponent<BasePlayerManager>();
}
```

一旦建立了对管理器脚本的引用，就会为该敌人设置一些默认属性，包括用于血量的整数变量 `thisEnemyStrength`：

```
myDataManager=myPlayerManager.DataManager;
myDataManager.SetName("Enemy");
myDataManager.SetHealth(thisEnemyStrength);
```

当 `Init()` 完成后，`canFire` 允许该敌人从现在开始发射，并且 `didInit` 被设置为 `true`，以便其他函数或脚本可以此 `Init()` 函数已完成：

```
canFire=true;
didInit=true;
```

由于大部分核心逻辑都发生在 `Update()` 函数中（该函数由 Unity 引擎每帧自动调用），因此在这里被声明为 `virtual` 函数，几乎肯定会被任何派自 `BaseArmedEnemy` 类的类所重写：

```
public virtual void Update()
{
```

如果 `canControl` 为 `false`，则不允许控制武器，因此此函数将提前退出：

```
// 如果我们被允许控制武器，我们就退出
// if(canControl)
    return;
```

拥有一个会跳出此函数的 `canControl` 变量，外带一个用于决定是否实际执行发射代码的变量，似乎是多余的，但其法为了一致性；所有的玩家脚本都使用 `canControl`，这里也使用了它。该脚本目前的形式只处理武器控制，没有什么能阻止它在以后增长为更复杂的东西。为了确保脚本在未来使用中保持扩展性，发射逻辑取决于 `thisGameGameObjectShouldFire` 是否设置为 `true`：

```
if(thisGameGameObjectShouldFire)
```

取决于该敌人当前设置使用的 `AIAttackState`，可能要求在发射之前能够对潜在目标拥有视线。`doFire` 是一个布尔变量，用于告诉发射条件（如视线）是否已满足以及允许发射。在开始检查发射条件之前，会假设将允许发射，并将 `doFire` 设置为 `false`：

```
// 我们使用 doFire 来决定现在
// 是否发射
dofire=false;
```

发射之间总会有一次停顿。布尔变量 `canFire` 用于确定此时是否应该允许脚本发射。

```
if( canFire )
{
```

`AIAttackState.random_fire` 顾如其名——除了生成一个随机数并查看它是否大于设定数字（在本例中为98）之外没有其他检查。当随机数足够大时，`doFire` 被设置为 `true`，以便：

```
AIAttackState.random_fire
{
    if(Random.Range(0,100) > 98)
    {
        doFire=true;
    }
}
else
{
    doFire=false;
}
```

