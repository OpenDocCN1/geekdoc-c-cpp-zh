

# Unity 教程游戏制作

在你的代码编辑器中打开 GameManager，并在 `Update()` 函数中的任何现有代码之前添加以下内容：

```cs
if (player == null) {
  return;
}
```

如果没有玩家，GameManager 将不会生成敌人。保存并切换到 Unity。

运行你的游戏并冲向外星人。过段时间后，陆战员成功地失去了那个头颅。为什么陆战员的身体还站在那里？

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_219_0.png)

这种奇怪的行为是由于重力和缩放导致的。典型的重力水平设置为 -9.81。如果你将模型缩放为每个单位一米，那么它们就能与重力良好配合。然而，你的模型尺寸大大了一些。你可以通过缩小模型或放大重力来修复这个问题——在本书中，我们将放大重力。

点击 Edit（编辑） > Project Settings（项目设置）Physics（物理），并将 Gravity（重力）设置为 (0, -900, 0)。

| Gravity | X:0 | Y:-900 | Z:0 |
|---|---|---|---|
| Default Material | None (Physics Material) | | |
| Bounce Threshold | 2 | | |
| Sleep Threshold | 0.005 | | |
| Default Contact Offs | 0.01 | | |

现在，玩家的死亡会让头部和身体像你在《权力的游戏》某集剧剧中看到的那样掉落。

# 管理脚本执行顺序

当你运行游戏时，可能会在控制台中看到一个空引用异常（null reference exception）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_220_0.png)

这一行指向 Gun 脚本，该脚本中正在访问 SoundManager。然而，这段代码在过去是可以运行的。可能发生了什么？

```cs
void Start()
{
    audioSource = GetComponent<AudioSource>();
    audioSource.PlayOneShot(SoundManager.Instance.gunfire);
}
```

这是一个脚本执行 Bug 的示例。Gun 脚本在 SoundManager 之前加载，但 SoundManager 需要先运行才能被使用。你可以重写脚本或更改脚本的顺序。

点击 Edit（编辑） > Project Settings（项目设置） > Execution Order（执行顺序）。你将看到以下对话框：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_220_1.png)

在中间，你会看到一个名为 Default Time（默认时间）的框。默认情况下，脚本在你的游戏中加载。你可以将脚本排在默认时间之前或之后。

点击 + 号添加新脚本并选择 Gun 脚本。

# Unity 教程游戏制作

## 第 8 章：最后的润色

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_221_0.png)

接下来，添加 SoundManager 脚本。你现在会看到有两个脚本，其中 Gun 先加载，SoundManager 后后加载。数字表示顺序。你可以手动更新此值，但不如将 SoundManager 拖到 Gun 脚本上方。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_221_1.png)

如果你需要脚本在任何脚本之前加载，也可以将这些脚本拖到 Default Time 框上方。目前，保持脚本现状。现在，一切准备就绪，点击 Apply（应用）按钮。

### 斩掉外星人的头

外星人也有摇头，所以它们应该以英雄相同的方式死去，但你可以对那些可怜的外星人头玩点小花。打开 Alien 脚本并添加以下实例变量：

```cs
public Rigidbody head;
public bool isAlive = true;
```

`head` 将帮助你发射头部，`isAlive` 将跟踪外星人的状态。将 Die() 替换为以下内容：

```cs
public void Die()
{
    isAlive = false;
    head.GetComponent<Animator>().enabled = false;
    head.isKinematic = false;
    head.useGravity = true;
    head.GetComponent<SphereCollider>().enabled = true;
    head.gameObject.transform.parent = null;
    head.velocity = new Vector3(0, 2.0f, 0.0f);
}
```

这段代码的作用与陆战员的死亡类似，但你禁用了外星人的 Animator。此外，这段代码会将头部从身体上发射出去。在结束括号之前添加这段代码：

```cs
OnDestroy.RemoveAllListeners();
SoundManager.Instance.PlayOneShot(SoundManager.alienDeath);
Destroy(gameObject);
```

此代码块通知监听者，移除它们，然后删除 GameObject。你想要确保不要多次调用 Die()，所以按如下方式修改 `OnTriggerEnter(Collider other)`：

```cs
void OnTriggerEnter(Collider other)
{
    if (isAlive)
    {
        Die();
        SoundManager.Instance.PlayOneShot(SoundManager.alienDeath);
    }
}
```

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_222_0.png)

在这里你首先检查 `isAlive`。最后，在 `Update()` 中，用类似的检查包围现有代码，以查看外星人是否存活。

```cs
if (isAlive)
{
    ...
}
```

保存并切换到 Unity。在 Project 视图中，点击 Alien prefab 旁边的展开三角形以显示其子物体，并选择 BobbleEnemy-Head。点击 Add Component（添加组件）按钮并从物理类别中选择 Rigidbody。取消勾选 Use Gravity（使用重力）选项并勾选 Is Kinematic（运动学模式）。

再次点击 Add Component，从物理类别中选择 Sphere Collider。将 Center（中心）设置为 (0, 0, 0.02)，Radius（半径）设置为 0.03。通过取消勾选组件复选框禁用组件。

最后，分配到层 Alien Head 并在提示时选择 Yes 修改子物体。

在 Project 视图中选择 Alien prefab。在 Inspector（检检器）中，将 BobbleEnemy-Head 拖到 head 属性中。

运行游戏。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_223_0.png)

积聚大量离体外星人头部并不需要多久。一段时间后，陆战员将难以区分死的外星人和活着的外星人。

将其命名为 SelfDestruct 并点击 Create（创建）。在编辑器中替换类内容如下：

```cs
public float destructTime = 3.0f;
public void Initiate()
{
    Invoke("selfDestruct", destructTime);
}

private void selfDestruct()
{
    Destroy(gameObject);
}
```

这会在指定的时间内删除该 GameObject。现在，玩家的死亡会让头部和身体像你在《权力的游戏》某集剧中看到的那样掉落。

### 添加粒子

你相信这个过程是如此干净吗？通常我们会使用粒子来创建火、水等效果。玩过带有雪效果的游戏吗？大多数情况下，粒子是由粒子发射器产生的。粒子是一个你应该深入研究的话题。

> **注意：** 如果你想深入探索 粒子系统，请查看我们的免费介绍：https://raywender.com/introduction-particle-systems

在 Project 浏览器中，将 AlienDeath 的实例拖入场景。你会看到外星血喷溅而出。真恶！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_225_0.png)

在 Hierarchy 中选择它，你会在 Scene 视图中看到一个带有几个选项的对话框。

| Particle Effect | | |
|---|---|---|
| Play | Restart | Stop |
| Playback Speed | 1.00 | |
| Playback Time | 0.00 | |
| Particles | 0 |
| Speed Range | 0.6 - 0.0 |
| Simulate Layers | Nothing | |
| Resumable | ✓ | |
| Show Bounds | | |

此面板允许你在构建粒子效果时实时调整设置。点击 Play 按钮。你会看到血液再次溅，并注意到按钮变成了 Pause。你还有一个 Stop 按钮可以结束粒子效果。

临时将 Alien prefab 拖入场景，并在 Hierarchy 中将 AlienParticles 拖入使其成为 Alien。选中 AlienParticles，将 Position 设置为 (0, 1.07, -1.7)，Rotation 设置为 (-90, 0, 0)。点击 Apply 按钮将更改应用到 AlienDeathParticle prefab。

通过选择 Hierarchy 中的 Alien 并点击 Inspector 中的 Apply 按钮，也将更改应用到 Alien prefab 的所有实例上。

现在，点击 Hierarchy 中的 AlienParticles 并点击 Play 按钮，看到外星人沐浴在绿血中。

