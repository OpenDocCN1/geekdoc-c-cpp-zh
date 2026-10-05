

# 教程 Unity 游戏

# 第 8 章：收尾工作

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_226_0.png)

它们已经在运行了，但会穿过地板，所以显然你需要对粒子进行特殊处理。你可以让粒子与世界碰撞，但在这种情况下，设置一个死亡地板更有意义。

在 Hierarchy（层级）中，选择 BobbleArena。点击 Create（创建）按钮，选择 3D Object 并选择 Plane（平面）。将其命名为 DeathFloor（死亡地板）并拖入 BobbleArena。将 Position（位置）设置为 (8.66, -0.16, 12.15)，Scale（缩放）设置为 (-14.9, 0.5, 15.6)。取消勾选 Collider（碰撞器）和 Mesh Renderer（网格渲染器）。

在 Hierarchy 中，选择 AlienDeathParticles。你会发现那里有许多关于粒子的选项。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_226_1.png)

点击 Collision（碰撞）部分将其展开——如果你没看到，请向下滚动。将 DeathFloor 拖到 Planes（平面）属性上。

| | | |
|---|---|---|
| Planes | DeathFloor (Transform) | |
| Visualization | Solid | |
| Scale Plane | 1.00 | |

点击 Play（播放）按钮。血液将汇聚在新的地板上了！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_227_0.png)

现在你必须处理一个小小的渲染问题。在这种情况下，Unity 渲染地板下方的粒子，因为它在绘制完粒子*之后*才绘制了地板。

为了避免这种情况，你需要将粒子分配到一个 Sorting Layer（排序层），它将决定 Unity 渲染对象的顺序。通常，你会在 Unity 2D 中使用这些，但在 3D 游戏中，排序层也有其用例。

展开粒子系统的 **Renderer**（渲染器）部分。在 **Sorting Layer** 属性中，选择 **Add Sorting Layer...**。Inspector（检查器）将变为 **Tags & Layers**（标签与层）。点击 + 并排序层命名为 **Foreground**（前景）。

| Sorting Layers |
|---|---|
| Layer | Default |
| Layer | Foreground |

返回 **Renderer** 模块，在 **Sorting Layer** 中，选择 **Foreground** 属性。记住，你需要对太空陆战（space marine）执行相同的操作。

现在点击 **Apply**（应用）按钮将更改应用于预制体（prefab）。

你发现了一个新问题：死亡地板没有添加到预制体，因为它是场景中的一个实例，而你的 Alien 预制体并不知道它的。稍后我们会处理这个问题。

同时，也给你的英雄加点血。将 MarineDeathParticles 预制体作为 BobbleMarine-Body 的子物体。将 Position 设置 (-1.68, 5.29, 0.63)，Rotation（旋转）设置为 (-90, 0, 0)。

在粒子系统中，展开 Collision 部分，并将 DeathFloor 拖到 Planes 属性上。在 Renderer 部分，将 Sorting Layer 设置为 Foreground。

点击 Play 按钮，看到太空陆战像喷泉一样喷血。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_228_0.png)

外星人和太空陆战的粒子系统已就绪；你只需要在代码中激活它们。

## 在代码中激活粒子

Unity 允许在代码中对粒子系统进行各种调整。在你的情况下，只需要知道粒子系统是否运行。

在 Project（项目）视图中，选择 Scripts 文件夹并点击 Create 按钮。选择 C# Script 并命名为 DeathParticles。在编辑器中打开该脚本。

添加以下实例变量：

```
private ParticleSystem deathParticles;
bool didStart = false;
```

deathParticles 指向当前的粒子系统，didStart 让你知道粒子系统已开始播放。

你需要获取粒子系统的引用，因此在 Start() 中添加以下内容：

```csharp
deathParticles = GetComponent<ParticleSystem>();
```

添加以下方法：

```csharp
public void Activate(){
    didStart = true;
    deathParticles.Play();
}
```

这会启动粒子系统并通知脚本它已开始。在 Update() 中添加以下内容：

```csharp
if (didStart && deathParticles.isStopped){
    Destroy(gameObject);
}
```

一旦粒子系统停止播放，脚本就会删除死亡粒子，因为它们只需播放一次。

最后，为了解决在代码中设置碰撞面的需求，添加以下方法：

```csharp
public void SetDeathFloor(GameObject deathFloor){
    if (deathParticles == null){
        deathParticles = GetComponent<ParticleSystem>();
    }
    deathParticles.collision.SetPlane(0, deathFloor.transform);
}
```

脚本首先检查粒子系统是否已加载，这是必要的，因为 Alien 预制体会被实例化并立即使用。

在 Start() 中 deathParticles 还没有被填充，这行代码填充了它。然后它设置了碰撞平面。

现在来激活粒子——外星人和太空陆战的过程类似，但外星人需要一些设置工作。

首先，你需要获取粒子系统的引用，它是 Alien GameObject 的子物体，所以你需要代码来获取它。

在你的代码编辑器中打开 Alien，添加以下内容：

```csharp
private ParticleSystem deathParticles;
```

在，首先，你需要获取粒子系统的引用，它是 Alien GameObject 的子物体，所以你需要代码来获取它。

在你的代码编辑器中打开 Alien，添加以下实例变量：

```csharp
private ParticleSystem deathParticles;
```

然后，创建以下方法：

```csharp
public ParticleSystem GetParticles()
{
    if (deathParticles == null)
    {
        deathParticles = GetComponentInChildren<ParticleSystem>();
    }
    return deathParticles;
}
```

魔法发生在 GetComponentChildren()。它返回找到的第一个。

在 Die 中在 Destroy(gameObject) 之前添加以下内容：

```csharp
if (deathParticles)
{
    deathParticles.parent = null;
    deathParticles.Activate();
}
```

这会在外星人死亡时产生血溅。否则，粒子会随 GameObject 一起销毁。

在 GameManager 中添加：

```csharp
public GameObject deathFloor;
```

在 Start() 中 alienScript 之后添加：

```csharp
GetParticles().SetDeathFloor(deathFloor);
```

现在激活粒子——外星人和太空陆战的过程类似，但外星人需要一些设置工作。

首先，你需要获取粒子系统的引用，它是 Alien GameObject 的子物体，所以你需要代码来获取它。

在你的代码编辑器中打开 Alien，添加以下实例变量：

```csharp
private ParticleSystem deathParticles;
```

在 Start() 中添加以下内容：

```csharp
deathParticles = GetComponentInChildren<ParticleSystem>();
```

最后，在 Die() 中在 Destroy() 之前添加以下内容：

```csharp
deathParticles.Activate();
```

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_231_0.png)

现在是太空陆战。在 Hierarchy 中选择 MarineDeathParticles 并点击 Add Component。在 scripts 下选择 DeathParticles。接下来，在编辑器中打开 PlayerController。

添加以下实例变量：

```csharp
private ParticleSystem deathParticles;
```

在 Start() 中添加以下内容：

```csharp
deathParticles = gameObject.GetComponentInChildren<ParticleSystem>();
```

最后，在 Die() 中在 Destroy() 之前添加以下内容：

```csharp
deathParticles.Activate();
```

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_231_1.png)

恭喜！你输掉了游戏！

## 赢得游戏

幸运的是，你有另一种方法避免掉脑袋。

胜利序列将如下运行：

- 当太空陆战杀死所有外星人时，舱门打开，电梯升起。
- 一旦太空陆战进入电梯，电梯就会升到天花板——也许是将太空陆战提升到不死状态或下一个关卡。谁知道呢？

深呼吸，拿起你的咖啡因饮料——你处于最后的冲刺阶段！

这部分是对你目前为止所学内容的很好的回顾。

首先，你需要为电梯门创建一个碰撞器，以便它知道玩家何时站在上面。

在 Hierarchy 中，选择 BobbleArena 并点击 Add Component。在 Physics 分类下选择 Sphere Collider。

首先，勾选 **is Trigger** 复选框。接下来，将 **Center** 设置为 (0, 0.22, 0)，**Radius** 设置为 1.65。确保取消勾选组件使其非激活状态。它只需要在太空陆战清理区域时处于激活。

接下来，点击 Add Component 并选择 New Script。将其命名为 Arena 并点击 Create and Add。在编辑器中打开该脚本。

```csharp
public GameObject player;
public Transform elevator;
private Animator arenaAnimator;
private SphereCollider sphereCollider;
```

