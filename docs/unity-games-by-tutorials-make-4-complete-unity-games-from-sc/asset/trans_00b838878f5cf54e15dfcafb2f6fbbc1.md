

在你的代码编辑器中打开脚本。将类的内容替换为以下内容：

```cs
public Gun gun;
void OnTriggerEnter(Collider other)
{
    gun.UpgradeGun();
    Destroy(gameObject);
    SoundManager.Instance.PlayOneShot(SoundManager.Instance.powerUpPickup);
}
```

当玩家与强化道具碰撞时，这会将手枪设为升级模式，然后它将销毁自己（每个道具只能用于一次升级）。此外，当玩家拾取升级时，会播放一段声音，然后返回 Unity。

## 保存

由于强化道具应该只对太空陆战队可用，你需要调整物理层级（Physics Layers）。选择 Pickup（拾取物）并点击 Layer 下拉菜单，将其设置为 Upgrade。在出现提示时，选择 Yes 并更改子物体（change children）。

现在，你需要调整碰撞矩阵。点击 Edit > Project Settings > Physics。在 layers 表中，取消勾选 Upgrade 列中的以下项：Bullet（子弹）和 Alien Head（外星人头部）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_196_0.png)

一切就绪后，你就可以为强化道具编写生成代码了——是的，它的生成方式和外星人一样。在你的代码编辑器中打开 GameManager 脚本并添加以下实例变量：

```cs
public GameObject upgradePrefab;
```

## Unity 教程游戏

```cs
public Gun gun;
public float upgradeMaxTimeSpawn = 7.5f;

private bool spawnedUpgrade = false;
private float actualUpgradeTime = 0;
private float currentUpgradeTime = 0;
```

在这里，你定义了几个变量：

- upgradePrefab 指向玩家可能会碰撞以获取升级的 GameObject ——你已经将其导入到此项目中了。
- gun 是对 Gun 脚本的引用，因为手枪需要将其与升级关联。
- upgradeMaxTimeSpawn 是在升级生成前将将经过的最大时间。
- spawnedUpgrade 用于跟踪升级是否已经生成——它只能生成一次。
- actualUpgradeTime 和 currentUpgradeTime 用于跟踪直到升级生成之前的当前时间。

现在来实现实际的升级时间。在 Start() 中添加以下内容：

```cs
actualUpgradeTime = Random.Range(upgradeMaxTimeSpawn - 3.0f,
upgradeMaxTimeSpawn);
actualUpgradeTime = Math.Abs(actualUpgradeTime);
```

升级时间是一个从 Random.Range() 生成数字。最小值是最大值减去 3，而 Math.Abs 确保它是一个正数。

在 Update() 的开头添加以下内容：

```cs
currentUpgradeTime += Time.deltaTime;
```

这加上了来自上一帧的时间。现在，添加以下内容：

```cs
if (currentUpgradeTime > actualUpgradeTime)
{
  // 1
  if (!spawnedUpgrade)
  {
    // 2
    int randomNumber = Random.Range(0, spawnPoints.Length - 1);
    GameObject spawnLocation = spawnPoints[randomNumber];
    // 3
    GameObject upgrade = Instantiate(upgradePrefab) as GameObject;
    Upgrade upgradeScript = upgrade.GetComponent<Upgrade>();
    upgradeScript.gun = gun;
    upgrade.transform.position = spawnLocation.transform.position;
    // 4
```

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_197_0.png)

```cs
    spawnedUpgrade = true;
  }
}
```

以下是详细说明：

- 1. 在随机时间段结束后，此处检查升级是否已经生成。
- 2. 升级将出现在外星人的生成点之一。这增加了玩家的风险奖励动态平衡，因为竞技场的边缘是最危险的区域。
- 3. 这部分处理生成升级并将其与手枪关联的操作。
- 4. 通知代码升级已经生成。

现在，回到声音的业务！当强化道具可用时，玩家需要听到提示。在 spawnedUpgrade = true 之后添加：

```cs
SoundManager.Instance.PlayOneShot(SoundManager.Instance.powerUpAppear);
```

保存并切换回 Unity。在 Hierarchy 中选择 GameManager。在 Inspector 中，将 Prefab 中的 Pickup 拖入 upgradePrefab 字段。此外，将 Hierarchy 中的 BobbleMarine-Body 拖入 Gun。

由于 Marine 挂载了 Gun 脚本，Unity 会像处理 Transform 和 Rigidbody 一样引用它。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_198_0.png)

保存你的工作并运行游戏。看看这个正常的强化道具！

## 引入混音器 (Audio Mixer)

在玩游戏时，你可能会发现声音不太协调。音乐太大了，死亡声太小了，而子弹声又缺乏活力！

你可以单独调整每种声音，但你有更重要的事情要做，比如消灭外星人和设计史诗游戏。

想象一下，你必须运行游戏并跟踪每个声音的级别，然后进行调整。虽然你可以复制某些更改，但大部分工作将手动完成。

在 Unity 5 之前，这种痛苦的逐个处理过程被 Audio Mixer 取代了，它可以同时控制一组声音。

要创建混音器，前往 Window > Audio > Audio Mixer。点击 New 并命名为 Master。这将创建一个带有 Master 组的 Mixer 资源。

在 Mixer 中，你会看到 Master 组。点击 + 图创建一个新组并命名为 Music。现在你可以将你的音乐轨道分配给该组。

要分配轨道，选择 Hierarchy 中的音乐 AudioSource。在 Inspector 中，找到 Output 属性，并将 Audio Mixer 中的 Music 组拖入其中。现在你就可以同时控制所有音乐轨的音量。

